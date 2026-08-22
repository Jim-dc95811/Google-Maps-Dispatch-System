# QGIS GeoTIFF Source Workflow — 2026-08-21

## Purpose

Create a georeferenced raster in QGIS that already looks exactly like the finished map, so ArcGIS Pro can build the native TPKX.

This document covers the **QGIS side only**.

## Proven test configuration

```text
QGIS project CRS: EPSG:3857
Output raster: GeoTIFF (.tif)
Raster content: rendered satellite imagery + rendered labels
Test maximum detail: Web Mercator Z18
Map units per pixel: 0.597164283559817
Tile size: 1024
Background transparency: OFF
```

## 1. Prepare the QGIS map

Open the QGIS project containing the map sources.

For the Esri Satellite + Google Labels test, the visible layer order must be:

```text
Google Labels      <- TOP
ESRI Satellite     <- BOTTOM
```

Both layers must be checked ON in the Layers panel.

### Critical lesson

Layer order matters during rasterization.

When `ESRI Satellite` was placed ahead of `Google Labels` in the **Layers to render** list, the satellite imagery covered the labels in the generated GeoTIFF.

The successful order was:

```text
1. Google Labels
2. ESRI Satellite
```

Do not include the `Annotations` layer unless it is intentionally part of the finished map.

## 2. Open Convert map to raster

Open:

```text
Processing
-> Toolbox
-> search: Convert map to raster
-> Raster tools
-> Convert map to raster
```

## 3. Set the map extent

In **Minimum extent to render**, use the desired map area.

For the live small-area test, QGIS used:

```text
-9146268.8731,-9144166.0472,3539208.9638,3540746.7555 [EPSG:3857]
```

For production, substitute the actual required area.

## 4. Set raster resolution

For the Z18 test:

```text
Map units per pixel = 0.597164283559817
```

QGIS may display this rounded as:

```text
0.597164
```

This is the standard Web Mercator Z18 resolution used for the test.

## 5. Set raster tile size

Use:

```text
Tile size = 1024
```

Leave:

```text
Buffer around tiles = 0
Make background transparent = unchecked
Map theme to render = Not selected
```

## 6. Select the layers to render

Open **Layers to render** and select exactly:

```text
Google Labels
ESRI Satellite
```

The list order must be:

```text
Google Labels
ESRI Satellite
```

Do not use `Select All` if unwanted layers such as `Annotations` are present.

## 7. Choose the output GeoTIFF

Set **Output layer** to a permanent `.tif` file, for example:

```text
C:\A\qgis tif test.tif
```

It is acceptable to overwrite an earlier test TIFF.

Leave:

```text
Open output file after running algorithm = checked
```

## 8. Run

Click **Run**.

The resulting GeoTIFF should visually contain both:

- the satellite imagery;
- the street/place labels.

## 9. Verify the finished GeoTIFF before leaving QGIS

Do not proceed to ArcGIS Pro until the GeoTIFF itself already looks like the finished map.

For the live successful test, the GeoTIFF was:

```text
GeoTIFF
EPSG:3857
RGB
4096 x 3072 pixels
0.597164283559817 meters/pixel
```

The labels were visibly baked into the image.

## What the GeoTIFF is

The GeoTIFF is one georeferenced, fixed-resolution raster image. It is not yet the multilevel tile pyramid.

ArcGIS Pro performs the next stage:

```text
QGIS GeoTIFF
-> ArcGIS Pro Create Map Tile Package
-> native TPKX
```

## Current production direction

For Field Maps compatibility, use:

```text
QGIS -> GeoTIFF -> ArcGIS Pro -> TPKX
```

The custom MBTiles -> TPKX converter remains experimental and is not the production path at this point.
