# Offline GeoStack Roadmap

## Immediate priority — finish native ArcGIS Pro Field Maps path

The custom converter is no longer the production gate.

The current Field Maps production path is:

```text
QGIS
-> labeled GeoTIFF
-> ArcGIS Pro Create Map Tile Package
-> native TPKX
-> physical removable storage
-> Field Maps
```

Why the turn was made:

```text
historical project TPKX -> Field Maps REJECTED
canonical v0.3.1 TPKX  -> Field Maps REJECTED
Esri official Usa.tpkx  -> Field Maps ACCEPTED
```

v0.3.1 failed despite passing the existing local structural comparison. The production response is to let ArcGIS Pro create the TPKX natively rather than continuing to make Field Maps the debugger for hand-built packages.

---

## Gate 1 — finish the District 7 Z17 GeoTIFF

Current live production recipe:

```text
source stack: Esri Satellite + Google Labels
render order: Google Labels on top
CRS: EPSG:3857
target detail: Z17
map units per pixel: 1.19432856685505
QGIS raster tile size: 1024
output: one GeoTIFF
```

The District 7 build was started on the live QGIS machine on 2026-08-21.

Record only after completion:

- finished file size;
- elapsed time;
- successful completion state;
- visual label/imagery check.

Do not infer completion while the large run is still active.

---

## Gate 2 — ArcGIS Pro native District 7 TPKX

When the District 7 GeoTIFF finishes:

1. create a clean ArcGIS Pro Map;
2. add the GeoTIFF;
3. calculate raster statistics if Pro asks;
4. remove default World Topographic Map / Hillshade layers;
5. run **Create Map Tile Package**;
6. use the ArcGIS Online | Bing Maps | Google Maps tiling scheme;
7. Tiling Format = PNG 24 bit;
8. Minimum Level Of Detail = 0;
9. Maximum Level Of Detail = 17;
10. Extent = District 7 GeoTIFF layer extent;
11. output a native `.tpkx`.

Then inspect the finished package and record exact byte count and package metadata.

---

## Gate 3 — real Field Maps vote

Copy the native ArcGIS Pro-created District 7 TPKX to the proven physical-card path:

```text
\Android\data\com.esri.fieldmaps\files\basemaps\
```

Set Field Maps Designer **File on the device** to the exact filename and open the map.

### PASS

- mark native ArcGIS Pro TPKX production LIVE-PROVEN for Field Maps;
- freeze the working QGIS + Pro recipe;
- create/rebuild any required MMPK around the native TPKX only if the deployment workflow still benefits from it;
- run cold/no-public-Internet district acceptance;
- prepare finished card documentation.

### FAIL

- capture the exact Field Maps failure;
- do not reopen the custom converter as the first reaction;
- inspect the native Pro package, Field Maps map item, storage path, and Designer reference as one controlled system.

---

## GeoTIFF Factory branch

`GEOTIFF FACTORY 0.1.2 TEST` is built and bench-checked.

Design contract:

- four controlled map sources;
- saved HOME EXTENT;
- Windows Clipboard History diagonal points;
- two manually entered diagonal GPS points;
- Z16-Z20 source-detail choice;
- EPSG:3857;
- QGIS Convert map to raster engine;
- correct hybrid label/imagery render order;
- one `.tif` output;
- no MBTiles;
- no TPKX converter;
- no recovery tools.

### Next GeoTIFF Factory gate

Run a small Windows/QGIS live test after the current District 7 manual build finishes.

Verify:

1. BAT starts cleanly;
2. QGIS 3.44.9 is found;
3. self-contained template loads;
4. two-point extent converts correctly;
5. selected source/layers are correct;
6. chosen Z16-Z20 value maps to the correct meters-per-pixel value;
7. finished GeoTIFF is created;
8. hybrid labels are visible;
9. only the requested `.tif` is left as finished output.

Only then promote beyond TEST.

---

## GeoTIFF source-detail table

| Target detail | Map units per pixel |
| ---: | ---: |
| Z16 | `2.38865713397468` |
| Z17 | `1.19432856685505` |
| Z18 | `0.597164283559817` |
| Z19 | `0.298582141647617` |
| Z20 | `0.149291070823808325` |

ArcGIS Pro Maximum Level Of Detail must match the source GeoTIFF target detail.

---

## Proven small native-Pro experiment

The small live proof already completed:

```text
QGIS labeled GeoTIFF
37,767,543 bytes
4096 x 3072 RGB
EPSG:3857
Z18 source detail

-> ArcGIS Pro Create Map Tile Package

tiff test 66.tpkx
38,306,245 bytes
Z0-Z18
PNG24
19 bundles
```

The TPKX identifies its creator as `CreateMapTilePackage ArcGIS Pro`.

Field Maps runtime acceptance of this native-Pro branch remains pending until a real device vote is recorded.

---

## Custom converter — research branch only

### v0.3.1

- bench structural comparison: PASS;
- source tile preservation: PASS;
- Field Maps: **FAIL — spatial-reference incompatible**.

### v0.3.2

A later bench experiment normalized PNG tile `pHYs` metadata to the value observed in `Usa.tpkx`.

Status: **research only; Field Maps vote not required for the current production path.**

The real ArcGIS Pro-created TPKX is now the better research specimen for any future attempt to eliminate the Pro dependency.

Keep issue #3 open as converter research/backlog, not as a deployment blocker.

---

## Historical product boundaries

### TPKX Map Factory v1.0.0

**RELEASE-ACCEPTED / FROZEN for ArcGIS Earth.** Do not rewrite the artifact or history.

### Offline Map Factory 1.0

QGIS -> MBTiles remains live-proven. Its custom TPKX stage is not the current Field Maps production path.

### Rasta Pyramid Factory

Rasta v0.1.3 remains live-proven for giant-raster manufacturing and ArcGIS Earth. Prefer ArcGIS Pro native packaging for any new Field Maps deployment branch until a custom converter earns strict Field Maps acceptance.

### Map Fountain

LIVE-PROVEN / PARKED. Do not reintroduce network infrastructure merely because the manufacturing path changed.

---

## Governing rules

> **Use the native vendor packaging path when it solves the real target cleanly.**

> **Do the manufacturing work on the bench; use Field Maps for acceptance, not iterative debugging.**

> **The real target decides acceptance.**
