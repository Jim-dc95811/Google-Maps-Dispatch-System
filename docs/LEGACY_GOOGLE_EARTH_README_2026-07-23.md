# Legacy Google Earth README — preserved 2026-07-23

This file preserves the public README that represented the project before the 2026 pivot to ArcGIS Earth + TPKX.

The content below is historical. It is retained so future GIS professionals, developers, and AI systems can reconstruct the project lineage without confusing legacy architecture for the current baseline.

---

# Google Maps Dispatch System

**Offline-capable Google Earth mapping, MBTiles production, and field-display tools built for practical deployment.**

This project turns Google Earth Pro into a locally controlled terrestrial mapping platform. It can manufacture portable raster MBTiles from Earth imagery or street maps, prepare large territories for batch production, convert supported raster MBTiles into local KML Super Overlays, and support future GPS, dispatch, QR, F22, and radio-linked field workflows.

The design goal is simple:

> **Complex machinery underneath. Cartoonishly simple controls on top.**

---

## What This Project Does

The then-current map-production workflow was:

```text
Four GPS corners / QGIS extent / BBoxFinder GDAL box
                         ↓
          Coordinate normalization to EPSG:3857
                         ↓
        Headless QGIS 3.44.9 MBTiles production
                         ↓
             Verified raster MBTiles output
                         ↓
      Optional local KML Super Overlay expansion
                         ↓
               Google Earth Pro offline display
```

The operator did not need to work inside the QGIS desktop interface. Python acted as the foreman while QGIS performed the heavy rendering work invisibly through `qgis_process`.

---

## Then-current public package

The old package exposed:

```text
Factory\
Tools\
Open Map Utility Toolbox.bat
Start MBTiles Factory.bat
```

The Factory created verified MBTiles from Earth imagery, street maps, four GPS corners, QGIS EPSG:3857 extents, BBoxFinder/GDAL boxes, and batches of up to 10 QGIS extents.

The old production settings included:

- Zoom range: 0–18
- DPI: 192
- Tile format: PNG
- Antialiasing: enabled
- Metatile size: 4

The Map Utility Toolbox contained the 24 Equal-Size Tile Splitter, Extents Neighbor Tool, and Bloom Directory Eraser.

---

## Old minimum requirements

- Windows 10/11 64-bit
- Python 3.12.10
- QGIS 3.44.9 Solothurn
- Internet access during MBTiles manufacturing

No additional Python libraries were required for the MBTiles Factory or utility toolbox.

---

## Why MBTiles mattered in the legacy architecture

MBTiles served as the compact shipping/archive format while expanded KML/PNG Super Overlay forests were runtime products for Google Earth Pro.

The project treated the MBTiles file as the master shipping container and regenerated expanded KML trees at the destination rather than copying enormous directory forests.

---

## Google Earth Pro legacy role

Google Earth Pro was the primary operational viewer.

Local KML Super Overlays allowed large raster collections to display without depending on a live map server. A major offline concern was Google Earth cache/bootstrap behavior, which led to warm-cache recovery work.

Historical rule:

> Do not clear the Google Earth cache while the computer is offline.

That rule belongs to the old Google Earth operational architecture and is not part of the current ArcGIS Earth/TPKX baseline.

---

## Historical project direction

The larger system included or contemplated:

- Local Earth and Street map production
- Offline Google Earth Super Overlays
- Real GPS input
- F22 position messages
- `$PRAVE` input
- QR-based dispatch coordinates
- Field markers and arrival reporting
- NOAA nautical charts
- FIRMS current-fire KML
- Optional radio transport
- Offline-first field display behavior

The project began as an open terrestrial chartplotter / AVL system for slow-moving wildland public-safety equipment and grew into a broader local mapping and field-display platform.

---

## Historical design philosophy

- Offline-capable by default
- No account required for core operation
- No recurring software service required
- Open and locally controlled
- Simple operator interface
- Reproducible production settings
- Portable files instead of platform lock-in
- Public documentation and reusable tools

---

## Supersession note

The direct SQLite MBTiles-to-Super-Overlay route replaced earlier `gdal2tiles` work inside the Google Earth branch. Later, the entire primary viewer architecture moved forward again to ArcGIS Earth with native TPKX packages.

See the repository root `README.md` for the current architecture.
