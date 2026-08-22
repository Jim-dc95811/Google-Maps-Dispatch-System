# TPKX / Field Maps Conformance — 2026-08-20 to 2026-08-21

## Decisive control

The original strict control remains:

```text
same physical microSD
same Field Maps app
same Designer map
same basemaps folder

historical project TPKX -> REJECTED
Esri official Usa.tpkx  -> ACCEPTED
```

That proved the Field Maps path and isolated the original defect to project-built TPKX construction.

## Repair lineage result

### v0.2.0

Corrected canonical Web Mercator LOD values and other metadata differences. Further package differences were found before Field Maps testing.

### v0.3.0 / v0.3.1

The converter was tightened to reproduce the then-observed `Usa.tpkx` structural conventions and to self-verify its output.

Bench evidence for v0.3.1 included:

- 174 / 174 source PNG tiles recovered byte-for-byte;
- valid Compact Cache V2 addressing/indexes;
- Esri bundle-header pattern;
- canonical LOD table;
- matching Web Mercator origin;
- matching root/item schema used in the comparison;
- thumbnail DPI normalization;
- no remaining defect found by the local comparison.

### Real target vote — v0.3.1

Field Maps still rejected the v0.3.1 package as spatial-reference incompatible.

Therefore:

```text
v0.3.1 BENCH STRUCTURE PASS
v0.3.1 FIELD MAPS FAIL
```

This is the key engineering correction: local comparison against one official TPKX specimen did not establish complete native equivalence.

## Web-map spatial reference check

The Field Maps Designer web-map JSON reported:

```text
wkid = 102100
latestWkid = 3857
falseX = -20037700
falseY = -30241100
xyTolerance = 0.001
xyUnits = 10000
```

Those values were already compatible with the v0.3.1 root metadata. The obvious visible WKID block was therefore not the missing piece.

The same JSON also demonstrated that Designer stores the exact device basemap filename in:

```text
applicationProperties.offline.offlinebasemap.referenceBasemapName
```

That filename must always match the actual card file being tested.

## v0.3.2 research follow-up

A remaining systematic PNG metadata difference was found:

```text
Esri Usa.tpkx tiles: pHYs 3780 x 3780 pixels/meter
QGIS small MBTiles tiles: pHYs 3779 x 3779 pixels/meter
AE SYSTEM CHECK synthetic tiles: no pHYs chunk
```

`ESRI_CANONICAL_TPKX_TEST_v0_3_2` was built to normalize PNG tile `pHYs` metadata without re-encoding pixel data.

Bench verification passed.

Status: **RESEARCH ONLY — NOT THE CURRENT PRODUCTION GATE.**

The project pivoted before spending more Field Maps cycles on hand-built TPKX experiments.

---

## Production bypass — native ArcGIS Pro TPKX

The project changed the manufacturing path to:

```text
QGIS
-> GeoTIFF
-> ArcGIS Pro Create Map Tile Package
-> native TPKX
-> Field Maps
```

A small live proof successfully created both the GeoTIFF and the native Pro TPKX.

### QGIS source

```text
37,767,543-byte GeoTIFF
4096 x 3072 RGB
EPSG:3857
Z18 source detail
```

### ArcGIS Pro output

```text
tiff test 66.tpkx
38,306,245 bytes
Z0-Z18
PNG24
19 bundles
creator = CreateMapTilePackage ArcGIS Pro
```

## New forensic lessons from a real ArcGIS Pro-generated TPKX

The native Pro package is a better production reference than trying to infer universal rules from `Usa.tpkx` alone.

Observed native-Pro facts:

- `spatialReference` uses the simple `{wkid:102100, latestWkid:3857}` form;
- `tileInfo.spatialReference` uses the same simple form;
- `root.json.layers` contains a real `Raster Layer` entry for the source GeoTIFF with legend information;
- ZIP entries are stored with Esri creator/extract metadata;
- the archive contains **no explicit ZIP directory records**;
- Compact Cache V2 bundle headers match the Esri pattern already discovered;
- `iteminfo.json` identifies `creator: CreateMapTilePackage ArcGIS Pro`.

These findings invalidate two earlier assumptions as universal requirements:

1. explicit `tile/` / `tile/Lxx/` ZIP directory entries are not required for a native ArcGIS Pro TPKX;
2. the extended spatial-reference object copied from `Usa.tpkx` is not required in ArcGIS Pro's own native raster TPKX.

A third difference is now a meaningful future converter research lead: the native Pro package contains a populated Raster Layer description rather than `layers: []`.

This is **not yet claimed as the sole reason v0.3.1 failed**. It is simply a concrete native-package difference worth preserving for future research.

---

## Current production decision

Do not continue using Field Maps as the iterative debugger for the custom converter.

Use:

```text
QGIS / GeoTIFF Factory
-> finished GeoTIFF
-> ArcGIS Pro native TPKX
-> Field Maps acceptance
```

The converter issue remains open as research/backlog for a possible future Pro-free workflow.

## Current acceptance matrix

| Object / path | Result |
| --- | --- |
| Historical custom TPKX -> Field Maps | ❌ FAIL |
| Esri official Usa.tpkx -> Field Maps | ✅ PASS |
| Custom v0.3.1 -> Field Maps | ❌ FAIL |
| Custom v0.3.2 | 🟡 BENCH RESEARCH ONLY |
| QGIS GeoTIFF small build | ✅ PASS |
| ArcGIS Pro GeoTIFF -> native TPKX build | ✅ PASS |
| ArcGIS Pro native TPKX -> Field Maps | 🟡 PENDING |

## Governing rule

> **Use the native vendor packaging path for production. Preserve custom-converter work as research until it earns the same real-target acceptance.**
