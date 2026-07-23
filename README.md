# Google Maps Dispatch System

**Offline-capable Google Earth mapping, MBTiles production, and field-display tools built for practical deployment.**

This project turns Google Earth Pro into a locally controlled terrestrial mapping platform. It can manufacture portable raster MBTiles from Earth imagery or street maps, prepare large territories for batch production, convert supported raster MBTiles into local KML Super Overlays, and support future GPS, dispatch, QR, F22, and radio-linked field workflows.

The design goal is simple:

> **Complex machinery underneath. Cartoonishly simple controls on top.**

---

## What This Project Does

The current map-production workflow is:

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

The operator does not need to work inside the QGIS desktop interface. Python acts as the foreman while QGIS performs the heavy rendering work invisibly through `qgis_process`.

---

## Current Public Package

After extracting the complete ZIP, the user sees only:

```text
Factory\
Tools\
Open Map Utility Toolbox.bat
Start MBTiles Factory.bat
```

That is intentional.

### Start MBTiles Factory

Use the Factory to create verified MBTiles from:

- Earth imagery
- Street maps
- Four GPS corners
- A QGIS EPSG:3857 extent
- A BBoxFinder / GDAL box
- A batch of up to 10 QGIS extents

The production settings are locked for repeatability:

- Zoom range: **0–18**
- DPI: **192**
- Tile format: **PNG**
- Antialiasing: **Enabled**
- Metatile size: **4**

The Factory verifies the resulting SQLite/MBTiles structure, zoom range, tile format, and an extracted sample tile.

### Open Map Utility Toolbox

The Toolbox contains three deliberate utilities:

#### 24 Equal-Size Tile Splitter

Splits one parent map extent into:

- 6 columns
- 4 rows
- 24 equal-size, perfectly aligned child extents

Numbering begins in the northwest corner and proceeds east, row by row, toward the south.

#### Extents Neighbor Tool

Given one center extent, generates eight same-size adjacent extents:

```text
A  B  C
H  1  D
G  F  E
```

All shared boundaries are aligned without gaps or overlaps.

#### Bloom Directory Eraser

Permanently deletes one expanded KML Super Overlay directory.

This operation bypasses the Recycle Bin and requires explicit confirmation. Compact MBTiles masters should be preserved before any expanded directory is erased.

---

## Minimum Requirements

### Operating System

- Windows 10 or Windows 11
- 64-bit

### Python

- Python **3.12.10**
- 64-bit
- Install from the official Python release page
- Check **Add python.exe to PATH** during installation

No additional Python libraries are required for the MBTiles Factory or Map Utility Toolbox.

### QGIS

- QGIS **3.44.9 Solothurn**
- 64-bit
- Default installation path:

```text
C:\Program Files\QGIS 3.44.9
```

### Other Requirements

- Internet access while manufacturing MBTiles
- Adequate free disk space
- The complete ZIP must be extracted before either BAT launcher is run

---

## Quick Start

1. Install Python 3.12.10.
2. Install QGIS 3.44.9.
3. Extract the complete project ZIP.
4. Double-click:

```text
Start MBTiles Factory.bat
```

or:

```text
Open Map Utility Toolbox.bat
```

5. Follow the controls on screen.

No manual QGIS operation is required during normal production.

---

## Why MBTiles?

MBTiles is the project’s compact transport and archive format.

A single MBTiles file can contain:

- Raster tiles
- Multiple zoom levels
- Bounds and metadata
- A complete portable map package inside one SQLite database

The MBTiles file is the **master shipping container**.

Expanded KML/PNG Super Overlay directories are runtime products. They may contain enormous numbers of small files and should normally be regenerated at the destination rather than copied between drives.

---

## Google Earth Pro

Google Earth Pro is the primary operational viewer.

Local KML Super Overlays allow large raster map collections to display without depending on a live map server. The project has also proven compatibility with selected external raster MBTiles, including NOAA chart material.

Important offline rule:

> **Do not clear the Google Earth cache while the computer is offline.**

Maintain a known-good archived warm cache so Google Earth can be restored if the active cache is cleared or corrupted.

---

## Project Direction

The larger Google Maps Dispatch System includes or is intended to include:

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

The project began as an open terrestrial chartplotter / AVL system for slow-moving wildland public-safety equipment and has grown into a broader local mapping and field-display platform.

---

## Design Philosophy

- Offline-capable by default
- No account required for core operation
- No recurring software service required
- Open and locally controlled
- Simple operator interface
- Reproducible production settings
- Portable files instead of platform lock-in
- Public documentation and reusable tools

This is not a cloud tracker wearing a different hat. It is a local mapping system built so the operator retains the maps, the data, and the machinery.

---

## Current Status

The Factory, Batch Factory, Map Utility Toolbox, 24-tile splitter, neighbor generator, and guarded directory eraser are working.

The current public-release work is focused on:

- Burn-in testing
- Final package auditing
- Dependency verification
- Exact installer preservation
- Google Earth appliance optimization
- Documentation and video
- A complete end-to-end public reveal

Proven production milestones include a completed 24-child master grid and verified offline Google Earth display using local Super Overlays.

---

## Important Project Rules

- Preserve compact MBTiles masters.
- Avoid copying expanded Super Overlay trees unless necessary.
- Expand maps at the destination computer.
- Use very small test areas before beginning large production.
- Keep active map blooms on a fast local SSD when possible.
- Do not modify a proven production build during burn-in without a documented reason.
- Do not revive superseded workflows as though they are current.

The direct SQLite MBTiles-to-Super-Overlay route replaced the earlier `gdal2tiles` workflow for this project.

---

## Acknowledgment

This project is being developed and published by **Jim Gaddy** with ChatGPT serving as a technical design, coding, documentation, and packaging partner.

The mission is to make practical offline mapping tools available to others without requiring proprietary accounts or recurring services.

---

## Project Motto

> **Four coordinates in. Verified MBTiles out.**

And when the factory is running:

> **The machine grinds like the tide.**
