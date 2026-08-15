# Public Release Checklist

This checklist records the minimum release gates for the TPKX Map Factory public baseline.

## v1.0.0 gates

- [x] GUI launches on Windows using the packaged BAT launcher.
- [x] Colored visual controls remain visible at the target screen size.
- [x] Manual decimal-degree GPS diagonal points populate a valid HOME EXTENT.
- [x] Normal Factory path completes a map build.
- [x] QGIS produces temporary raster MBTiles.
- [x] Proven converter builds TPKX.
- [x] Destination receives the finished TPKX product.
- [x] Advanced existing-MBTiles -> TPKX path completes.
- [x] Large advanced conversion accepted by ArcGIS Earth.
- [x] Large Esri World / Google Labels Factory run accepted by ArcGIS Earth.
- [x] v1.0.0 small release smoke package accepted by ArcGIS Earth.
- [x] Version 1.0.0 feature freeze declared.

## Acceptance rule

ArcGIS Earth is the final operational acceptance authority for finished TPKX packages.

## Change rule

New features belong in v1.1 or later unless a verified defect requires a maintenance release.