# Google Maps Dispatch System

## 2026 current architecture: TPKX Map Factory + ArcGIS Earth

This repository began as a Google Earth Pro terrestrial chartplotter and offline-map project. That history is preserved here, but the **current operational architecture has moved forward to ArcGIS Earth (AE) with native TPKX packages**.

The present map-production chain is:

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

> **Complex machinery underneath. Cartoonishly simple controls on top.**

The normal user does not need to operate QGIS manually, understand SQLite, learn Compact Cache V2, or own ArcGIS Pro. The finished map is one `.tpkx` file that ArcGIS Earth opens natively.

---

## TPKX Map Factory v1.0.0

**Status: LIVE-PROVEN / RELEASE ACCEPTED — 2026-08-15**

TPKX Map Factory v1.0.0 is the first frozen public baseline of the ArcGIS Earth / TPKX architecture.

### Normal-user workflow

```text
1. Choose map source
2. Choose map area
3. Choose zoom range
4. BUILD TPKX MAP
5. Open the finished .tpkx in ArcGIS Earth
```

The normal GUI exposes four map choices:

1. **Google Earth**
2. **Google Hybrid**
3. **Esri World**
4. **Esri World / Google Labels**

The current frozen raster recipe is:

- QGIS **3.44.9**
- Python **3.14.5** established known-good
- PNG raster tiles
- **96 DPI**
- antialiasing **ON**
- metatile **4**
- operator-selectable **Z0–Z20**
- temporary manufacturing format: **MBTiles**
- final operator deliverable: **one `.tpkx`**

### Advanced GIS workflow

The same GUI also includes:

**ADVANCED: MBTILES → TPKX**

A GIS professional can therefore build any suitable raster cartography in QGIS, export the finished tile pyramid to MBTiles, and use the Factory only as the TPKX packaging bridge.

That keeps the beginner interface simple without taking power away from advanced users.

---

## Why the converter matters

QGIS already knows how to create the map. ArcGIS Earth already knows how to display native TPKX. The missing interoperability bridge was:

```text
QGIS raster MBTiles → Esri Compact Cache V2 / TPKX
```

The custom Python converter was implemented from the published TPKX / Compact Cache V2 structure.

It **does not rerender the cartography**.

It reads the already-rendered raster tiles from MBTiles, converts the row addressing required by the target cache structure, writes Compact Cache V2 bundles and package metadata, and produces a TPKX archive.

Conceptually:

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
.bundle binary records + indexes
        ↓
root.json + iteminfo.json + thumbnail
        ↓
ZIP64 .tpkx
```

The critical TMS row conversion is:

```text
y_arcgis = (2^z - 1) - y_tms
```

Tile placement and bundle indexing are deterministic. The raster tile bytes produced by QGIS are preserved rather than being resampled into a new cartographic pyramid.

> **QGIS makes the pixels. The converter packs the pixels. ArcGIS Earth displays the pixels.**

---

## Live acceptance evidence

The architecture has been tested well beyond toy examples.

### First integrated Factory proof

- Source: Google Hybrid
- Area: 113.31 sq mi
- Zooms: Z8–Z18
- Tiles: 23,119
- Finished Windows File Explorer size: **3,560,735 KB**
- Elapsed: 0:13:55
- ArcGIS Earth: **PASS**

### Large advanced MBTiles → TPKX proof

- Existing MBTiles supplied directly to the advanced converter
- Tiles: **271,497**
- Bundles: 47
- Zooms: Z8–Z18
- Finished Windows File Explorer size: **25,561,426 KB**
- Elapsed: 0:17:59
- ArcGIS Earth: **PASS**

### Large Esri World / Google Labels Factory proof

- Area: approximately 1,378.89 sq mi
- Tiles: **271,242**
- Zooms: Z8–Z18
- Finished Windows File Explorer size: **24,291,406 KB**
- Elapsed: 2:51:52
- ArcGIS Earth: **PASS**

### v1.0.0 release smoke test

- Map area entered from two manual decimal-degree GPS diagonal points
- Factory normalized the corners and produced the EPSG:3857 HOME EXTENT
- Area: approximately 0.12 sq mi
- Output: `test2 small.tpkx`
- Windows File Explorer size reported by Factory: **12,852 KB**
- Elapsed: 0:00:12
- ArcGIS Earth: **PASS**

For this project, **ArcGIS Earth is the final operational acceptance authority** for a finished TPKX: it must open, land in the correct place, expose the expected zoom behavior, and render correctly.

---

## ArcGIS Earth operational role

ArcGIS Earth is now the project’s primary viewer.

Relevant capabilities observed or proven during this project include:

- native local TPKX display
- KML/KMZ support
- KML NetworkLinks
- 3D globe navigation
- native GNSS/NMEA capability
- local Automation API
- native drawing / marker display
- session restoration of previously loaded TPKX files
- online point-to-point driving directions when connectivity exists

The key architectural rule is that online services are enhancements, not dependencies.

---

## Hard offline requirement

> **There can be no operational dependence on Internet connectivity. Period.**

Internet access can be used while preparing or refreshing maps. At incident/showtime, core operation must continue without a hotspot, without cellular coverage, and without a live map service.

The operating concept that emerged from this work is **Persistent Geographic Awareness**:

> Keeping current position, surroundings, routes, and terrain continuously visible and available without having to summon them from a network.

With a large display, local high-resolution TPKX imagery, and own-position GNSS, the operator moves from merely knowing:

```text
I am at this coordinate.
```

to understanding:

```text
I am on this road, in this forest, inside this terrain, with this context around me.
```

---

## PRAVE / live-position integration

The larger dispatch project has also moved forward with ArcGIS Earth.

The `$PRAVE` decoder now has a **LIVE-PROVEN ArcGIS Earth Automation API path**. Controlled test traffic displayed units `7-101` through `7-106` as native ArcGIS Earth drawings using the established fire-truck RSSI icon family.

Observed healthy test state included:

```text
UNITS=6
API_OK=47
API_BAD=0
BAD_RMC=0
BAD_PRAVE=0
RMC=FRESH
```

The forward design is protocol-specific decoding at the edge followed by normalization into one live-position manager rather than forcing every transport through KML.

Continuing inputs include:

- `$PRAVE`
- F22
- native GNSS / NMEA
- QR dispatch / bounded command input
- KML/KMZ / NetworkLinks where interoperability makes KML the correct tool

KML remains important. It is no longer required as the default live-position transport merely because the original Google Earth architecture used it.

---

## Human-interface philosophy

The public Factory is intentionally **not** designed like a GIS workstation.

The GUI uses colored icons and strong visual landmarks so the operator can:

```text
see → recognize → click
```

instead of:

```text
scan → read → interpret → decide → click
```

The normal-user front door remains simple. Advanced GIS freedom lives behind the existing-MBTiles converter path.

---

## Repository map

The repository now separates the current architecture from its history.

### Current material

- `README.md` — current public front door
- `docs/TECHNICAL_ARCHITECTURE.md` — GIS/software architecture in detail
- `docs/NOTES_FOR_GIS_PROFESSIONALS.md` — short professional interpretation
- `docs/QUICK_START.md` — normal-user and advanced-user workflow
- `docs/PROJECT_STATUS_2026-08-15.md` — frozen status checkpoint
- `docs/AI_CONTINUITY_RESTART_NOTE.md` — restart context for future human/AI maintainers
- `docs/HISTORICAL_TIMELINE.md` — project evolution
- `docs/SOURCE_AND_LICENSING_NOTE.md` — separation between technical capability and source-data rights
- `releases/TPKX_MAP_FACTORY_v1_0_0_RELEASE_NOTES.md` — v1.0 release record
- `releases/PUBLIC_RELEASE_CHECKLIST.md` — v1.0 release gates

### Preserved legacy material

- `docs/LEGACY_GOOGLE_EARTH_README_2026-07-23.md`

The legacy document is preserved so future readers can reconstruct the evolution without mistaking superseded Google Earth/KML architecture for the current baseline.

---

## Current requirements

### Windows

- Windows 10 or Windows 11, 64-bit

### Python

- Python **3.14.5** is the current known-good project baseline.
- No additional Python libraries are required by the core TPKX converter path.

### QGIS

- QGIS **3.44.9**
- Current project path convention:

```text
C:\Google Earth Project\QGIS\
```

The required QGIS project files are placed there for Factory use.

### ArcGIS Earth

ArcGIS Earth is the current primary viewer for finished TPKX packages.

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
- Treat Google Earth work as valuable lineage, not the current baseline.
- Distinguish DESIGNED, BUILT, BENCH-PROVEN, and LIVE-PROVEN states.
- Document enough detail that future GIS professionals and AI systems can reconstruct the system without inventing history.

---

## Source-data note

TPKX Map Factory is a map-manufacturing and format-conversion workflow. It does not grant rights to imagery, labels, basemaps, or other source data.

Users are responsible for complying with the terms, licenses, caching rules, export restrictions, attribution requirements, and redistribution rules that apply to each source they use.

The technical ability to request, render, cache, package, or display content is separate from the legal right to redistribute that content.

---

## Authorship and AI collaboration

The project is developed and published by **Jim Gaddy** with **ChatGPT / Tool Master** serving as technical design, coding, GIS research, documentation, packaging, and diagnostic partner.

The MBTiles → TPKX bridge illustrates why AI changes the cost of this kind of engineering. The underlying formats and mathematics were already available. The 2026 difference is the ability to hold SQLite/MBTiles, Web Mercator tile math, TMS addressing, binary file structures, Compact Cache V2, Python implementation, QGIS rendering, and ArcGIS Earth acceptance behavior in one working context and rapidly build the missing glue.

---

## Project mottoes

> **Build it online. Carry it offline.**

> **QGIS makes the pixels. The converter packs the pixels. ArcGIS Earth displays the pixels.**

And the small-software lesson:

> **It is not the number of bytes that matters. It is what the bytes are doing.**
