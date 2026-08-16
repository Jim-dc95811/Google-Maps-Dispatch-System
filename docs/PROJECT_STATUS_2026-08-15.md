# Offline GeoStack — Project Status — 2026-08-15

## RELEASE ACCEPTED

**TPKX Map Factory v1.0.0** is the current map-manufacturing baseline inside **Offline GeoStack**.

### LIVE-PROVEN

- QGIS 3.44.9 raster production
- temporary raster MBTiles manufacturing stage
- custom MBTiles → TPKX conversion
- Esri Compact Cache V2 packaging
- native TPKX display in ArcGIS Earth
- large Factory production runs
- large existing-MBTiles advanced conversion
- manual decimal-degree GPS extent entry
- ArcGIS Earth session restoration of loaded TPKX packages
- PRAVE → ArcGIS Earth Automation API native drawing path

### CURRENT MASTER PROJECT

**Offline GeoStack — QGIS → TPKX → ArcGIS Earth + Live Field Positioning**

### CURRENT PRIMARY VIEWER

**ArcGIS Earth (AE)**

### CURRENT HARD REQUIREMENT

**No operational dependence on Internet connectivity.**

### CURRENT PUBLIC FACTORY SETTINGS

- Python 3.14.5
- QGIS 3.44.9
- PNG
- 96 DPI
- antialiasing ON
- metatile 4
- Z0–Z20

### FACTORY SOURCES

- Google Earth
- Google Hybrid
- Esri World
- Esri World / Google Labels

### RELEASE PACKAGE

The accepted Windows archive is named:

`TPKX_MAP_FACTORY_v1_0_0.zip`

The release is accepted and preserved in the canonical project archive. The GitHub documentation and required QGIS projects are current. The exact binary archive should only be attached to GitHub when the accepted ZIP can be uploaded intact; a connector-truncated copy was deliberately removed.

### TECHNICAL DETAIL

See:

- `docs/professional_report/README.md`
- `docs/TECHNICAL_ARCHITECTURE.md`
- `releases/README.md`

### PROJECT LINEAGE

The repository slug and earlier **Google Maps Dispatch System** naming are historical lineage. The Google Earth Pro / KML Super Overlay architecture is preserved under `docs/LEGACY_GOOGLE_EARTH_README_2026-07-23.md` and should be treated as history rather than the current baseline.
