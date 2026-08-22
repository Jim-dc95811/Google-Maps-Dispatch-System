# ArcGIS Pro GeoTIFF -> Native TPKX Workflow — 2026-08-21

## Purpose

Convert a finished QGIS GeoTIFF into a native ArcGIS Pro TPKX for the Field Maps production path.

This document covers the ArcGIS Pro side only.

## Input contract

The GeoTIFF should already contain the final rendered cartography.

For the proven Esri hybrid test:

```text
Google Labels above ESRI Satellite
EPSG:3857
RGB GeoTIFF
```

ArcGIS Pro is not expected to recreate the QGIS labels. They are already baked into the raster.

---

## 1. Start a clean ArcGIS Pro Map project

Create a new **Map** project.

Add the GeoTIFF with:

```text
Map -> Add Data
```

If ArcGIS Pro asks to calculate raster statistics, choose **Yes**. The statistics support display/contrast and do not change the georeferencing or source pixels.

Verify the GeoTIFF visibly contains both imagery and labels before proceeding.

---

## 2. Remove default ArcGIS basemap layers

Open the **Contents** pane from the View tab.

Remove or uncheck:

- World Topographic Map;
- World Hillshade.

Leave only the GeoTIFF in the map for this production workflow.

---

## 3. Open Create Map Tile Package

Open:

```text
Analysis
-> Geoprocessing / Tools
-> Find Tools
-> Create Map Tile Package
```

On the live interface, Tools is represented by the small red toolbox icon in the Analysis ribbon.

---

## 4. Set Create Map Tile Package parameters

Use:

```text
Input Map: Map
Package for ArcGIS Online | Bing Maps | Google Maps: checked
Create Multiple Packages: unchecked
Tiling Format: PNG 24 bit
Minimum Level Of Detail: 0
Maximum Level Of Detail: match the source GeoTIFF target detail
Extent: use the GeoTIFF layer extent
Area of Interest: blank for the standard rectangular build
Output File: desired .tpkx path
```

Summary may contain a short description. Tags are optional.

### Source detail -> ArcGIS Pro maximum LOD

| QGIS source detail | ArcGIS Pro Maximum Level Of Detail |
| ---: | ---: |
| Z16 | 16 |
| Z17 | 17 |
| Z18 | 18 |
| Z19 | 19 |
| Z20 | 20 |

The production rule is simple: **the Pro maximum LOD matches the GeoTIFF source detail.**

---

## 5. Run

Click **Run**.

ArcGIS Pro creates the lower zoom levels and writes the native TPKX / Compact Cache V2 package.

---

## Proven small build

Input GeoTIFF:

```text
37,767,543 bytes
4096 x 3072 RGB
EPSG:3857
Z18 source resolution
```

Output:

```text
tiff test 66.tpkx
38,306,245 bytes
Z0-Z18
PNG24
19 Compact Cache V2 bundles
creator: CreateMapTilePackage ArcGIS Pro
```

The TPKX is only about 539 KB larger than the one-resolution source GeoTIFF in this small test while adding the complete Z0-Z18 tile pyramid.

---

## Native package observations

Direct inspection of the ArcGIS Pro-generated package showed:

```text
spatialReference: wkid 102100 / latestWkid 3857
storageFormat: esriMapCacheStorageModeCompactV2
packetSize: 128
tileImageInfo format: PNG24
```

`iteminfo.json` includes:

```text
creator: CreateMapTilePackage ArcGIS Pro
type: Compact Tile Package
typeKeywords: Compact Tile Package, Tile Package, tpkx
```

The native package also contains a real `Raster Layer` description for the source TIFF in `root.json.layers`.

Important forensic correction: this ArcGIS Pro-produced TPKX does **not** contain explicit ZIP directory records. Therefore explicit `tile/` / `tile/Lxx/` ZIP directory entries are not a universal requirement for a native TPKX.

---

## Field Maps acceptance state

The ArcGIS Pro build itself is proven.

Field Maps runtime acceptance is still pending until the native Pro-created TPKX is copied to the physical-card `basemaps` directory, Designer is set to the exact filename, and Field Maps opens it successfully.

Do not call this branch Field Maps LIVE-PROVEN before that vote.

---

## Production chain

```text
QGIS GeoTIFF
-> ArcGIS Pro Create Map Tile Package
-> native TPKX
-> physical removable storage
-> Field Maps
```

> **QGIS owns the finished pixels. ArcGIS Pro owns the native TPKX package. Field Maps owns acceptance.**
