# Offline GeoStack

## QGIS → TPKX → ArcGIS Earth + Live Field Positioning

**A Windows-first offline geospatial stack for manufacturing native TPKX maps, running them in ArcGIS Earth, and feeding live GNSS / PRAVE / F22 / QR field data without depending on the Internet at showtime.**

This repository began life as the **Google Maps Dispatch System**. That history is preserved, but the current 2026 architecture has outgrown the old name.

**Offline GeoStack** is the master project identity.

The current production chain is:

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
          ↓
GNSS / PRAVE / F22 / QR / KML field inputs
```

> **QGIS makes the pixels. The converter packs the pixels. ArcGIS Earth displays the pixels.**

> **Build it online. Carry it offline.**

The normal user does not need to operate QGIS manually, understand SQLite, learn Compact Cache V2, or own ArcGIS Pro. The finished map is one `.tpkx` file that ArcGIS Earth opens natively.

---

## Why this exists

Two mature GIS worlds were already almost touching:

- **QGIS** could render sophisticated cartography and generate raster MBTiles.
- **ArcGIS Earth** could consume native TPKX packages beautifully, including offline.

What was missing for this workflow was the bridge:

```text
raster MBTiles → Esri Compact Cache V2 / TPKX
```

That bridge now exists as a custom Python converter and is integrated into **TPKX Map Factory v1.0.0**.

The converter does **not** rerender the map. It preserves the existing raster tile bytes, converts the addressing/container structure, builds Compact Cache V2 bundles, writes TPKX metadata, and packages the result.

That means a GIS professional can build whatever cartography they want in QGIS and use the advanced converter path to carry those finished pixels into ArcGIS Earth.

---

## TPKX Map Factory v1.0.0

**Status: LIVE-PROVEN / RELEASE ACCEPTED — 2026-08-15**

### Normal-user workflow

```text
1. Choose map source
2. Choose map area
3. Choose zoom range
4. BUILD TPKX MAP
5. Open the finished .tpkx in ArcGIS Earth
```

The normal GUI exposes four frozen map choices:

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

The same GUI includes:

**ADVANCED: MBTILES → TPKX**

That path is for people who already know what they are doing in QGIS.

Build parcels, contours, labels, roads, utilities, local imagery, historical scans, forestry layers, or any other suitable rasterized layer stack in QGIS, export compatible raster MBTiles, then let Offline GeoStack package it for ArcGIS Earth.

The beginner does not have to become a GIS operator. The GIS operator does not have to accept beginner limitations.

---

## The converter in one screenful

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

Critical TMS row conversion:

```text
y_arcgis = (2^z - 1) - y_tms
```

Tile placement and bundle indexing are deterministic. The raster tile bytes produced by QGIS are preserved rather than resampled into a new cartographic pyramid.

The result is not a screenshot and not a flattened poster. It is a real multi-zoom native TPKX package.

---

## Live acceptance evidence

This architecture has been tested beyond toy examples.

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

For this project, **ArcGIS Earth is the final operational acceptance authority** for finished TPKX output.

If AE opens it, places it correctly, exposes the expected zoom behavior, and renders the cartography correctly, the package answers to the runtime that matters.

---

## ArcGIS Earth runtime

ArcGIS Earth is the current primary 3D operational viewer.

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

## No operational Internet dependency

> **There can be no operational dependence on Internet connectivity. Period.**

Internet access can be used while preparing or refreshing maps. At incident/showtime, core operation must continue without a hotspot, without cellular coverage, and without a live map service.

The practical operating idea is simple:

```text
manufacture the geographic environment beforehand
        ↓
carry the TPKX locally
        ↓
open AE
        ↓
operate even if the network disappears
```

The map is already in the trunk.

The project uses the term **Persistent Geographic Context** for the operating condition in which position, surroundings, routes, and terrain remain continuously visible without having to summon them from a network.

---

## Live positioning and field inputs

Offline GeoStack is not only a map factory.

### PRAVE → ArcGIS Earth

The `$PRAVE` decoder now has a **LIVE-PROVEN ArcGIS Earth Automation API path**.

Controlled traffic displayed units `7-101` through `7-106` as native ArcGIS Earth drawings using the established fire-truck RSSI icon family.

Observed healthy test state included:

```text
UNITS=6
API_OK=47
API_BAD=0
BAD_RMC=0
BAD_PRAVE=0
RMC=FRESH
```

The forward architecture is protocol-specific decoding at the edge followed by normalization into one live-position manager rather than forcing every transport through KML.

Continuing inputs include:

- `$PRAVE`
- F22
- native GNSS / NMEA
- QR dispatch / bounded command input
- KML/KMZ / NetworkLinks where interoperability makes KML the correct tool

KML remains first-class. It simply no longer has to carry jobs that native TPKX or the Automation API can do better.

---

## Required QGIS projects

The two current QGIS reference projects are included in this repository under:

`required_qgis_projects/`

They are intended to be placed at:

```text
C:\Google Earth Project\QGIS\
```

Files:

- `REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz`
- `ESRI and Google Labels.qgz`

The project uses read-only reference files plus archive recovery rather than a hash-gate workflow.

---

## Repository map

### Start here

- `README.md` — public front door
- `docs/README.md` — documentation index and architecture diagram
- `docs/TECHNICAL_ARCHITECTURE.md` — detailed converter / pipeline engineering
- `docs/professional_report/` — long-form professional GIS and future-AI technical record
- `docs/PRAVE_ARCGIS_EARTH_INTEGRATION.md` — live positioning path
- `docs/OFFLINE_OPERATION_AND_PERSISTENT_GEOGRAPHIC_AWARENESS.md` — offline doctrine (filename retained for continuity; current public wording uses Geographic Context)
- `docs/AI_ENGINEERING_METHOD.md` — human/AI development method
- `CHANGELOG.md` — release and architecture evolution
- `CONTRIBUTING.md` — acceptance rules and do-not-regress guidance

### Legacy lineage

- `docs/LEGACY_GOOGLE_EARTH_README_2026-07-23.md`
- `docs/legacy/`

The old Google Earth material is preserved because it explains how the project learned the tile-pyramid, KML, cache, server, and field-deployment lessons that made the current architecture possible.

It is history, not the current baseline.

---

## Current requirements

### Windows

- Windows 10 or Windows 11, 64-bit

### Python

- Python **3.14.5** is the current known-good project baseline.
- No additional Python libraries are required by the core TPKX converter path.

### QGIS

- QGIS **3.44.9**

### ArcGIS Earth

ArcGIS Earth is the current primary viewer for finished TPKX packages.

---

## Engineering rules

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
- Distinguish DESIGNED, BUILT, BENCH-PROVEN, LIVE-PROVEN, and RELEASE-ACCEPTED states.
- Document enough detail that future GIS professionals and AI systems can reconstruct the system without inventing history.

---

## Source-data note

Offline GeoStack is a map-manufacturing, format-conversion, and field-display workflow. It does not grant rights to imagery, labels, basemaps, or other source data.

Users are responsible for complying with the terms, licenses, caching rules, export restrictions, attribution requirements, and redistribution rules that apply to each source they use.

Technical capability and source-data rights are separate questions.

---

## Authorship and AI collaboration

The project is developed and published by **Jim Gaddy** with **ChatGPT / Tool Master** serving as technical design, coding, GIS research, documentation, packaging, and diagnostic partner.

The MBTiles → TPKX bridge illustrates why AI changes the cost of this kind of engineering. The underlying formats and mathematics already existed. The 2026 difference is the ability to hold SQLite/MBTiles, Web Mercator tile math, TMS addressing, binary file structures, Compact Cache V2, Python implementation, QGIS rendering, Windows behavior, and ArcGIS Earth acceptance behavior in one working context and rapidly build the missing glue.

---

# Offline GeoStack

**QGIS → TPKX → ArcGIS Earth + Live Field Positioning**

> **It is not the number of bytes that matters. It is what the bytes are doing.**
