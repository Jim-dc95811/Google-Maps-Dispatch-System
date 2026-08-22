# GeoTIFF Factory

## Current test artifact

```text
GEOTIFF_FACTORY_0_1_4_TEST.zip
24,612 bytes
SHA-256 a2aac728c732b658dc1a9ea0843fcaa7fe3fdeca2d235cd7ac0d3021dcc11778
```

Status: **BUILT / BENCH SELF-TESTED — Windows QGIS live test pending.**

The exact test ZIP is preserved in the project Library.

## Purpose

This is a separate product from Offline Map Factory. It performs one job only:

```text
map source + two-point extent + target detail Z16-Z20
-> hidden QGIS 3.44.9 Convert map to raster
-> finished EPSG:3857 GeoTIFF
-> ArcGIS Pro Create Map Tile Package
-> native TPKX
```

There is no MBTiles stage and no TPKX converter in this Factory.

## Operator surface

The package root contains only:

```text
RUN GEOTIFF FACTORY.bat
System Files/
```

The GUI provides the four established source choices:

- Google Earth
- Google Hybrid
- Esri World
- Esri World / Google Labels

## 0.1.4 Box 2 restoration

The GeoTIFF Factory area-entry controls are deliberately copied from **Offline Map Factory 1.0 Box 2** rather than redesigned.

The area box uses the established two-column arrangement:

```text
LEFT
HOME EXTENT — order: xmin, xmax, ymin, ymax
Approx. Area
saved extent field
example
LOAD TWO DIAGONAL POINTS FROM WINDOWS CLIPBOARD HISTORY

RIGHT
ENTER 2 DIAGONAL SETS OF GPS COORDINATES
PIN 1 — Latitude, Longitude
PIN 2 — Latitude, Longitude
example
USE THESE TWO GPS POINTS

BOTTOM
3 choices: saved extent / Clipboard History / manual GPS coordinates
```

The window footprint is also returned to the proven Offline Map Factory dimensions:

```text
1100 x 700
minimum 1000 x 640
```

This keeps the full GeoTIFF operator surface visible without changing the established extent workflow.

### Clipboard History behavior — exact Offline Map Factory behavior

0.1.3 incorrectly introduced a new interactive Clipboard History selection sequence. That behavior is removed.

0.1.4 copies the actual Offline Map Factory 1.0 implementation:

- the exact `GET_CLIPBOARD_HISTORY.ps1` helper is included byte-for-byte;
- pressing **LOAD TWO DIAGONAL POINTS FROM WINDOWS CLIPBOARD HISTORY** reads Windows Clipboard History once;
- the program scans history from newest to older entries;
- it finds the two most recent distinct valid `Latitude, Longitude` coordinate entries;
- it converts those two diagonal points directly into HOME EXTENT;
- no separate PIN 1 / PIN 2 prompts are introduced;
- no Win+V selection sequence is introduced.

The copied helper SHA-256 is:

```text
fb88b644f64989511d65b1832e4b928125b8a340b8e5270ad04e6d271154dca9
```

Manual PIN 1 / PIN 2 parsing and error behavior are also aligned with Offline Map Factory 1.0: decimal-degree `Latitude, Longitude`, either diagonal corner first.

## Target detail

Target detail is selectable from Z16 through Z20 using the proven Web Mercator map-units-per-pixel values:

| Zoom | Map units per pixel |
| ---: | ---: |
| 16 | 2.38865713397468 |
| 17 | 1.19432856685505 |
| 18 | 0.597164283559817 |
| 19 | 0.298582141647617 |
| 20 | 0.149291070823808325 |

## QGIS construction

The Factory uses QGIS 3.44.9 headlessly through `qgis_process` and the `native:rasterize` / **Convert map to raster** algorithm.

Locked production settings:

- EPSG:3857
- tile size 1024
- extent buffer 0
- transparent background OFF
- target map-units-per-pixel from the table above
- one finished `.tif` output

For hybrid sources, render order is explicitly:

```text
Google Labels      TOP
imagery            BOTTOM
```

This order is based on the live QGIS/ArcGIS Pro test where the reverse order hid the labels in the finished GeoTIFF.

## Hidden template

The package includes a private QGIS template derived from the established `ESRI and Google Labels.qgz` project. A disposable copy is made for each run. The reference template is not modified during production.

## Bench checks completed

- Python source compilation: PASS
- exact Offline Map Factory Clipboard History helper copied byte-for-byte: PASS
- Clipboard History parsing path copied from Offline Map Factory: PASS
- two-point GPS -> EPSG:3857 extent conversion: PASS
- manual GPS point behavior aligned with Offline Map Factory: PASS
- HOME EXTENT parsing: PASS
- Z16-Z20 resolution table: PASS
- 1024-aligned raster-size estimator: PASS
- QGZ template archive: PASS
- hybrid label-over-imagery render order: PASS
- `native:rasterize` engine path retained: PASS
- clean package root: one BAT + one System Files folder

## Live acceptance still required

The container bench cannot execute the installed Windows QGIS runtime or Windows Clipboard History API. The next real acceptance should use the same operator routine already proven in Offline Map Factory:

1. copy one diagonal coordinate;
2. copy the opposite diagonal coordinate;
3. press **LOAD TWO DIAGONAL POINTS FROM WINDOWS CLIPBOARD HISTORY**;
4. confirm HOME EXTENT populates automatically;
5. build a small Esri World / Google Labels Z17 GeoTIFF;
6. verify QGIS 3.44.9 builds it successfully;
7. verify imagery and labels;
8. open the GeoTIFF in ArcGIS Pro and create the native TPKX.

Do not promote this test build as live-proven until that Windows/QGIS test passes.
