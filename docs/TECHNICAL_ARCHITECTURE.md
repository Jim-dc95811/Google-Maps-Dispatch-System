# Offline GeoStack — Technical Architecture

## Purpose

This document records the current 2026 architecture of **Offline GeoStack** after the move from a single TPKX deployment path to a dual local-deployment model:

1. **native TPKX** for ArcGIS Earth local-file use;
2. **raster MBTiles served as local HTTPS WMTS** for ArcGIS Earth Mobile.

The frozen v1.0.0 TPKX Map Factory remains the accepted baseline. Later TEST branches expand around that baseline without rewriting its proven converter.

Master project identity:

**Offline GeoStack — QGIS → MBTiles / TPKX → ArcGIS Earth Desktop + Mobile + Live Field Positioning**

---

## 1. Current architectural summary

```text
Source imagery / QGIS layer stack
        ↓
QGIS 3.44.9 rendering engine
        ↓
verified raster tile pyramid in MBTiles
        ↓
        ├───────────────────────────────────────────┐
        │                                           │
        ↓                                           ↓
Custom MBTiles → TPKX converter             USB Map Fountain
        ↓                                   local HTTPS WMTS
Compact Cache V2 bundles                            ↓
        ↓                                   Android USB tether
native .tpkx                                        ↓
        ↓                                   ArcGIS Earth Mobile
ArcGIS Earth Windows / Mobile
```

Live positioning and command context sit around the ArcGIS Earth runtime:

- native GNSS / NMEA;
- PRAVE;
- F22;
- QR;
- KML/KMZ / NetworkLinks where appropriate.

No outside Internet connection is required for either local raster deployment path.

---

## 2. Why QGIS remains the rendering engine

QGIS already solves the GIS/cartographic work:

- reprojection;
- raster/vector compositing;
- label rendering;
- antialiasing;
- source access;
- zoom-dependent cartography;
- tile-pyramid generation;
- MBTiles output.

The Factory therefore treats QGIS as a rendering engine rather than rebuilding GIS behavior.

Current known-good render baseline:

- QGIS 3.44.9;
- EPSG:3857 / Web Mercator tile scheme;
- PNG raster tiles;
- 96 DPI;
- antialiasing ON;
- metatile 4;
- operator-selectable Z0–Z20.

---

## 3. MBTiles is now a branch point

MBTiles is SQLite-based and exposes the raster pyramid through the standard raster `tiles` table:

```text
zoom_level
tile_column
tile_row
tile_data
```

`tile_data` contains already-rendered PNG/JPEG bytes.

### Frozen v1.0 meaning

In the release-accepted v1.0.0 normal workflow, MBTiles is temporary manufacturing material and the published operator product is TPKX.

### Current v1.2 TEST meaning

The mobile Map Fountain proof changed the value of MBTiles. It can now be a deliberate final product when the operator wants live local serving to ArcGIS Earth Mobile.

TPKX Map Factory v1.2.0 TEST therefore exposes:

```text
TPKX
MBTiles
Both
```

`Both` is the current TEST default.

The architecture still manufactures **one** QGIS tile pyramid. It does not create separate cartography for the two outputs.

---

## 4. MBTiles → TPKX bridge

The custom converter implements the published TPKX / Compact Cache V2 structure.

It does **not** rerender the map, flatten zooms, or resample imagery. It preserves the existing tile image bytes and changes the addressing/container structure around them.

Critical TMS row conversion:

```text
y_arcgis = (2^z - 1) - y_tms
```

`x` remains the tile column.

Compact Cache V2 uses a packet size of 128:

```text
bundle_row = floor(row / 128) × 128
bundle_col = floor(col / 128) × 128
index = (row mod 128) × 128 + (col mod 128)
```

The converter writes bundle headers/indexes/tile bytes plus package metadata such as:

- `root.json`;
- `iteminfo.json`;
- `thumbnail.png`;
- zoom-level bundle directories;
- ZIP64-compatible `.tpkx` container.

The frozen `MBTiles_to_TPKX_v0_1_0.py` converter is LIVE-PROVEN and should not be casually rewritten.

---

## 5. Tile-byte preservation

For raster PNG/JPEG MBTiles, the converter reads `tile_data` from SQLite and writes those bytes into Compact Cache V2.

This preserves QGIS-created cartography, including zoom-specific label placement and layer hierarchy.

Useful shorthand:

> **QGIS makes the pixels. The converter packs the pixels. ArcGIS Earth displays the pixels.**

For the Map Fountain path, the converter is not involved:

> **QGIS makes the pixels. MBTiles stores the pixels. Map Fountain serves the requested pixels. ArcGIS Earth Mobile displays them.**

---

## 6. TPKX acceptance

Structural validation is necessary but not sufficient.

A TPKX is accepted only when the intended ArcGIS Earth runtime:

- opens it without complaint;
- places it correctly;
- exposes the expected zoom behavior;
- renders the expected imagery/cartography;
- behaves normally during navigation.

This project does not substitute byte-level internal success for target-viewer acceptance.

That lesson became especially important during the TPKX → MBTiles recovery experiment: controlled recovery could match raster tile bytes, yet a recovered production MBTiles later showed blurred/missing regions on ArcGIS Earth Mobile. The recovery path was therefore rejected for production use.

---

## 7. TPKX Map Factory workflows

### Frozen v1.0 normal path

```text
choose source
→ choose area
→ choose zoom range
→ QGIS MBTiles
→ frozen converter
→ TPKX
→ ArcGIS Earth
```

### Frozen v1.0 advanced path

```text
existing raster MBTiles
→ ADVANCED MBTILES → TPKX
→ ArcGIS Earth
```

### v1.2.0 TEST normal output choices

```text
TPKX
MBTiles
Both
```

- **TPKX:** build MBTiles, convert, verify, publish TPKX.
- **MBTiles:** build/verify/publish MBTiles and skip converter.
- **Both:** preserve the same QGIS-built MBTiles and also create TPKX from it.

The accepted v1.0.0 branch remains separate until v1.2 earns live acceptance.

---

## 8. Source recipes

The frozen v1.0.0 GUI exposes:

1. Google Earth;
2. Google Hybrid;
3. Esri World;
4. Esri World / Google Labels.

The converter remains source-agnostic. Licensing, caching, attribution, export, and redistribution rules remain source-specific and separate from binary-format capability.

---

## 9. ArcGIS Earth Windows role

ArcGIS Earth Windows remains the primary desktop 3D operational runtime.

Live-proven/observed project capabilities include:

- local TPKX display;
- KML/KMZ / NetworkLinks;
- native GNSS/NMEA own-position;
- local Automation API;
- native drawings / markers;
- PRAVE live-position rendering;
- session restoration of loaded TPKX packages.

Known-good native GNSS observation used 9600 baud with GLL + RMC present.

---

## 10. ArcGIS Earth Mobile local TPKX

**Status: LIVE-PROVEN on multiple packages — 2026-08-16**

Android ArcGIS Earth Mobile opened locally stored TPKX packages through `Add Data → File`, including:

- Rasta Thames Bridge;
- smaller Esri map;
- smaller Google Hybrid map.

One larger Google Hybrid package returned `spatial reference not supported`. Because other packages loaded, treat this as a package-level compatibility question until metadata differences are isolated.

---

## 11. USB Map Fountain

**Status: LIVE-PROVEN — v0.2.1 TEST — 2026-08-16**

Live chain:

```text
raster MBTiles on Windows PC / SSD
        ↓
HTTPS WMTS
        ↓
Android USB tether / Remote NDIS
        ↓
ArcGIS Earth Mobile
```

The Windows PC listens on the USB-tether interface. ArcGIS Earth Mobile requests individual WMTS tiles by zoom/row/column.

Observed live server traffic showed Android requests such as:

```text
GET /wmts/tiles/<unique-map-id>/GoogleMapsCompatible/<z>/<row>/<col>.png
→ 200
```

### Why unique map IDs matter

An early multi-map build reused one WMTS layer identity and one tile URL namespace. ArcGIS Earth Mobile could therefore display stale cached tiles from the previous small test map.

v0.2.1 fixed this by assigning every selected MBTiles a unique map/service identity and unique tile URL namespace.

### HTTPS + QR

The live test progressed from HTTP to HTTPS and then QR-based service entry.

The current prototype certificate was tied to the observed USB-tether PC address during testing. General certificate/IP lifecycle management remains productization work; do not confuse the live proof with a finished universal installer.

### Offline acceptance

Outside Internet connectivity was removed while the private USB-tether network remained active. ArcGIS Earth Mobile continued consuming/displaying local map tiles.

### Multiple large maps

Three different substantial MBTiles were displayed through the path, including a large Lago panorama.

### Operator envelope

Live observation:

> **Deliberate pan/zoom is smooth and reliable. Rapid repeated zooming or whipping the view around can outrun the current delivery/render path.**

This is current operator guidance, not a claim of a fixed theoretical limit.

---

## 12. TPKX → MBTiles recovery experiment

**Status: REJECTED AS PRODUCTION PATH**

A reverse Compact Cache V2 tool was prototyped to recover raster tiles from existing TPKX packages.

Controlled Thames Bridge testing showed:

- bundle extraction worked;
- tile coordinate recovery worked;
- recovered tile bytes matched the controlled original tile set.

A subsequent production ESG1S recovery produced a large MBTiles whose mobile visual result included blurred/missing regions.

Decision:

- remove recovery from TPKX Map Factory v1.2;
- rebuild important MBTiles directly through QGIS;
- preserve MBTiles at manufacture time whenever Map Fountain deployment may be needed.

This is a deliberate target-viewer decision, not a theoretical statement that Compact Cache V2 cannot be decoded.

---

## 13. Offline doctrine

> **There can be no operational dependence on Internet connectivity. Period.**

This requirement refers to outside/public connectivity, not useful private local links.

Both are valid offline designs:

```text
TPKX already stored locally
```

and

```text
MBTiles on local depot
→ private USB/local network
→ local HTTPS WMTS
→ ArcGIS Earth Mobile
```

The Map Fountain path was live-proven with outside Internet removed.

---

## 14. Persistent Geographic Context

**Persistent Geographic Context** describes a state in which position, surroundings, routes, terrain, and local context remain continuously visible without depending on a public-network request at showtime.

Local TPKX and local Map Fountain are two different ways to keep that geographic inventory close to the operator.

---

## 15. Human factors / GUI rules

Normal-user GUI design should favor:

```text
see → recognize → click
```

over:

```text
scan → read → interpret → decide → click
```

Long operations must also be truthful about state.

Do **not** show:

- `FINISHED`;
- a full green progress bar;
- `COMPLETE`;

while final verification/publishing is still running.

QGIS internal metatile/work-unit counts must not be labeled as final raster tile counts.

---

## 16. Live desktop acceptance evidence

### Integrated Google Hybrid

- 23,119 tiles;
- Z8–Z18;
- Windows File Explorer size **3,560,735 KB**;
- elapsed **0:13:55**;
- ArcGIS Earth **PASS**.

### Advanced MBTiles → TPKX

- 271,497 tiles;
- 47 bundles;
- Z8–Z18;
- Windows File Explorer size **25,561,426 KB**;
- elapsed **0:17:59**;
- ArcGIS Earth **PASS**.

### Large Esri World / Google Labels

- 271,242 tiles;
- Z8–Z18;
- Windows File Explorer size **24,291,406 KB**;
- elapsed **2:51:52**;
- ArcGIS Earth **PASS**.

### v1.0 release smoke test

- `test2 small.tpkx`;
- Windows File Explorer size **12,852 KB**;
- elapsed **0:00:12**;
- ArcGIS Earth **PASS**.

---

## 17. Live field data

PRAVE → ArcGIS Earth Automation API is LIVE-PROVEN with units `7-101` through `7-106` and native fire-truck RSSI drawings.

Observed healthy state:

```text
UNITS=6
API_OK=47
API_BAD=0
BAD_RMC=0
BAD_PRAVE=0
RMC=FRESH
```

Forward inputs include PRAVE, F22, native GNSS/NMEA, QR, and KML/KMZ interoperability.

---

## 18. Do-not-regress rules

1. Do not return Google Earth Pro to primary-viewer status by inertia.
2. Do not present KML Super Overlay / Blooming Onion as the current basemap baseline.
3. Do not casually rewrite the frozen MBTiles→TPKX converter.
4. Do not discard MBTiles automatically when the operator selected MBTiles/Both or may need Map Fountain deployment.
5. Do not revive TPKX→MBTiles recovery as a production shortcut without solving and live-proving the visual defect.
6. Do not reintroduce removed beginner-facing extent/Grid-ID complexity merely for advanced users.
7. Keep advanced GIS freedom through existing-MBTiles → TPKX.
8. Retain KML for interoperability.
9. Preserve the no-operational-public-Internet-dependency rule.
10. Validate TPKX in the intended ArcGIS Earth target.
11. Validate mobile Map Fountain through actual service requests and visual navigation, not just a successful server start.
12. Do not market incidental multi-client behavior as a supported multi-user product.
13. Preserve **Offline GeoStack** as the master identity.

---

## 19. Known-good software baseline

- Windows 10/11 64-bit;
- Python 3.14.5;
- QGIS 3.44.9;
- ArcGIS Earth Windows;
- ArcGIS Earth Mobile Android.

The frozen core TPKX converter uses the Python standard library.

---

## 20. Engineering interpretation

The project is primarily interoperability engineering.

```text
QGIS already knew how to manufacture the raster pyramid.
ArcGIS Earth already knew how to display TPKX and WMTS.
The missing work was making the exact local bridges reliable and operator-usable.
```

That is the central architectural lesson of Offline GeoStack.
