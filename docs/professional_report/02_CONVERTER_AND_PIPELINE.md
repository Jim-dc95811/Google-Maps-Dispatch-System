# Professional GIS Report — Part 2

## 6. Geographic Extent and Coordinate Handling

### 6.1 Three operator entry modes

| Mode | Operator input | Internal result |
| --- | --- | --- |
| Saved HOME EXTENT | EPSG:3857 order: xmin, xmax, ymin, ymax | Validated and normalized QGIS extent |
| Clipboard History | Two diagonal/opposite latitude, longitude points | Points parsed -> Web Mercator extent |
| Manual GPS points | Two diagonal/opposite latitude, longitude decimal-degree pairs | Points parsed -> Web Mercator extent |

The public UI intentionally calls manual coordinates “GPS coordinates” rather than exposing projection jargon to ordinary users. Either diagonal corner can be entered first; the program normalizes minima and maxima. A saved HOME EXTENT remains available for advanced/repeat production and uses the explicit QGIS-oriented order `xmin, xmax, ymin, ymax`. This order is shown directly in the GUI because it differs from the common `xmin, ymin, xmax, ymax` convention.

### 6.2 Web Mercator

The Factory operates on the standard Web Mercator tile pyramid (EPSG:3857 / Esri latestWkid 3857; wkid 102100 is also written in TPKX metadata for ArcGIS compatibility). The converter uses the standard Web Mercator latitude limit and LOD resolutions. The live v1.0.0 smoke-test package shows a `fullExtent` in EPSG:3857 and an item extent in EPSG:4326, demonstrating the two metadata representations used by the package.

## 7. Cartographic Source Handling and Layer Composition

The public v1.0.0 menu is intentionally frozen to four choices: Google Earth, Google Hybrid, Esri World, and Esri World / Google Labels. All expose operator-selected Z0-Z20. The Factory is not a generic source editor; it is a controlled production interface around approved QGIS projects.

### 7.1 Esri World / Google Labels blend

The preferred hybrid cartography is built in QGIS from Esri imagery beneath a Google labels-only layer. The QGIS project determines layer order and visual composition. The converter never needs to understand that the finished raster tile contains imagery plus labels: it receives already-rendered tile bytes. This is a crucial separation of responsibilities: QGIS owns cartographic semantics, the converter owns package mechanics.

### 7.2 Why this matters to advanced users

Any custom stack that QGIS can render into a compatible raster MBTiles can, in principle, use the advanced converter path. That means parcels, flood zones, roads, addresses, topographic overlays, forestry information, local annotations, historical maps, or other layers may be “baked” into the pixel pyramid before conversion. The TPKX does not need to know which upstream layers produced those pixels.

## 8. MBTiles as a Temporary Manufacturing Intermediate

MBTiles is used because it is a compact SQLite container for a tile pyramid and because QGIS natively produces it. The Factory expects a standard raster `tiles` table exposing `zoom_level`, `tile_column`, `tile_row`, and `tile_data`. The normal Factory additionally verifies PNG format, bounds metadata, represented zoom range, tile count, and the existence of a tile index before conversion.

```text
tiles:
  zoom_level   INTEGER
  tile_column  INTEGER
  tile_row     INTEGER
  tile_data    BLOB

metadata commonly includes:
  name
  format
  bounds
  minzoom
  maxzoom
```

The public product deliberately does not leave the intermediate MBTiles in the user-selected destination. QGIS projects, temporary MBTiles, converter work folders, QGIS logs, and partial outputs are created under Windows TEMP by the v1.0 pipeline and removed after success, failure, or cancellation. This is a product-design decision: the normal user asked for a TPKX, so the normal user receives a TPKX.

## 9. Custom MBTiles -> TPKX Converter: Technical Implementation

### 9.1 Input contract

- Raster Web Mercator MBTiles.
- 256 x 256 PNG or JPEG tiles.
- Standard `tiles` table containing `zoom_level`, `tile_column`, `tile_row`, `tile_data`.
- TMS-style MBTiles row convention handled by the converter.
- Vector tile / PBF / WebP inputs are rejected by v0.1.0.
- Input database is opened read-only during conversion.

### 9.2 Pixel preservation

The converter does not decode and re-render the source cartography. Each `tile_data` BLOB is read from SQLite and written to the Compact Cache V2 bundle as bytes. For the Factory’s PNG path, this preserves the QGIS-rendered image tile without introducing another cartographic rendering pass. This is why label size, color, source blending, antialiasing, and upstream layer appearance must be solved in QGIS, not in the converter.

### 9.3 TMS row conversion

MBTiles rows are treated as TMS bottom-origin. Esri Compact Cache rows are top-origin. For zoom level `z` and MBTiles `tile_row` `tms_y`, the converter computes:

```text
arcgis_y = (2 ** z - 1) - tms_y
```

The transformation is integer arithmetic. It does not round geographic coordinates or estimate tile placement. The tile column `x` is retained. After the row flip, the tile is assigned to the correct Compact Cache V2 bundle and row-major index position.

### 9.4 Web Mercator metadata and LOD table

The converter constructs a Web Mercator LOD table using a base resolution of `156543.03392804097` and halves the resolution for each zoom. It writes 256 x 256 tile dimensions, 96 DPI, the standard top-left Web Mercator origin, minimum and maximum LOD values matching the source MBTiles, and full/initial extents. Esri’s Compact Cache documentation states that resolution is the accurate map-coordinate conversion value and that scale/DPI are advisory display metadata.

### 9.5 TPKX package members

Esri’s open tile-package specification defines a TPKX as a compressed package containing `iteminfo.json`, `root.json`, a thumbnail, and a tile directory containing Compact Cache V2 bundle files organized by level of detail. The converter creates exactly this model.

```text
root.json
iteminfo.json
thumbnail.png
tile/
  L00/
    R0000C0000.bundle
  L01/
    ...
  L18/
    ...
```

## 10. Compact Cache V2 Binary Mechanics

Compact Cache V2 is where most of the converter’s exactness requirement lives. Esri documents the format specifically to allow programmers to read and write it. A bundle covers a 128 x 128 tile region: at most 16,384 tile slots. Tiles are located through an in-file index.

### 10.1 Bundle naming

```text
bundle_start_row = (row // 128) * 128
bundle_start_col = (col // 128) * 128
filename = R<row_hex>C<col_hex>.bundle
```

Rows and columns in bundle names are multiples of 128 and are encoded in hexadecimal. Example output from the live v1.0 smoke package includes `tile/L09/R0080C0080.bundle` and `tile/L18/R1a500C11680.bundle`. This matches the Esri naming rule.

### 10.2 Fixed header and index

| Field | Value / implementation |
| --- | --- |
| Header size | 64 bytes |
| Version | 3 |
| Record count | 16,384 |
| Offset byte count | 5 |
| Index size | 131,072 bytes (16,384 x 8) |
| Fixed bundle prefix | 131,136 bytes (header + index) |
| Packet size | 128 |
| Endianness | Little-endian |

### 10.3 Tile index position

```text
index_position = (row % 128) * 128 + (col % 128)
byte_offset_in_index = 8 * index_position
absolute_index_record_offset = 64 + byte_offset_in_index
```

Esri specifies row-major index order with top-left orientation. The converter follows that indexing rule exactly.

### 10.4 Combined offset/size record

Each 8-byte index entry combines a 40-bit tile offset and a 24-bit tile size. The converter stores the value as:

```text
index_value = tile_offset + (tile_size << 40)
```

Esri documents the reciprocal interpretation as `TileOffset = IDX mod 2^40` and `TileSize = floor(IDX / 2^40)`. The converter also retains the four-byte size prefix before each tile record for Compact Cache V2 compatibility.

## 11. Precision, Determinism, and “No Fudging” Audit

A specific project question was whether the conversion relied on approximations such as coordinate rounding, shortened pi values, or arbitrary geographic adjustments. The code audit found no `round()` call in the converter. Python `math.pi` is used in the Mercator calculations. Tile addressing and bundle placement are integer operations. Coordinate values used for package construction are standard Python double-precision floating-point values.

| Area | Behavior |
| --- | --- |
| Tile identity / zoom / column / row | Integer, deterministic |
| TMS -> top-origin row flip | Exact integer expression `(2^z - 1 - row)` |
| Bundle assignment | Integer division by 128 |
| Index slot | Modulo and integer arithmetic |
| Tile bytes | Copied; not re-rendered by converter |
| Mercator trigonometry | Python double precision using `math.pi` |
| Printed bounds | Formatted to 8 decimal places for console display only; unformatted values continue into metadata |
| DPI/scale constant | `INCHES_PER_METER = 39.37` affects scale metadata; not tile location |

The practical acceptance check is stronger than a theoretical code review alone: large converted packages aligned visually in ArcGIS Earth with no detectable offset, seam, scale mismatch, or progressive spatial drift. For this raster workflow, the converter’s relevant geographic addressing is deterministic and exact within normal floating-point metadata calculations.

## 12. Production Pipeline, Verification, and Cleanup

### 12.1 Normal build orchestration

`TPKX_PIPELINE.py` v1.0.0 creates a Windows TEMP work root, asks `DIRECT_MBTILES_ENGINE.py` to build `factory_intermediate.mbtiles`, invokes `MBTiles_to_TPKX_v0_1_0.py` as a subprocess, verifies the generated package, then publishes the final file to the user-selected destination. The converter itself is executed unchanged; the wrapper provides production hygiene around it.

### 12.2 TPKX structural verification

- Final package must exist and be non-empty.
- ZIP must contain `root.json`, `iteminfo.json`, and `thumbnail.png`.
- At least one `.bundle` must exist.
- `root.json` `storageInfo.storageFormat` must equal `esriMapCacheStorageModeCompactV2`.
- Reported `minLOD` and `maxLOD` must match the source MBTiles zoom range.
- The final published TPKX is re-inspected after it is moved to the selected destination.

### 12.3 Failure and cancellation behavior

The pipeline is designed to avoid leaving a misleading partial product. If conversion fails, any published output is removed. Temporary work roots are deleted in `finally` blocks, including read-only cleanup handling. Cancellation terminates the active child process tree. This behavior fixed earlier development builds in which disposable QGZ copies inherited read-only attributes and could remain in the destination directory.

### 12.4 Output rule

> **OUTPUT RULE**  
> The selected destination receives the finished `.tpkx` only. Temporary QGIS projects, MBTiles, logs, converter work directories, and partial outputs remain in Windows TEMP and are removed.

## 13. Advanced Existing-MBTiles Conversion Path

The advanced path was added after recognizing that the converter is valuable independently of the point-and-shoot Factory. A GIS professional can use a full custom QGIS project, produce raster MBTiles using any suitable workflow, then use the same GUI to convert the result to native TPKX. QGIS is not launched during this path.

The v0.1.6 advanced converter live completion processed 271,497 tiles, Z8-Z18, 47 Compact Cache V2 bundles, Windows File Explorer size 25,561,426 KB, elapsed 0:17:59. The advanced-converter output (`converter test`) opened directly in ArcGIS Earth. AE is the acceptance authority for the advanced path.

The advanced workflow reads the source MBTiles in read-only mode, checks the standard `tiles` schema, records min/max zoom and tile count, runs the stable converter into a TEMP output, verifies Compact Cache V2 structure and zoom range, then moves the verified TPKX to the selected destination. The input MBTiles is not intentionally modified.

## 14. Human-Factors GUI Design

The v1.0 GUI is intentionally not a generic GIS application. The target operator may not know what a tile pyramid, CRS, MBTiles database, Compact Cache, or `qgis_process` is. The interface therefore prioritizes recognition over textual decoding: source icons, clipboard icon, GPS target icon, build/factory icon, cancel icon, a visually distinct advanced-converter control, an always-visible progress bar, and a persistent status line.

### 14.1 “Snake-brain” navigation principle

A core UI lesson from live testing was that humans navigate interfaces faster by recognizing visual landmarks than by repeatedly parsing plain text. The v1.0 release therefore added color icons as functional navigation cues, not decoration. The public workflow is structured as three numbered tasks followed by one dominant build action.

### 14.2 Progress heartbeat

During the first large advanced conversion, tile progress appeared to freeze because the stable converter prints progress in 5,000-tile increments and expensive bundle/file operations can create long pauses between updates. The process was still healthy. v1.0 adds an independent one-second `WORKING` heartbeat/timer and an always-visible progress bar. Actual tile counts remain authoritative, while the heartbeat reassures the operator that the GUI event loop is alive.
