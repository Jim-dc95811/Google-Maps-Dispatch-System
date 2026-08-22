# Source / Engineering Branches

This folder records current experimental and production-support branches without rewriting frozen historical releases.

## GeoTIFF Factory

[`geotiff_factory/`](geotiff_factory/)

Current Field Maps manufacturing direction:

```text
QGIS / GeoTIFF Factory
-> finished EPSG:3857 GeoTIFF
-> ArcGIS Pro Create Map Tile Package
-> native TPKX
-> Field Maps
```

Current artifact: `GEOTIFF_FACTORY_0_1_2_TEST.zip`.

Status: **BUILT / BENCH-CHECKED — WINDOWS/QGIS LIVE TEST PENDING.**

## Esri canonical custom TPKX converter research

[`esri_canonical_tpkx_test/`](esri_canonical_tpkx_test/)

The custom converter is preserved as research/backlog after Field Maps rejected v0.3.1 despite its local structural and tile-preservation checks passing.

Production no longer waits on this branch. A real ArcGIS Pro-generated raster TPKX is now the preferred future research specimen if the project later attempts to remove the ArcGIS Pro dependency.

## Frozen historical source boundary

Historical accepted Factory artifacts remain frozen in their original release records. Do not silently rebuild or relabel them because current Field Maps production uses a different packaging path.
