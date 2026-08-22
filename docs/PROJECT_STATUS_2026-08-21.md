# Offline GeoStack — Project Status — 2026-08-21

## Executive state

The Field Maps production branch has pivoted away from custom TPKX construction.

Strict target evidence now reads:

```text
historical project TPKX -> Field Maps REJECTED
canonical v0.3.1 TPKX  -> Field Maps REJECTED
Esri official Usa.tpkx  -> Field Maps ACCEPTED
```

The production response is:

```text
QGIS
-> finished labeled GeoTIFF
-> ArcGIS Pro Create Map Tile Package
-> native TPKX
-> physical removable storage
-> Field Maps
```

The custom converter remains a research branch, not the deployment gate.

---

## Mission lock

> A Field Maps user must be able to open the app with zero public Internet and use a district-wide Esri Hybrid map through Z17. The same local map should stop the heavy basemap from consuming cellular data when service exists.

---

## QGIS GeoTIFF proof

The small live test successfully produced a georeferenced labeled master raster.

```text
GeoTIFF size: 37,767,543 bytes
Dimensions: 4096 x 3072
Bands: RGB
CRS: EPSG:3857
Source detail: Z18
Resolution: 0.597164283559817 meters/pixel
```

Critical layer-order rule:

```text
Google Labels   <- top
ESRI Satellite  <- bottom
```

Reversing the order hid the labels under the imagery.

---

## ArcGIS Pro native TPKX proof

ArcGIS Pro successfully converted the small GeoTIFF using **Create Map Tile Package**.

```text
Output: tiff test 66.tpkx
Size: 38,306,245 bytes
Zooms: Z0-Z18
Tiling format: PNG24
Bundles: 19
Creator: CreateMapTilePackage ArcGIS Pro
```

Forensic package observations:

- WKID 102100 / latestWKID 3857;
- Compact Cache V2 packet size 128;
- Esri bundle-header pattern;
- `root.json.layers` contains a real Raster Layer record describing the source TIFF;
- no explicit ZIP directory entries;
- root spatial-reference objects are minimal WKID/latestWKID objects rather than the extended objects used by the custom converter.

These observations now replace earlier assumptions that every working TPKX must copy the exact ZIP-directory and root-SR shape of `Usa.tpkx`.

Field Maps runtime acceptance of the ArcGIS Pro-created package is still pending.

---

## GeoTIFF Factory 0.1.2 TEST

A separate GeoTIFF Factory branch is built and bench-checked.

Operator contract:

- four map-source choices;
- standard saved HOME EXTENT;
- Windows Clipboard History diagonal-point input;
- two manual diagonal GPS points;
- Z16-Z20 target detail;
- EPSG:3857;
- QGIS Convert map to raster engine;
- correct layer composition;
- one finished `.tif` output;
- no MBTiles;
- no TPKX converter;
- no recovery tool.

Package surface:

```text
RUN GEOTIFF FACTORY.bat
System Files\
```

Runtime template:

```text
System Files\GEO_TIFF_FACTORY_TEMPLATE.qgz
```

The branch is self-contained and does not require the historical QGZ files at runtime.

Status: **BUILT / BENCH-CHECKED — WINDOWS/QGIS LIVE TEST PENDING.**

---

## GeoTIFF target-detail table

| Target | Map units per pixel |
| ---: | ---: |
| Z16 | `2.38865713397468` |
| Z17 | `1.19432856685505` |
| Z18 | `0.597164283559817` |
| Z19 | `0.298582141647617` |
| Z20 | `0.149291070823808325` |

ArcGIS Pro Maximum Level Of Detail should match the QGIS source detail.

---

## District 7 current run

A District 7 Esri Satellite + Google Labels GeoTIFF build was started on the live QGIS machine.

```text
Target: Z17
Map units per pixel: 1.19432856685505
```

Status: **LIVE BUILD STARTED — COMPLETION PENDING.**

Do not record final size or elapsed time until the run finishes.

Next chain after completion:

```text
District 7 Z17 GeoTIFF
-> ArcGIS Pro native TPKX
-> physical card
-> Field Maps
```

---

## Custom converter status

### Historical converter

ArcGIS Earth: proven.
Field Maps: failed.

### v0.3.1

Bench structure/tile preservation: passed.
Field Maps: **failed as spatial-reference incompatible**.

### v0.3.2

A bench-only follow-up normalized PNG tile `pHYs` metadata to the value observed in `Usa.tpkx`.

Status: research only. It is no longer the production gate.

The newly available ArcGIS Pro-created TPKX is now the preferred reference specimen for any future converter research.

---

## Current status matrix

| Capability | Status |
| --- | --- |
| QGIS labeled GeoTIFF small test | ✅ LIVE-PROVEN |
| ArcGIS Pro GeoTIFF -> native TPKX | ✅ LIVE BUILD PASS / FIELD MAPS PENDING |
| GeoTIFF Factory 0.1.2 TEST | 🟡 BUILT / BENCH-CHECKED |
| District 7 Z17 GeoTIFF | 🟡 LIVE BUILD STARTED |
| Field Maps Designer + physical basemaps path | ✅ LIVE-PROVEN |
| Esri official Usa.tpkx in Field Maps | ✅ LIVE-PROVEN |
| Historical custom TPKX in Field Maps | ❌ FAILED |
| v0.3.1 custom TPKX in Field Maps | ❌ FAILED |
| v0.3.2 converter | 🟡 RESEARCH ONLY |
| ArcGIS Earth Windows project TPKX | ✅ LIVE-PROVEN |
| ArcGIS Earth Mobile local project TPKX | ✅ LIVE-PROVEN |
| Historical TPKX Map Factory v1.0.0 | ✅ RELEASE-ACCEPTED / FROZEN FOR EARTH |
| Map Fountain | ✅ LIVE-PROVEN / PARKED |

---

## Immediate next actions

1. Let the District 7 Z17 GeoTIFF finish.
2. Record exact completion evidence.
3. Live-test GeoTIFF Factory 0.1.2 on a small area.
4. Package the finished District 7 GeoTIFF in ArcGIS Pro as a native Z0-Z17 TPKX.
5. Put that native TPKX on the physical card.
6. Set Designer to the exact filename.
7. Let Field Maps vote.

---

## Do not regress

- Do not make the custom converter the production blocker again without a reason.
- Do not call a Pro-created TPKX Field Maps-proven until Field Maps opens it.
- Do not infer completion of the large District 7 GeoTIFF while QGIS is still running.
- Do not rewrite historical accepted releases.
- Do not add MBTiles/converter clutter to the GeoTIFF Factory.
- Do not make public Internet a showtime requirement.

> **QGIS makes the finished raster. ArcGIS Pro makes the native TPKX. Field Maps makes the acceptance decision.**
