# Offline GeoStack — Notes for GIS Professionals

The shortest technical description of the core manufacturing system is:

> **QGIS performs the cartography. Raster MBTiles holds the finished tile pyramid. A custom Python converter repackages those unchanged tile images into Esri Compact Cache V2 / TPKX. The target application consumes the resulting local package.**

The converter is intentionally not a GIS renderer. It is an interoperability bridge.

## Why that distinction matters

If the desired cartography can be produced in QGIS and exported as suitable raster MBTiles, the converter does not need to understand the underlying layers, symbols, labels, imagery sources, or vector features. It receives already-rendered pixels.

This keeps concerns separated:

- **QGIS** — rendering, source handling, labels, symbology, composition, reprojection.
- **MBTiles** — raster tile-pyramid container; manufacturing handoff and, when deliberately preserved, useful finished/interchange product.
- **Converter** — addressing translation, Compact Cache V2 binary packaging, TPKX metadata.
- **TPKX** — compact native deployment package used by ArcGIS Earth and documented by Esri as an on-device basemap type for ArcGIS Field Maps.
- **ArcGIS Earth / Field Maps** — downstream runtimes with different operational roles.
- **GNSS / PRAVE / F22 / QR / KML** — live or interoperable field-input layers around the offline basemap/runtime system.

## Advanced-user implication

The public Factory includes an **ADVANCED: MBTILES → TPKX** path. A GIS professional can therefore ignore the Factory's canned source menu, construct a custom QGIS project, render raster MBTiles, and use only the converter stage.

That is the intended advanced escape hatch rather than adding professional-GIS complexity to the beginner-facing Factory GUI.

## MBTiles preservation rule

If MBTiles will be useful downstream, preserve the direct QGIS-built MBTiles at manufacture time.

Do not use reverse TPKX → MBTiles recovery as a production shortcut. A controlled fixture recovered exact tile bytes, but a recovered production MBTiles later showed blurred/missing regions on ArcGIS Earth Mobile.

Target-viewer acceptance outranks internal structural cleverness.

## Precision

The critical TMS-to-ArcGIS Y conversion and bundle addressing are integer operations. The converter does not deliberately round tile coordinates or resample imagery. Human-readable console/status formatting is separate from the values used to build the package.

## Validation

Structural verification is performed during packaging, but **the intended real target is the final operational acceptance authority**.

The large advanced path has processed 271,497 tiles into 47 Compact Cache V2 bundles and rendered successfully in ArcGIS Earth. The large normal Factory path has processed 271,242 tiles and rendered successfully. The exact v1.0 release smoke test also passed.

A production-scale TPKX at **25,561,426 KB** in Windows File Explorer was also opened directly from router-attached SMB storage over Wi-Fi in ArcGIS Earth.

## Current mobile deployment direction

The normal personal-phone direction is now:

```text
TPKX
→ microSD
→ Android
→ ArcGIS Field Maps / ArcGIS Earth
```

Esri documents TPKX sideloading to Android/device microSD for Field Maps. Offline GeoStack's own Field Maps target test is still pending, so keep vendor support and project acceptance as separate evidence states.

## Map Fountain boundary

Map Fountain successfully proved both Windows native TPKX-over-SMB and Android Static REST WMTS router paths. It is now parked from the primary personal-phone workflow and retained as engineering evidence / possible future Starlink-basecamp shared storage.

## Operational doctrine

Offline GeoStack treats locally manufactured map packages as operational inventory rather than an emergency fallback cache.

> **There can be no operational dependence on Internet connectivity. Period.**

For personal mobile use, the current simplification is even more direct: put the map bytes on the removable storage before the user needs them.
