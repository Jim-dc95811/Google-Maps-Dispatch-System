# Offline GeoStack Roadmap

## Immediate priority — repair strict Field Maps TPKX conformance

The current top engineering gate is no longer the large district-card cold test.

A live control test proved:

```text
project converter TPKX -> Field Maps REJECTED
Esri official Usa.tpkx  -> Field Maps ACCEPTED
```

Both were tested through the same physical-card `basemaps` path and same Field Maps Designer workflow.

Therefore the current defect is isolated to the project's MBTiles -> TPKX package construction.

### Resume here

1. run a **small MBTiles** through `ESRI_CANONICAL_TPKX_TEST_v0_2_0`;
2. place the new TPKX in `\Android\data\com.esri.fieldmaps\files\basemaps\`;
3. set Designer to the exact filename;
4. open it in Field Maps;
5. if it passes, promote the canonical construction as the replacement converter design;
6. integrate the corrected converter into Offline Map Factory and Rasta;
7. regenerate the district TPKX;
8. rebuild the district MMPK from that corrected TPKX;
9. resume full cold/no-Internet card acceptance.

Do not waste a district-scale rebuild before the small conformance specimen passes.

- [TPKX / Field Maps Conformance — 2026-08-20](docs/TPKX_FIELD_MAPS_CONFORMANCE_2026-08-20.md)

---

## Converter rule

Esri's official `Usa.tpkx` is the golden master.

The historical converter remains valid evidence for ArcGIS Earth compatibility, but its output failed strict Field Maps acceptance.

The repair branch copies Esri's canonical Web Mercator LOD values and native metadata conventions instead of recalculating them.

One verified deviation:

```text
LOD 0 historical scale: 591657527.5917094
LOD 0 Esri scale:       591657527.591555
```

This is a real difference, not yet proven to be the sole cause.

Governing engineering rule:

> **When an official working reference implementation exists, reproduce/conform to it first.**

---

## Offline Map Factory 1.0

**Status: BUILT / SELF-TESTED — RELEASE ACCEPTANCE BLOCKED ON TPKX CONFORMANCE.**

Current operator feature set remains:

- 4 sources: Google Earth, Google Hybrid, Esri World, Esri World / Google Labels;
- HOME EXTENT, Clipboard History diagonal points, or two manual GPS points;
- Z0-Z20;
- TPKX / MBTiles / Both;
- Advanced existing MBTiles -> TPKX;
- no REST / Static WMTS output.

The QGIS -> MBTiles side remains live-proven. The TPKX stage must use the corrected canonical converter before the new product line can be release-accepted for the broader deployment mission.

### Factory acceptance after converter repair

1. launcher starts;
2. both required QGZ references are found;
3. small MBTiles-only build;
4. small TPKX-only build;
5. small Both build;
6. Advanced MBTiles -> TPKX;
7. TPKX opens in ArcGIS Earth;
8. representative TPKX passes Field Maps when that deployment claim is made;
9. cleanup/final-output state is correct.

---

## Historical TPKX Map Factory v1.0.0

**RELEASE-ACCEPTED / FROZEN — for the tested ArcGIS Earth target.**

Do not rewrite or re-zip the accepted artifact.

The 2026-08-20 Field Maps failure does not erase the 2026-08-15 acceptance; it narrows the compatibility claim. Historical output is proven in ArcGIS Earth but cannot be represented as Field Maps-conformant.

---

## District-card mission

> **A Field Maps user must be able to open the app with zero public Internet and use a district-wide Esri Hybrid map through Z17. The same local map should stop the heavy basemap from burning cellular data when service exists.**

Intended chain after the converter passes:

```text
Offline Map Factory
-> corrected district TPKX
-> ArcGIS Pro minimal MMPK wrapper
-> physical microSD
   +-- Field Maps mappackages\DISTRICT.mmpk
   +-- Field Maps basemaps\DISTRICT.tpkx
-> Android
-> Field Maps + ArcGIS Earth Mobile
```

### Proven tonight

- Field Maps Designer workflow: LIVE-PROVEN;
- map shared Everyone/public: LIVE-PROVEN;
- physical-card basemaps path: LIVE-PROVEN;
- Esri official `Usa.tpkx`: LIVE-PROVEN in Field Maps;
- project historical converter TPKX: FAILED / NEEDS REPAIR.

### ArcGIS Pro bridge

ArcGIS Pro 3.7 packaging remains PASS for small and district-scale MMPKs. But Pro preserves the source TPKX intact, so it is not a repair mechanism. Rebuild MMPK only after corrected TPKX acceptance.

---

## ArcGIS Earth Mobile

Local TPKX remains LIVE-PROVEN on multiple project packages.

The strict Field Maps failure must not be generalized into an Earth Mobile failure.

---

## Rasta Pyramid Factory

Rasta v0.1.3 remains LIVE-PROVEN for giant-raster manufacturing and ArcGIS Earth display.

Its TPKX output inherits the historical converter lineage, so Field Maps compatibility is currently **not approved** until the canonical converter replacement is proven and integrated.

---

## Map Fountain

Map Fountain remains LIVE-PROVEN / PARKED from normal personal-phone deployment.

Preserve it for actual shared-storage needs such as Starlink/basecamp NAS or multi-client access. Do not revive it because the TPKX converter needs repair; those are separate engineering subjects.

---

## Non-goals

- guessing at TPKX metadata instead of conforming to Esri's working sample;
- rebuilding the 52 GB district products before a tiny specimen passes;
- reviving protected-folder ADB/MTP injection;
- restoring REST to the clean Factory;
- requiring router/server infrastructure for normal personal-phone deployment;
- making public Internet mandatory;
- optimizing storage elegance ahead of reliability.

## Governing rules

> **The real target decides acceptance.**

> **Esri's native TPKX is the reference; our converter conforms to it.**
