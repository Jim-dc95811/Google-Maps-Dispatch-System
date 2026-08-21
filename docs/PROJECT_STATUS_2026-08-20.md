# Offline GeoStack — Project Status — 2026-08-20

## Executive state — late checkpoint

The project's immediate bottleneck is now precisely identified.

ArcGIS Field Maps successfully accepted Esri's official `Usa.tpkx` from the physical microSD `basemaps` directory while rejecting the project's converter-built District 7 TPKX from the same workflow.

That result proves the Android storage path and Field Maps configuration. The verified defect is in the project's historical MBTiles -> TPKX output/package construction.

The current engineering priority is therefore:

```text
small MBTiles
-> Esri-canonical test converter v0.2.0
-> small TPKX
-> physical microSD
-> Field Maps
```

The district-scale rebuild and full MMPK cold-card acceptance follow only after this small conformance gate passes.

---

## Mission lock

> **A Field Maps user must be able to open the app with zero public Internet and use a district-wide Esri Hybrid map through Z17. The same local map should eliminate the need to burn cellular data on the heavy basemap when service exists.**

The user-facing value remains freedom from **map rationing**.

---

## Field Maps control test — LIVE-PROVEN workflow

The following workflow is now project-proven:

- Field Maps Designer map: `District 7 Local Basemap Test`;
- Offline: enabled;
- basemap source: **File on the device**;
- sharing: **Everyone (public)**;
- physical-card path:

```text
\Android\data\com.esri.fieldmaps\files\basemaps\
```

Esri official `Usa.tpkx` was copied to that directory, Designer was pointed at the exact filename, and Field Maps accepted it.

### Result matrix

| Test object | Result |
| --- | --- |
| Esri official `Usa.tpkx` | ✅ **FIELD MAPS PASS** |
| Project converter-built District 7 TPKX | ❌ **FIELD MAPS REJECTED — spatial reference incompatible** |

The same project converter lineage is known to open in ArcGIS Earth Windows, ArcGIS Earth Mobile on multiple project packages, and ArcGIS Pro.

Conclusion: the historical converter is **Earth-compatible but not presently Field Maps-conformant**.

---

## What package inspection showed

The rejected project TPKX reported expected-looking Web Mercator values:

- package/tile/extents SR: WKID 102100 / latestWKID 3857;
- tile size: 256 x 256;
- DPI: 96;
- standard Web Mercator origin;
- Z0-Z17 LOD sequence.

That means the failure cannot be resolved by assuming the displayed WKID is simply wrong.

A package-wide conformance check against Esri's working specimen is required.

---

## Concrete converter deviation found

The historical converter calculated Web Mercator LOD resolution/scale values.

Esri's native specimen stores fixed canonical values.

Example:

```text
LOD 0 scale
historical converter: 591657527.5917094
Esri native sample:    591657527.591555
```

That difference repeats through the LOD table.

This is a verified deviation. It is **not yet proven to be the sole cause** of the Field Maps rejection.

---

## Canonical repair candidate

A separate TEST converter was built while leaving the frozen historical converter untouched:

```text
ESRI_CANONICAL_TPKX_TEST_v0_2_0
```

The test implementation copies Esri's native/published conventions for:

- LOD 0-23 resolutions/scales;
- Web Mercator origin;
- spatial-reference structure;
- `root.json` conventions;
- `iteminfo.json` field types.

The existing Compact Cache V2 bundle writer remains because its package/bundle mechanics already passed bench inspection against the published format.

### Current evidence

- synthetic MBTiles conversion: PASS;
- ZIP/package construction: PASS;
- Compact Cache V2 bundle headers/indexes: PASS;
- Field Maps acceptance: **PENDING**.

See:

- `docs/TPKX_FIELD_MAPS_CONFORMANCE_2026-08-20.md`

---

## Offline Map Factory 1.0

Status is now more precise:

**BUILT / SELF-TESTED — RELEASE ACCEPTANCE BLOCKED ON TPKX CONFORMANCE.**

The QGIS -> MBTiles manufacturing side remains valid and live-proven.

The historical TPKX converter stage must be replaced by a Field Maps-conformant construction before the new Factory is promoted for the full current deployment mission.

Current product contract remains:

- Google Earth;
- Google Hybrid;
- Esri World;
- Esri World / Google Labels;
- HOME EXTENT / Clipboard History / manual GPS points;
- Z0-Z20;
- TPKX / MBTiles / Both;
- Advanced existing MBTiles -> TPKX;
- no REST / Static WMTS in the clean Factory.

---

## Historical TPKX Map Factory v1.0.0

Status remains:

**RELEASE-ACCEPTED / FROZEN — for the tested ArcGIS Earth target.**

The historical accepted ZIP must not be rewritten, re-zipped, or silently replaced.

The new Field Maps failure narrows the compatibility claim; it does not erase the original 2026-08-15 acceptance evidence.

---

## ArcGIS Pro MMPK bridge

ArcGIS Pro 3.7 successfully created:

- a small minimal MMPK from an existing project TPKX;
- a district-wide approximately 52 GB MMPK from the approximately 52 GB District 7 TPKX.

Small specimen observations:

- analyzer: 0 errors / 0 warnings / 0 messages;
- MMPK version: 3.0;
- original TPKX preserved intact under `commondata/new_tpkx/`;
- `.mmap` references the packaged local TPKX;
- no HTTP/HTTPS references found in the small `.mmap` / `.mapx`;
- MMPK rendered in Windows ArcGIS Earth while Earth showed Not signed in.

### Updated interpretation

The MMPK bridge is a valid packaging proof but **not a TPKX repair mechanism**.

Because Pro preserves the source TPKX intact, the approximately 52 GB MMPK built from the old converter lineage should not be treated as the next Field Maps gold object. Rebuild it after the corrected district TPKX exists.

---

## Intended district-card architecture after conformance repair

```text
Offline Map Factory
-> corrected district TPKX
-> ArcGIS Pro minimal MMPK wrapper
-> physical microSD
   +-- Android\data\com.esri.fieldmaps\files\mappackages\DISTRICT.mmpk
   +-- Android\data\com.esri.fieldmaps\files\basemaps\DISTRICT.tpkx
-> Android
-> Field Maps + ArcGIS Earth Mobile
```

Redundancy remains acceptable. Storage efficiency ranks below field reliability.

---

## ArcGIS Earth Mobile

ArcGIS Earth Mobile local TPKX remains **LIVE-PROVEN on multiple project packages**.

The strict Field Maps failure does not invalidate that evidence.

User-facing role remains:

```text
Field Maps          -> agency workflow / packaged map
ArcGIS Earth Mobile -> fast direct local TPKX viewer
```

---

## SD-card / reader lesson

The laptop built-in SD reader produced write-protection behavior on multiple cards/adapters. Another computer wrote successfully.

Treat the laptop reader as suspect.

The SD card is disposable test media. It may be renamed, rewritten, reformatted, or wiped whenever useful to prove the workflow.

---

## Current status matrix

| Capability | Status |
| --- | --- |
| Offline Map Factory 1.0 | 🟡 **BUILT / SELF-TESTED — BLOCKED ON TPKX CONFORMANCE** |
| Historical TPKX Map Factory v1.0.0 | ✅ **RELEASE-ACCEPTED / FROZEN FOR EARTH TARGET** |
| QGIS -> raster MBTiles | ✅ **LIVE-PROVEN** |
| Historical MBTiles -> TPKX in ArcGIS Earth | ✅ **LIVE-PROVEN** |
| Historical converter TPKX in Field Maps | ❌ **FAILED / NEEDS REPAIR** |
| Field Maps Designer + physical `basemaps` path | ✅ **LIVE-PROVEN** |
| Esri official `Usa.tpkx` in Field Maps | ✅ **LIVE-PROVEN** |
| Esri-canonical converter v0.2.0 | 🟡 **BUILT / SELF-TESTED — FIELD MAPS PENDING** |
| ArcGIS Pro existing TPKX -> minimal MMPK | ✅ **PASS** |
| Pro-created MMPK in Windows ArcGIS Earth | ✅ **PASS** |
| Corrected district TPKX | 🟡 **PENDING SMALL-CONFORMANCE PASS** |
| Corrected district MMPK / cold Field Maps card | 🟡 **PENDING CORRECTED TPKX** |
| ArcGIS Earth Mobile local TPKX | ✅ **LIVE-PROVEN** |
| Fire protected-folder ADB/MTP injection | ❌ **REJECTED** |
| Map Fountain | ✅ **LIVE-PROVEN / PARKED** |
| Rasta v0.1.3 core | ✅ **LIVE-PROVEN FOR EARTH TARGET** |
| TPKX -> MBTiles recovery | ❌ **REJECTED as production path** |

---

## Immediate next action — no ambiguity

1. select a small raster MBTiles;
2. run `ESRI_CANONICAL_TPKX_TEST_v0_2_0`;
3. place the output TPKX in the physical-card Field Maps `basemaps` directory;
4. point Designer to the exact filename;
5. let Field Maps decide.

### If PASS

- make canonical construction the replacement converter design;
- integrate it into Offline Map Factory;
- propagate it into Rasta's TPKX branch;
- regenerate district TPKX;
- rebuild district MMPK;
- resume cold/no-Internet district-card acceptance.

### If FAIL

Continue package-wide comparison to Esri `Usa.tpkx`. Do not guess or patch one visible field at random.

---

## Do not regress

- Do not call a package Field Maps-compatible because Earth opens it.
- Do not use ArcGIS Pro MMPK wrapping as a supposed repair of the source TPKX.
- Do not spend hours rebuilding district-scale products before the tiny canonical specimen passes.
- Do not discard the original release evidence; narrow the compatibility claim instead.
- Do not revive REST/Map Fountain because of a converter defect.
- Do not return to protected-folder ADB/MTP injection.
- Do not make public Internet an operational requirement.
- Do not invent Esri package conventions when an official working specimen exists.

## Governing rules

> **When an official working reference implementation exists, reproduce/conform to it first.**

> **The real target decides acceptance.**
