# OFFLINE GEOSTACK — AI CONTINUITY / RESTART NOTE

## Current truth — late 2026-08-20

If coming to this project cold, do **not** resume from the earlier MMPK-only acceptance plan.

The newest live evidence is a strict Field Maps TPKX control test:

```text
project converter-built TPKX -> Field Maps REJECTED
Esri official Usa.tpkx       -> Field Maps ACCEPTED
```

Both were tested through the same physical microSD `basemaps` directory and same Field Maps Designer workflow.

Therefore the current engineering subject is the **MBTiles -> TPKX package construction**, not the SD card, not Designer, not the web map, and not general Web Mercator.

Read first:

1. `docs/TPKX_FIELD_MAPS_CONFORMANCE_2026-08-20.md`
2. `docs/PROJECT_STATUS_2026-08-20.md`
3. `README.md`
4. `ROADMAP.md`
5. deployment repo `docs/FIELD_MAPS_TPKX_CONFORMANCE_2026-08-20.md`

---

## Immediate resume point

Run exactly this small acceptance before any district rebuild:

```text
small raster MBTiles
-> ESRI_CANONICAL_TPKX_TEST_v0_2_0
-> small new TPKX
-> physical microSD
-> \Android\data\com.esri.fieldmaps\files\basemaps\
-> Field Maps Designer exact filename
-> Field Maps
```

### Pass condition

Field Maps opens the new TPKX normally.

If PASS:

- canonical converter becomes replacement design;
- integrate into Offline Map Factory;
- propagate into Rasta TPKX output;
- regenerate district TPKX;
- rebuild district MMPK from corrected TPKX;
- resume cold/no-Internet district acceptance.

If FAIL:

- do not guess;
- compare package-wide against Esri official `Usa.tpkx`;
- inspect `root.json`, `iteminfo.json`, ZIP layout, top-level files, tile hierarchy, Compact Cache V2 bundle/index behavior, metadata types and conventions;
- make evidence-driven corrections only;
- let Field Maps vote again.

---

## Official specimen rule

Esri's official working `Usa.tpkx` is now the golden master for TPKX conformance.

Permanent engineering doctrine:

> **When an official working reference implementation exists, reproduce/conform to it first. Do not invent an alternative until the reference path has been exhausted.**

The project's converter gets no creative freedom where Esri has supplied a working reference.

---

## Historical converter truth

The old converter is not worthless and its prior evidence is not erased.

It remains proven for:

- ArcGIS Earth Windows;
- ArcGIS Earth Mobile on multiple project packages;
- ArcGIS Pro ingestion;
- large Compact Cache V2 production workloads.

But it failed strict ArcGIS Field Maps acceptance.

Use precise language:

**historical converter = Earth-compatible / Field Maps nonconformant until repaired.**

One verified difference is the Web Mercator LOD table.

Example LOD 0 scale:

```text
historical converter: 591657527.5917094
Esri native sample:    591657527.591555
```

The old converter calculated these values. The current v0.2.0 TEST branch copies Esri's canonical LOD 0-23 values exactly.

Do not claim the LOD difference is the sole root cause until Field Maps proves it.

---

## Esri-canonical v0.2.0 TEST

Status:

**BUILT / SELF-TESTED — FIELD MAPS TARGET PENDING.**

It copies Esri's native conventions for:

- LOD 0-23 resolutions/scales;
- Web Mercator origin;
- spatial-reference structure;
- `root.json` conventions;
- `iteminfo.json` field types.

Compact Cache V2 bundle writing remains based on the existing published-format implementation.

Bench checks passed for:

- synthetic MBTiles conversion;
- package/ZIP structure;
- bundle headers;
- bundle indexes.

Field Maps is the next and only meaningful vote.

---

## Offline Map Factory 1.0 contract

Normal operator capability remains:

- 4 sources: Google Earth, Google Hybrid, Esri World, Esri World / Google Labels;
- area by HOME EXTENT, Clipboard History diagonal points, or two manual GPS points;
- Z0-Z20;
- output TPKX / MBTiles / Both;
- Advanced existing MBTiles -> TPKX;
- no REST / Static WMTS output.

Status now:

**BUILT / SELF-TESTED — RELEASE ACCEPTANCE BLOCKED ON TPKX CONFORMANCE.**

QGIS -> MBTiles is not the problem. The TPKX packaging stage is reopened under a verified defect.

### Finished-package standard stays unchanged

```text
OFFLINE MAP FACTORY 1.0 - Installation Guide.pdf
OFFLINE MAP FACTORY 1.0 - User Guide.pdf
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
RUN OFFLINE MAP FACTORY.bat
System Files\
```

Do not put developer clutter back in the public root.

---

## Historical TPKX Map Factory v1.0.0

Status remains:

**RELEASE-ACCEPTED / FROZEN — for the actual ArcGIS Earth target tested on 2026-08-15.**

Do not rewrite or re-zip that accepted binary.

The new Field Maps evidence narrows compatibility claims. It does not erase historical acceptance.

---

## Field Maps facts now proven

### LIVE-PROVEN

- `District 7 Local Basemap Test` Designer map created;
- Offline enabled;
- File on the device selected;
- shared Everyone/public;
- physical-card path works:

```text
\Android\data\com.esri.fieldmaps\files\basemaps\
```

- Esri official `Usa.tpkx` works in Field Maps.

### FAILED / NEEDS REPAIR

Project converter-built District 7 TPKX is discovered but rejected as spatial-reference incompatible.

The inspected package still reports expected-looking Web Mercator values, so do not reduce the failure to a superficial WKID typo.

---

## ArcGIS Pro MMPK result

The ArcGIS Pro 3.7 bridge remains PASS:

- small MMPK created;
- district approximately 52 GB MMPK created;
- small specimen analyzer 0/0/0;
- MMPK version 3.0;
- original TPKX preserved under `commondata/new_tpkx/`;
- no HTTP/HTTPS references found in the small `.mmap` / `.mapx`;
- rendered in Windows ArcGIS Earth while Earth showed Not signed in.

Updated interpretation:

**Pro packaging does not repair the source TPKX.**

Do not spend time rebuilding the district MMPK until the corrected TPKX passes Field Maps.

---

## Intended district-card architecture after repair

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

Redundant bytes are acceptable if they improve reliability.

---

## ArcGIS Earth Mobile

Local TPKX remains **LIVE-PROVEN on multiple project packages**.

Do not generalize the Field Maps failure into an Earth Mobile failure.

---

## SD-card / reader rule

The laptop's built-in SD reader produced write-protection behavior across multiple cards/adapters. Another computer wrote successfully.

Treat the reader as suspect.

The SD card is disposable test media. Rename, delete, overwrite, reformat, or rebuild it whenever useful.

---

## Map Fountain

Map Fountain is **LIVE-PROVEN / PARKED**.

Do not revive it merely because the TPKX converter needs repair. Reopen only for a real shared-storage need such as Starlink/basecamp NAS or true multi-client map distribution.

---

## Rasta

Rasta v0.1.3 remains LIVE-PROVEN for giant-raster manufacturing and ArcGIS Earth viewing.

Its TPKX output inherits the historical converter lineage. Do not claim Field Maps compatibility for Rasta TPKX until the canonical converter is proven and integrated.

---

## Do not regress

- Do not call Earth acceptance proof of Field Maps conformance.
- Do not patch random metadata fields because they look different.
- Do not use ArcGIS Pro MMPK wrapping as a supposed sanitizer.
- Do not rebuild 52 GB district products before the tiny canonical test passes.
- Do not erase historical accepted artifacts.
- Do not casually defend the old converter now that a verified defect exists.
- Do not revive REST or protected-folder ADB/MTP dead ends.
- Do not make public Internet mandatory.
- Do not confuse self-test success with real-target acceptance.

---

## Known-good environment

- Windows 10/11 64-bit
- Python 3.14.5
- QGIS 3.44.9
- ArcGIS Pro 3.7
- PNG tiles
- 96 DPI
- antialiasing ON
- metatile 4
- Z0-Z20

---

## Four-project family

1. `Offline-GeoStack` — master manufacturing/integration and TPKX conformance repair.
2. `Rasta-Pyramid-Factory` — giant-raster manufacturing; TPKX branch inherits converter repair.
3. `Map-Fountain` — proven shared-storage/network reference, parked.
4. `Android-Field-Maps-and-ArcGIS-Earth-` — real Field Maps/Android deployment evidence.

---

## Governing principle

> **Esri's native TPKX is the reference. Field Maps is the judge. The real target decides acceptance.**
