# Offline GeoStack — Notes for GIS Professionals

The shortest technical description of the current system is:

> **QGIS performs the cartography. Raster MBTiles holds the finished tile pyramid. A custom Python converter repackages those unchanged tile images into Esri Compact Cache V2 / TPKX. ArcGIS Earth consumes the resulting package natively.**

The converter is intentionally not a GIS renderer. It is an interoperability bridge.

## Why that distinction matters

If the desired cartography can be produced in QGIS and exported as suitable raster MBTiles, the converter does not need to understand the underlying layers, symbols, labels, imagery sources, or vector features. It receives already-rendered pixels.

This keeps concerns separated:

- **QGIS** — rendering, source handling, labels, symbology, composition, reprojection.
- **MBTiles** — temporary raster tile-pyramid container.
- **Converter** — addressing translation, Compact Cache V2 binary packaging, TPKX metadata.
- **ArcGIS Earth** — native display, 3D navigation, and operational runtime.
- **GNSS / PRAVE / F22 / QR / KML** — live or interoperable field-input layers around the offline basemap.

## Advanced-user implication

The public Factory includes an **ADVANCED: MBTILES → TPKX** path. A GIS professional can therefore ignore the Factory's canned source menu, construct a custom QGIS project, render raster MBTiles, and use only the converter stage.

That is the intended advanced escape hatch rather than adding professional-GIS complexity to the beginner-facing Factory GUI.

## Precision

The critical TMS-to-ArcGIS Y conversion and bundle addressing are integer operations. The converter does not deliberately round tile coordinates or resample imagery. Human-readable console/status formatting is separate from the values used to build the package.

## Validation

Structural verification is performed during packaging, but **ArcGIS Earth is the final operational acceptance authority** in this project.

The large advanced path has already processed 271,497 tiles into 47 Compact Cache V2 bundles and rendered successfully in AE. The large normal Factory path has processed 271,242 tiles and rendered successfully in AE. The exact v1.0 release smoke test also passed.

## Operational doctrine

Offline GeoStack treats locally manufactured map packages as operational inventory rather than an emergency fallback cache.

> **There can be no operational dependence on Internet connectivity. Period.**
