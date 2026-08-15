# TPKX Map Factory v1.0.0 — Quick Start

## Install once

1. Install ArcGIS Earth.
2. Install Python 3.14.5.
3. Install QGIS 3.44.9.
4. Create:

```text
C:\Google Earth Project\QGIS\
```

5. Place the two required QGIS `.qgz` project files in that folder.
6. Extract `TPKX_MAP_FACTORY_v1_0_0.zip`.

## Make a map

1. Open the Factory.
2. Choose one of the four map sources.
3. Choose the map area using either:
   - a prepared HOME EXTENT,
   - two diagonal coordinate pairs from Windows Clipboard History, or
   - two manually entered decimal-degree GPS coordinate pairs.
4. Choose minimum and maximum zoom.
5. Click **BUILD TPKX MAP**.
6. Choose the output filename when prompted.
7. Wait for COMPLETE.
8. Open the finished `.tpkx` directly in ArcGIS Earth.

The user-selected destination should receive one finished `.tpkx` file. Temporary manufacturing data is not intended to remain there.

## Advanced GIS users

If you already have a suitable raster MBTiles file:

1. Click **ADVANCED: MBTILES → TPKX**.
2. Select the `.mbtiles` file.
3. Choose the output `.tpkx` filename.
4. Wait for COMPLETE.
5. Open the finished package in ArcGIS Earth.

This allows you to build any desired raster layer stack in QGIS and use the Factory only as the TPKX packaging bridge.

## Operational rule

The finished TPKX is intended to support offline operation.

> **There can be no operational dependence on Internet connectivity. Period.**

Build/refresh maps before they are needed. At showtime, the map is already in the trunk.