# QGIS GeoTIFF Source Workflow — 2026-08-21

## Purpose

Create a georeferenced raster in QGIS that already looks exactly like the finished map, so ArcGIS Pro can build the native TPKX.

This document covers the **QGIS side only**.

## Production chain

```text
QGIS rendered map
-> GeoTIFF in EPSG:3857
-> ArcGIS Pro Create Map Tile Package
-> native TPKX
```

The GeoTIFF is one fixed-resolution master raster. ArcGIS Pro later creates the lower zoom levels.

---

## 1. Prepare the QGIS map

Open the QGIS project containing the map sources.

For the Esri Satellite + Google Labels workflow, the visible layer order must be:

```text
Google Labels      <- TOP
ESRI Satellite     <- BOTTOM
```

Both layers must be checked ON.

### Critical live-test lesson

Layer order matters during rasterization.

When `ESRI Satellite` was first/top in **Layers to render**, the imagery covered the labels in the generated GeoTIFF.

The successful order was:

```text
1. Google Labels
2. ESRI Satellite
```

Do not include `Annotations` unless intentionally required in the finished map.

---

## 2. Open Convert map to raster

Open:

```text
Processing
-> Toolbox
-> search: Convert map to raster
-> Raster tools
-> Convert map to raster
```

---

## 3. Set the extent

In **Minimum extent to render**, use the required map area in EPSG:3857.

For the small live test, QGIS used:

```text
-9146268.8731,-9144166.0472,3539208.9638,3540746.7555 [EPSG:3857]
```

Production uses the actual requested area.

---

## 4. Choose source detail

Set **Map units per pixel** from this table:

| Target detail | Map units per pixel |
| ---: | ---: |
| Z16 | `2.38865713397468` |
| Z17 | `1.19432856685505` |
| Z18 | `0.597164283559817` |
| Z19 | `0.298582141647617` |
| Z20 | `0.149291070823808325` |

QGIS may display the value rounded in the GUI.

Examples:

```text
District Z17 -> 1.19432856685505
Small Z18 test -> 0.597164283559817
Selected high-detail Z20 -> 0.149291070823808325
```

ArcGIS Pro **Maximum Level Of Detail** should later match the target detail chosen here.

---

## 5. Remaining raster settings

Use:

```text
Tile size = 1024
Buffer around tiles = 0
Make background transparent = unchecked
Map theme to render = Not selected
```

---

## 6. Select Layers to render

Select exactly the intended source stack.

For Esri imagery + Google labels:

```text
Google Labels
ESRI Satellite
```

The list order must keep labels first/top.

Do not use Select All when unwanted layers are present.

---

## 7. Choose output

Set **Output layer** to a permanent `.tif` file.

Example:

```text
C:\A\qgis tif test.tif
```

Overwriting an earlier test TIFF is acceptable when intentional.

Leave **Open output file after running algorithm** checked if desired.

---

## 8. Run and verify

Click **Run**.

Do not proceed to ArcGIS Pro until the GeoTIFF itself visibly contains the intended finished cartography.

Verify:

- imagery present;
- labels present;
- labels not hidden beneath imagery;
- georeferencing is EPSG:3857.

### Proven small result

```text
GeoTIFF
37,767,543 bytes
4096 x 3072 RGB
EPSG:3857
Z18 source detail
0.597164283559817 meters/pixel
```

---

## District 7 current production recipe

A live District 7 manual build was started with:

```text
Esri Satellite + Google Labels
Z17
map units per pixel = 1.19432856685505
```

Completion and final size remain pending until QGIS actually finishes.

---

## GeoTIFF Factory automation

The manual workflow above is now being automated in the separate:

```text
GEOTIFF FACTORY 0.1.2 TEST
```

The Factory keeps the established two-point extent workflow, four controlled source choices and Z16-Z20 selection, but outputs only a finished `.tif`.

It deliberately contains:

- no MBTiles production path;
- no TPKX converter;
- no recovery tools.

The GeoTIFF Factory live Windows/QGIS acceptance is pending.

See `src/geotiff_factory/README.md`.

---

## Current production direction

For Field Maps:

```text
QGIS / GeoTIFF Factory
-> GeoTIFF
-> ArcGIS Pro
-> native TPKX
-> Field Maps
```

The custom MBTiles -> TPKX converter remains research rather than the production route.
