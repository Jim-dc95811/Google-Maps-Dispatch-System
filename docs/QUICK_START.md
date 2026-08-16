# Offline GeoStack — TPKX Map Factory v1.0.0 Quick Start

## Install once

1. Install ArcGIS Earth.
2. Install Python 3.14.5.
3. Install QGIS 3.44.9.
4. Create:

```text
C:\Google Earth Project\QGIS\
```

5. Download the two files from [`required_qgis_projects/`](../required_qgis_projects/) and place them in that folder with their exact filenames.
6. Obtain the release-accepted `TPKX_MAP_FACTORY_v1_0_0.zip` and extract it completely before use.

> **GitHub binary note:** the exact accepted ZIP is preserved in the canonical project archive. The connector used during this repository rebuild could not transmit that ZIP intact, so the bad copy was removed. See [`releases/README.md`](../releases/README.md). The exact ZIP should be attached directly to GitHub before public binary distribution.

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

This is the direct interoperability path for GIS professionals: build the desired raster layer stack in QGIS, export suitable raster MBTiles, then let the Factory package those existing tiles into TPKX.

## What the Factory is doing underneath

```text
Normal path:
QGIS project → raster MBTiles → Compact Cache V2 → TPKX → ArcGIS Earth

Advanced path:
existing raster MBTiles → Compact Cache V2 → TPKX → ArcGIS Earth
```

The converter does not rerender the cartography. QGIS owns the pixels; the converter owns the package mechanics.

## Operational rule

> **There can be no operational dependence on Internet connectivity. Period.**

Build or refresh maps before they are needed. At showtime, the map is already in the trunk.
