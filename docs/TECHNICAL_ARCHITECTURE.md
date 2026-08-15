# TPKX Map Factory / ArcGIS Earth Technical Architecture

## Purpose

This document records the current 2026 GIS architecture of the Google Maps Dispatch System after its migration from a Google Earth Pro / KML Super Overlay baseline to **ArcGIS Earth + native TPKX**.

It is intended for GIS professionals, software engineers, and future AI systems that need enough detail to reconstruct the actual data path rather than treating the Factory as a black box.

---

## 1. Architectural summary

The production chain is:

```text
Source imagery / QGIS layer stack
        ↓
QGIS 3.44.9 rendering engine
        ↓
Raster tile pyramid in MBTiles
        ↓
Custom Python MBTiles → TPKX converter
        ↓
Esri Compact Cache V2 bundles
        ↓
TPKX package
        ↓
ArcGIS Earth
```

The normal operator sees only a simplified GUI. QGIS performs cartographic rendering. The converter performs format/address translation and packaging. The finished operator deliverable is a single `.tpkx` file.

---

## 2. Why QGIS remains the rendering engine

QGIS already solves the difficult GIS work:

- reprojection
- raster and vector layer compositing
- label rendering
- antialiasing
- source access
- zoom-dependent cartography
- tile-pyramid generation
- MBTiles output

Reimplementing these functions would add risk without adding value. The Factory therefore treats QGIS as a rendering engine instead of attempting to become a GIS engine.

Current normal Factory render recipe:

- QGIS 3.44.9
- Web Mercator tile scheme / EPSG:3857
- PNG raster tiles
- 96 DPI
- antialiasing ON
- metatile 4
- operator-selectable Z0–Z20

---

## 3. MBTiles as manufacturing intermediate

MBTiles is SQLite-based and exposes the raster pyramid in a simple schema. The converter expects a standard raster MBTiles `tiles` table containing:

```text
zoom_level
tile_column
tile_row
tile_data
```

`tile_data` contains the already-rendered PNG or JPEG bytes.

In the normal Factory workflow, MBTiles is **not the public/operator deliverable**. It is a temporary manufacturing intermediate between QGIS and TPKX and is cleaned after successful packaging.

Advanced GIS users may intentionally provide their own raster MBTiles directly to the converter path.

---

## 4. The MBTiles → TPKX interoperability problem

The key interoperability gap was straightforward:

- QGIS can create raster MBTiles.
- ArcGIS Earth natively consumes TPKX.
- There was no simple public bridge in the required direction for this workflow.

The custom converter implements the published TPKX / Compact Cache V2 structure.

It does **not** rerender the map.

It does **not** flatten zoom levels into a new raster.

It does **not** resample the tile imagery.

It preserves the existing tile image bytes and changes the addressing/container structure around them.

---

## 5. TMS row conversion

Raster MBTiles commonly stores rows using TMS bottom-origin Y addressing. ArcGIS compact cache addressing is top-origin.

For each tile at zoom `z`:

```text
y_arcgis = (2^z - 1) - y_tms
```

`x` remains the tile column.

This conversion is integer math and deterministic.

---

## 6. Compact Cache V2 bundle structure

The converter uses Esri Compact Cache V2 with a packet size of 128.

Each bundle therefore represents:

```text
128 × 128 = 16,384 possible tile positions
```

For a converted ArcGIS row/column:

```text
bundle_row = floor(row / 128) × 128
bundle_col = floor(col / 128) × 128
```

The tile position inside a bundle is:

```text
index = (row mod 128) × 128 + (col mod 128)
```

Bundle files are named from the starting row and column of the packet and grouped by zoom level.

The converter writes the Compact Cache V2 binary header, fixed index area, tile-length records, tile bytes, and packed index entries expected by the format.

---

## 7. Tile-byte preservation

The converter reads `tile_data` from SQLite and writes those bytes directly into the Compact Cache V2 bundle.

For PNG/JPEG raster MBTiles, the conversion stage therefore preserves the cartography created by QGIS.

This is important because each QGIS zoom level may contain independent label placement, road hierarchy, annotation, and raster detail. The converter does not reinterpret these pixels.

A useful mental model is:

> QGIS creates the pixels. The converter files the pixels into the cabinet ArcGIS Earth understands.

---

## 8. Coordinate and precision behavior

No application-level rounding is used for tile placement.

Critical addressing uses integer math. Web Mercator metadata uses normal double-precision floating-point calculations and Python's `math.pi`.

The converter may format coordinates to a fixed number of decimal places for human-readable console/status output, but those display strings are not fed back into the packaged coordinate values.

The important distinction is:

- **display formatting** may be rounded for readability;
- **tile placement and package construction** are not rounded to a simplified decimal grid.

---

## 9. Package metadata

The converter creates the TPKX support structure expected around the bundle files, including:

- `root.json`
- `iteminfo.json`
- `thumbnail.png`
- `tile/Lxx/*.bundle`

The root metadata identifies the Web Mercator spatial reference, tile dimensions, DPI, origin, LOD table, minimum and maximum LOD, extents, and Compact Cache V2 storage mode.

The package is then written as a ZIP64-compatible `.tpkx`.

Metadata such as package GUID and creation time can legitimately differ between two conversions of the same MBTiles. Therefore byte-for-byte package identity is not the acceptance rule.

---

## 10. Verification and acceptance philosophy

The converter performs structural checks, but the project deliberately uses **ArcGIS Earth as the final acceptance authority**.

A finished TPKX is accepted when ArcGIS Earth:

- opens it without complaint;
- places it in the correct geographic location;
- exposes the expected zoom behavior;
- renders the expected imagery/cartography;
- behaves normally during navigation.

This matters more operationally than two TPKX files having identical archive bytes.

---

## 11. Factory v1.0.0 workflows

### Normal operator path

```text
1. Choose map source
2. Choose map area
3. Choose zoom range
4. BUILD TPKX MAP
5. Save .tpkx
6. Open in ArcGIS Earth
```

The operator can define the map area in three ways:

1. Paste a prepared QGIS-style HOME EXTENT.
2. Load two diagonal coordinate pairs from Windows Clipboard History.
3. Enter two diagonal GPS decimal-degree coordinate pairs manually.

Manual GPS input uses ordinary:

```text
Latitude, Longitude
```

The Factory normalizes corner order and converts internally to the EPSG:3857 extent required by QGIS.

The direct HOME EXTENT field uses the project’s visible order:

```text
xmin, xmax, ymin, ymax
```

### Advanced GIS path

```text
Existing raster MBTiles
        ↓
ADVANCED: MBTILES → TPKX
        ↓
TPKX
        ↓
ArcGIS Earth
```

This path is intentionally simple. It does not ask for source, extent, or zoom because those properties already exist in the MBTiles.

It enables a GIS professional to perform all cartographic composition in QGIS and use the Factory only as the TPKX packaging bridge.

---

## 12. Source recipes

The v1.0.0 GUI exposes four frozen source choices:

1. Google Earth
2. Google Hybrid
3. Esri World
4. Esri World / Google Labels

The Esri World / Google Labels choice is a QGIS-rendered two-layer composition:

```text
Google labels-only layer
        over
Esri World Imagery
```

QGIS renders the composite pixels before MBTiles creation. The converter remains layer-agnostic.

This architecture is deliberately extensible: any raster result QGIS can legitimately render into suitable MBTiles can be fed to the advanced converter.

Source-data licensing, caching, export, attribution, and redistribution rules remain source-specific and are outside the binary-format conversion itself.

---

## 13. Temporary data and destination cleanliness

The public Factory design requires the user-selected destination to receive only the final `.tpkx` product.

Temporary QGIS projects, temporary MBTiles, work directories, and converter support material belong in temporary workspace and are cleaned after success.

The intent is appliance-like behavior:

```text
operator selects destination
        ↓
Factory works elsewhere
        ↓
destination receives one finished TPKX
```

This prevents intermediate manufacturing artifacts from being mistaken for operator deliverables.

---

## 14. Human factors / GUI design

The v1.0.0 GUI intentionally uses colored icons and strong visual landmarks.

The design goal is:

```text
see → recognize → click
```

instead of:

```text
scan → read → interpret → decide → click
```

This matters because the target audience includes ordinary operators who should not have to become GIS technicians to manufacture a map.

The advanced converter remains visible but visually separated so advanced power does not contaminate beginner simplicity.

---

## 15. Live acceptance evidence

### Integrated Google Hybrid proof

- Area: 113.31 sq mi
- Zooms: Z8–Z18
- Tiles: 23,119
- Windows File Explorer size: 3,560,735 KB
- Elapsed: 0:13:55
- ArcGIS Earth: PASS

### Advanced MBTiles → TPKX proof

- Tiles: 271,497
- Bundles: 47
- Zooms: Z8–Z18
- Windows File Explorer size: 25,561,426 KB
- Elapsed: 0:17:59
- ArcGIS Earth: PASS

### Large Esri World / Google Labels Factory proof

- Approximate area: 1,378.89 sq mi
- Tiles: 271,242
- Zooms: Z8–Z18
- Windows File Explorer size: 24,291,406 KB
- Elapsed: 2:51:52
- ArcGIS Earth: PASS

### v1.0.0 release smoke test

- Area: approximately 0.12 sq mi
- Input method: two manual decimal-degree GPS diagonal points
- Output: `test2 small.tpkx`
- Windows File Explorer size reported by Factory: 12,852 KB
- Elapsed: 0:00:12
- ArcGIS Earth: PASS

---

## 16. ArcGIS Earth operational role

ArcGIS Earth is now the project’s primary 2026 viewer.

Relevant capabilities observed or proven in this project include:

- native local TPKX display;
- KML/KMZ support;
- KML NetworkLinks;
- 3D globe navigation;
- local Automation API;
- native drawing/marker display;
- GNSS/NMEA capability;
- session restoration of previously loaded TPKX files;
- online driving directions when connectivity exists.

Internet-dependent conveniences are treated as optional enhancements.

---

## 17. Hard offline rule

The project has one non-negotiable operational requirement:

> **There can be no operational dependence on Internet connectivity. Period.**

The Internet may be used during map manufacturing and refresh cycles. At incident/showtime, the command system must continue to perform essential functions with Internet connectivity absent.

This requirement applies to core map viewing, the command picture, and other essential incident functions.

---

## 18. Persistent Geographic Awareness

The phrase **Persistent Geographic Awareness** emerged from the operational design.

It describes a state in which position, surroundings, routes, terrain, and local context remain continuously visible without the operator repeatedly requesting them from a network service.

With a large screen, local high-resolution TPKX imagery, and own-position GNSS, the operator moves from:

```text
"I am at this coordinate."
```

to:

```text
"I am on this road, in this forest, inside this terrain, with this context around me."
```

This is particularly important for command, wildfire, forestry, utility, delivery, rural access, and other field operations where mobile connectivity cannot be assumed.

---

## 19. PRAVE and live data

The project’s `$PRAVE` path has been migrated from Google Earth-oriented output to a live-proven ArcGIS Earth Automation API implementation.

A controlled test displayed units `7-101` through `7-106` in ArcGIS Earth using native drawings and the established fire-truck RSSI icon family.

Observed healthy test state included:

```text
UNITS=6
API_OK=47
API_BAD=0
BAD_RMC=0
BAD_PRAVE=0
RMC=FRESH
```

The forward architecture is protocol-specific decoding at the edge followed by normalization into one ArcGIS Earth live-position manager.

KML remains available where interoperability, persistence, or external feeds make KML the correct tool.

---

## 20. Planned / continuing live inputs

- `$PRAVE`
- F22
- native GNSS/NMEA
- QR dispatch coordinates and bounded commands
- KML/KMZ / NetworkLinks where appropriate

The project does not require every live transport to be forced through KML merely because the original Google Earth architecture did so.

---

## 21. Legacy lineage

Earlier project branches solved real problems and remain technically valuable:

- MBTiles production in QGIS
- direct MBTiles → KML Super Overlay conversion
- KML Blooming Onion deployment
- large map-depot design
- warm-cache recovery experiments
- Network Earth local serving
- Wireshark/PCAP diagnostics
- Google Earth Enterprise exploration

These efforts provided the tile-pyramid, cache, KML, network, and deployment understanding that made the TPKX/ArcGIS Earth pivot rapid.

They should be preserved as history but not presented as the current baseline.

---

## 22. Do-not-regress rules

1. Do not return Google Earth Pro to primary-viewer status by inertia.
2. Do not require a local KML/PNG server when native TPKX solves the basemap problem.
3. Do not make temporary MBTiles a normal public deliverable.
4. Do not casually rewrite the proven converter without a verified defect.
5. Do not add persistent logs/work folders to the user’s chosen TPKX destination.
6. Do not reintroduce removed beginner-facing complexity merely for advanced users.
7. Keep advanced GIS freedom through the existing-MBTiles converter path.
8. Retain KML for interoperability rather than discarding it.
9. Preserve the no-operational-Internet-dependency rule.
10. Validate finished map packages in ArcGIS Earth.

---

## 23. Known-good software baseline

- Windows 10/11 64-bit
- Python 3.14.5
- QGIS 3.44.9
- ArcGIS Earth

No additional Python libraries are required by the core TPKX converter path; it uses the Python standard library.

---

## 24. Engineering interpretation

The important technical achievement is not a new raster renderer or a new globe.

It is interoperability:

```text
QGIS already knew how to manufacture the map.
ArcGIS Earth already knew how to display the finished package.
The missing component was the exact deterministic bridge between them.
```

The converter is therefore small relative to the systems it connects, but its value lies in the exact ordering of bytes, rows, indexes, metadata, and package structure.

That is the central architectural lesson of this project.
