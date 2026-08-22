# GeoTIFF Factory

## Current test artifact

```text
GEOTIFF_FACTORY_0_1_2_TEST.zip
SHA-256 b25c86b7ceb3892512e99f4f5e67892c4765747411c06c9175be66b3a8a5fad4
```

Status: **BUILT / BENCH SELF-TESTED — Windows QGIS live test pending.**

The exact tested ZIP is preserved in the project Library.

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

Area entry supports the established HOME EXTENT and two diagonal GPS-point workflow. The two points may be entered in either diagonal order; the Factory normalizes them to an EPSG:3857 QGIS extent.

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
- all four temporary source-project constructions: PASS
- hybrid label-over-imagery render order: PASS
- Google source substitution into disposable QGZ: PASS
- `native:rasterize` JSON parameter contract: PASS
- clean package layout: PASS

## Live acceptance still required

The container bench cannot execute the installed Windows QGIS runtime. The first real acceptance test should therefore be a small known extent, preferably Esri World / Google Labels at Z17, with QGIS Desktop closed.

Pass condition:

1. Factory launches from the BAT file.
2. QGIS 3.44.9 is found.
3. GeoTIFF builds successfully.
4. GeoTIFF is EPSG:3857.
5. Satellite/imagery and labels render in the correct order.
6. ArcGIS Pro opens the GeoTIFF normally and can create the native TPKX.

Do not promote this test build as live-proven until that Windows/QGIS test passes.
