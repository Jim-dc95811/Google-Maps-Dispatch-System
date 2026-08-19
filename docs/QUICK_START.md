# Offline Map Factory 1.0 — Quick Start

**Status: BUILT / SELF-TESTED — LIVE ACCEPTANCE PENDING**

For full first-time setup, use the supplied **Offline Map Factory 1.0 Installation Guide**.

## Install once

1. Install **Python 3.14.5 (64-bit)**.
2. Install **QGIS 3.44.9 (64-bit)**.
3. Create:

```text
C:\Google Earth Project\QGIS\
```

4. Copy these two supplied files into that folder with their exact names:

```text
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
```

5. Keep the Factory launcher and `System Files` folder together.

User-facing Factory folder:

```text
RUN OFFLINE MAP FACTORY.bat
System Files\
```

## Make a map

1. Double-click **RUN OFFLINE MAP FACTORY.bat**.
2. Choose one of four sources:
   - Google Earth
   - Google Hybrid
   - Esri World
   - Esri World / Google Labels
3. Choose the map area using:
   - HOME EXTENT;
   - two diagonal points from Windows Clipboard History; or
   - two manual Latitude,Longitude points.
4. Choose minimum and maximum zoom, **Z0–Z20**.
5. Choose finished output:
   - **TPKX**;
   - **MBTiles**; or
   - **Both**.
6. Click **BUILD MAP**.
7. Choose the destination/name.
8. Review the build summary and begin.
9. Wait for **COMPLETE**.

## Output meaning

- **TPKX** — compact tile package for ArcGIS Earth and compatible offline deployment.
- **MBTiles** — compact raster tile master/interchange file.
- **Both** — preserves the MBTiles and creates the matching TPKX.

## Advanced Tool

If you already have suitable raster MBTiles:

1. Open **ADVANCED TOOLS**.
2. Choose **Tool 1 — MBTiles → TPKX**.
3. Select the MBTiles file.
4. Name the output TPKX.
5. Let the converter package the existing raster tiles.

The converter does not rerender the cartography.

## Current boundary

Offline Map Factory 1.0 deliberately does **not** include REST / Static WMTS output.

That work remains engineering history from the Map Fountain exploration.

## Operational rule

> **Build or refresh maps before they are needed. Essential map use must not depend on public Internet connectivity.**
