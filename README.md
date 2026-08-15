# Google Maps Dispatch System

## 2026 current architecture: TPKX Map Factory + ArcGIS Earth

This repository began as a Google Earth Pro terrestrial chartplotter and offline-map project. That history is still important, but the **current 2026 operational architecture has moved forward to ArcGIS Earth (AE)**.

The current map-production chain is:

```text
Map source / QGIS layer stack
          ↓
QGIS 3.44.9 raster rendering
          ↓
Temporary raster MBTiles
          ↓
Custom MBTiles → TPKX converter
(Esri Compact Cache V2)
          ↓
Native .tpkx package
          ↓
ArcGIS Earth
```

The project goal remains the same:

> **Complex machinery underneath. Cartoonishly simple controls on top.**

The major difference is that the finished map is now a **native TPKX package consumed directly by ArcGIS Earth**. Google Earth Pro/KML Super Overlay work is retained as project history and interoperability work, not the current primary deployment path.

---

## TPKX Map Factory v1.0.0

**TPKX Map Factory v1.0.0 is live-proven.**

It gives two deliberately different workflows from the same GUI.

### Normal-user workflow

1. Choose a map source.
2. Choose the map area.
3. Choose the zoom range.
4. Click **BUILD TPKX MAP**.
5. Open the resulting `.tpkx` directly in ArcGIS Earth.

The normal operator does not have to manually use QGIS, SQLite, MBTiles internals, Compact Cache V2, or ArcGIS Pro.

### Advanced GIS workflow

Advanced users who already work in QGIS can build any raster cartography they want, export it to raster MBTiles, and use:

**ADVANCED: MBTILES → TPKX**

This bypasses the canned Factory map-source stage and exposes the same proven converter engine directly.

That means a GIS professional can compose imagery, labels, parcel boundaries, roads, overlays, custom symbology, or other rasterized QGIS content and carry the finished pixels into ArcGIS Earth as a native TPKX package.

---

## Current frozen Factory recipe

The v1.0.0 public Factory uses:

- **QGIS 3.44.9**
- **Python 3.14.5** established known-good for this project
- Raster tile format: **PNG**
- DPI: **96**
- Antialiasing: **ON**
- Metatile: **4**
- Operator-selectable zoom range: **Z0–Z20**
- Temporary manufacturing format: **MBTiles**
- Final operator deliverable: **one `.tpkx` file**

Current Factory source choices:

1. **Google Earth**
2. **Google Hybrid**
3. **Esri World**
4. **Esri World / Google Labels**

The Esri World / Google Labels recipe is a QGIS-rendered two-layer composition: Esri imagery underneath with a labels-only Google layer above. QGIS performs the compositing; the TPKX converter does not need to understand how the pixels were created.

**Important:** map-source licensing, caching, export, and redistribution rules are source-specific. The Factory and converter are format/workflow tools; users remain responsible for using source data in ways permitted by the applicable provider or license.

---

## Why the converter matters

QGIS already has an excellent raster tile-rendering engine and can create MBTiles. ArcGIS Earth already has excellent native TPKX support. The missing bridge was a simple, reusable way to take a finished raster MBTiles pyramid and package it as Esri Compact Cache V2 / TPKX.

The custom converter was built from the published TPKX and Compact Cache V2 structure rather than by rerendering the map.

Conceptually it does this:

```text
MBTiles SQLite tiles
  zoom_level
  tile_column
  tile_row
  tile_data
        ↓
TMS row → ArcGIS top-origin row
        ↓
128 × 128 Compact Cache V2 bundle addressing
        ↓
.bundle binary records + index
        ↓
root.json + iteminfo.json + thumbnail
        ↓
ZIP64 .tpkx package
```

The important design decision is that the converter **preserves the existing raster tile bytes**. It does not redraw, sharpen, blur, resample, or reinterpret the cartography.

Tile placement is deterministic. MBTiles/TMS Y addressing is converted using the standard row inversion:

```text
y_arcgis = (2^z - 1) - y_tms
```

Bundle placement then uses integer addressing into 128 × 128 Compact Cache V2 packets.

This is a packaging and addressing conversion, not a second rendering stage.

---

## Live acceptance results

The system has been tested with both small smoke-test maps and large production-style packages.

### First integrated Factory proof

- Source: Google Hybrid
- Area: 113.31 sq mi
- Zooms: Z8–Z18
- Tiles: 23,119
- Finished Windows File Explorer size: **3,560,735 KB**
- Elapsed: 0:13:55
- Result: opened and rendered correctly in ArcGIS Earth

### Large advanced MBTiles → TPKX proof

- Existing MBTiles supplied directly to the advanced converter path
- Tiles: **271,497**
- Bundles: 47
- Zooms: Z8–Z18
- Finished Windows File Explorer size: **25,561,426 KB**
- Elapsed: 0:17:59
- Result: opened and rendered correctly in ArcGIS Earth

### Large Factory Esri World / Google Labels proof

- Area: approximately 1,378.89 sq mi
- Estimated / completed tiles: **271,242**
- Zooms: Z8–Z18
- Finished Windows File Explorer size: **24,291,406 KB**
- Elapsed: 2:51:52
- Result: opened and rendered correctly in ArcGIS Earth

### v1.0.0 release smoke test

- Manual decimal-degree GPS diagonal points
- Factory converted coordinates to the required EPSG:3857 extent
- Area: approximately 0.12 sq mi
- Finished file: `test2 small.tpkx`
- Windows File Explorer size reported by Factory: **12,852 KB**
- Elapsed: 0:00:12
- Result: opened and rendered correctly in ArcGIS Earth

For this project, **ArcGIS Earth is the final acceptance authority**: a package must open, land in the correct geographic position, expose the expected zoom behavior, and render correctly.

---

## ArcGIS Earth operational findings

ArcGIS Earth has proven to be a substantially better 2026 fit for this project than continuing to rebuild around legacy Google Earth behavior.

Live-observed / live-proven capabilities relevant to this project include:

- Native local TPKX display
- KML/KMZ compatibility
- KML NetworkLinks
- 3D globe operation
- Native GNSS/NMEA capability
- Local Automation API
- Native drawing/marker capability
- Session restoration: previously loaded TPKX files repopulate after restart
- Online point-to-point driving directions when connectivity is available

The system treats online services as optional enhancements, not operational dependencies.

---

## Hard offline requirement

This project now has a non-negotiable architectural rule:

> **There can be no operational dependence on Internet connectivity. Period.**

Internet access can be used during preparation to manufacture or refresh map packages. At incident/showtime, core operation must continue with the Internet absent.

That means:

- TPKX map display works locally.
- Essential map viewing does not require a hotspot.
- Essential command functions must not depend on cellular coverage.
- Loss of Internet must not collapse the command picture.

The concept that emerged from this work is **Persistent Geographic Awareness**:

> Keeping current position, surroundings, routes, and terrain continuously visible and available without having to summon them from a network.

A large-screen map display with local high-resolution imagery and own-position GNSS changes the operator experience from merely knowing **“I am at this coordinate”** to understanding **“I am in this place, on this road, inside this terrain.”**

---

## PRAVE / live-position integration

The larger dispatch system has also moved forward with ArcGIS Earth.

The project’s PRAVE decoder now has a live-proven ArcGIS Earth Automation API path. Test traffic displayed six units (`7-101` through `7-106`) as native ArcGIS Earth drawings using the established fire-truck RSSI icon set.

Observed test status included:

```text
UNITS=6
API_OK=47
API_BAD=0
BAD_RMC=0
BAD_PRAVE=0
RMC=FRESH
```

The current architecture is to decode protocol-specific inputs at the edge and normalize them into one live-position manager rather than force every transport through KML.

Planned / continuing inputs include:

- `$PRAVE`
- F22
- Native GNSS / NMEA
- QR dispatch / bounded command input
- KML where interoperability or external feeds make KML the correct tool

KML remains important. It is simply no longer required as the default live-position transport when the ArcGIS Earth Automation API provides a cleaner native path.

---

## Human-interface philosophy

The public Factory is intentionally not a GIS workstation UI.

The normal-user front door is designed around recognition rather than technical vocabulary:

- colored source icons
- map-area controls
- GPS coordinate entry
- visible zoom controls
- one large BUILD button
- one clearly separated advanced MBTiles conversion button
- visible progress state

The goal is:

> **see → recognize → click**

rather than:

> scan → read → interpret → decide → click

Advanced GIS capability is still present, but it is placed behind the advanced MBTiles → TPKX path so beginner simplicity is not sacrificed.

---

## Repository history

The repository name **Google-Maps-Dispatch-System** reflects the project’s origin. Earlier work proved:

- direct MBTiles → KML Super Overlay conversion
- local Google Earth Pro offline map deployment
- KML forests / Blooming Onion packaging
- map utility tooling
- warm-cache recovery experiments
- Network Earth local serving
- Google Earth Enterprise client/server archaeology

That work was not wasted. It produced the tile-pyramid, KML, caching, transport, and diagnostic knowledge that made the ArcGIS Earth / TPKX architecture understandable quickly.

However, **the current baseline is ArcGIS Earth + TPKX**. Do not revive legacy Google Earth workflows and present them as current architecture.

The previous README has been preserved in this repository as:

`docs/LEGACY_GOOGLE_EARTH_README_2026-07-23.md`

---

## Files in this repository

Current public material includes:

- `README.md` — current project front door
- `docs/TECHNICAL_ARCHITECTURE.md` — GIS/engineering detail
- `docs/LEGACY_GOOGLE_EARTH_README_2026-07-23.md` — preserved previous public architecture
- `releases/TPKX_MAP_FACTORY_v1_0_0.zip` — TPKX Map Factory v1.0.0
- `releases/TPKX_MAP_FACTORY_v1_0_0_RELEASE_NOTES.md` — v1.0 release record

A longer professional engineering report also exists for GIS professionals and future AI/human maintainers, covering project lineage, converter internals, acceptance evidence, PRAVE integration, offline doctrine, and do-not-regress rules.

---

## Requirements

### Windows

- Windows 10 or Windows 11, 64-bit

### Python

- Python **3.14.5** is the current known-good project baseline.
- No additional Python libraries are required for the TPKX Factory/converter path.

### QGIS

- QGIS **3.44.9**
- Current project path convention:

```text
C:\Google Earth Project\QGIS\
```

The required QGIS project files are placed there for Factory use.

### ArcGIS Earth

ArcGIS Earth is the current primary viewer for finished `.tpkx` packages.

---

## Design principles

- Offline operation is fundamental, not a fallback mode.
- Core operation must not depend on cellular or Internet availability.
- Use native TPKX for ArcGIS Earth raster basemaps.
- Use QGIS as the rendering engine.
- Preserve finished raster tiles during MBTiles → TPKX conversion.
- Keep the proven converter stable; integrate around it rather than casually rewriting it.
- Produce one clean finished TPKX for the operator.
- Keep temporary manufacturing material out of the destination directory.
- Keep simple users simple and advanced users powerful.
- Retain KML for the jobs KML does well.
- Treat Google Earth work as valuable lineage, not the new baseline.
- Publicly document the machinery so other people and future AI systems can reconstruct it.

---

## Authorship and AI collaboration

The project is developed and published by **Jim Gaddy** with **ChatGPT / Tool Master** serving as technical design, coding, GIS research, documentation, packaging, and diagnostic partner.

The MBTiles → TPKX converter is an example of the kind of engineering problem that becomes dramatically more approachable when one working context can simultaneously reason about:

- SQLite / MBTiles
- Web Mercator tile mathematics
- TMS/XYZ addressing
- binary file structures
- Esri Compact Cache V2
- Python implementation
- QGIS rendering
- ArcGIS Earth acceptance behavior

The underlying formats and mathematics are not new. The 2026 change is the reduced cost of assembling the knowledge and producing the missing glue.

---

## Current project motto

> **Build it online. Carry it offline.**

And the engineering version:

> **QGIS makes the pixels. The converter packs the pixels. ArcGIS Earth displays the pixels.**
