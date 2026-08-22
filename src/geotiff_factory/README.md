# GeoTIFF Factory

## Current test artifact

```text
GEOTIFF_FACTORY_0_1_3_TEST.zip
22,183 bytes
SHA-256 9f98d67f9c38fee6ba71f538ef887aa10af901f7e1d1c5e68685590b492fd84a
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

## 0.1.3 GUI correction

The first 0.1.2 live-open screenshot showed that the tall vertical area-entry layout pushed the Finished GeoTIFF controls below the visible Windows work area.

0.1.3 corrects that by restoring the proven **Offline Map Factory Box 2** area layout rather than inventing a new extent panel.

The area box is now the familiar two-column arrangement:

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

This directly follows the proven Offline Map Factory operator workflow documented in its user guide and live screenshots.

The window/header/cards were also compacted so boxes 1 through 4 and BUILD GEOTIFF remain visible together on a common Windows display.

### Clipboard History behavior

The large Clipboard History button now uses the operator's existing Windows `Win+V` history instead of adding fragile hidden WinRT/PowerShell history parsing. The Factory prompts for PIN 1 and PIN 2 in sequence, detects the selected `Latitude,Longitude` text, fills both pins, and computes HOME EXTENT.

Manual pins remain complete `Latitude,Longitude` strings, matching the established Offline Map Factory interface.

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
- two-point GPS -> EPSG:3857 extent conversion: PASS
- HOME EXTENT parsing: PASS
- Z16-Z20 resolution table: PASS
- 1024-aligned raster-size estimator: PASS
- QGZ template archive: PASS
- hybrid label-over-imagery render order: PASS
- `native:rasterize` engine path retained from 0.1.2: PASS
- 1366x768 virtual-screen GUI preview: all four numbered boxes and BUILD GEOTIFF visible
- clean package layout: PASS

## Live acceptance still required

The container bench cannot execute the installed Windows QGIS runtime. The first real acceptance test should therefore be a small known extent, preferably Esri World / Google Labels at Z17, with QGIS Desktop closed.

Pass condition:

1. Factory launches from the BAT file.
2. Entire interface is visible without clipped lower controls.
3. Box 2 behaves like the established Offline Map Factory area workflow.
4. QGIS 3.44.9 is found.
5. GeoTIFF builds successfully.
6. GeoTIFF is EPSG:3857.
7. Satellite/imagery and labels render in the correct order.
8. ArcGIS Pro opens the GeoTIFF normally and can create the native TPKX.

Do not promote this test build as live-proven until that Windows/QGIS test passes.
