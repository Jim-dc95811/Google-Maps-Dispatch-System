# Offline GeoStack — Historical Timeline

## Origin

The project began as an open terrestrial chartplotter / AVL concept for slow-moving wildland public-safety equipment. Early work used OpenCPN, NMEA/WPL-style positioning, custom radio transport, and QGIS-produced map content.

## Google Earth phase

The primary viewer moved to Google Earth Pro. That branch produced:

- direct raster MBTiles → KML Super Overlay conversion;
- KML forest / Blooming Onion deployment;
- custom local map utilities;
- large offline map-depot production;
- warm-cache recovery experiments;
- Network Earth local serving;
- packet-capture analysis;
- Google Earth Enterprise exploration.

The project learned how tile pyramids, KML Regions/LOD, caches, local serving, and offline viewer behavior actually worked.

## 2026 ArcGIS Earth pivot

ArcGIS Earth proved to provide a modern native fit for the original operational goals:

- native TPKX offline basemaps;
- KML/KMZ and NetworkLinks;
- 3D globe operation;
- GNSS/NMEA capability;
- local Automation API;
- native drawings/markers;
- session restoration.

The remaining interoperability problem was QGIS → TPKX.

## MBTiles → TPKX bridge

A custom Python converter was built from the published Esri TPKX / Compact Cache V2 structure. It preserves the QGIS-rendered raster tile bytes, flips TMS Y addressing to ArcGIS top-origin addressing, writes 128×128 Compact Cache V2 bundles and metadata, and packages the result as TPKX.

The standalone converter was live-proven in ArcGIS Earth and then integrated into the Factory.

## TPKX Map Factory

The integrated Factory matured through test versions v0.1.0 through v0.1.6. Major simplifications included:

- four frozen map-source choices;
- 96 DPI raster recipe;
- no Neighbor Extent tool in the normal public GUI;
- no Grid ID;
- no automatic filename scheme;
- manual decimal-degree GPS diagonal points;
- clean one-TPKX destination behavior;
- advanced existing-MBTiles → TPKX button;
- colored visual controls and progress indication.

## Live field integration moves to ArcGIS Earth

The `$PRAVE` display path was migrated to the ArcGIS Earth Automation API and live-proven with six controlled units, native labels, and the established fire-truck RSSI icon family. This established the broader architecture: protocol-specific input at the edge, normalized live state in the middle, and ArcGIS Earth as the native display/runtime.

## 2026-08-15 — v1.0 release acceptance

**TPKX Map Factory v1.0.0 was release accepted.**

The current map baseline became:

```text
QGIS → temporary MBTiles → TPKX → ArcGIS Earth
```

with a hard operational requirement that essential field/command behavior have no Internet dependency.

## 2026-08-15 — master project renamed Offline GeoStack

The original repository name, **Google Maps Dispatch System**, no longer described the system accurately. The project now spans map manufacturing, format interoperability, native offline ArcGIS Earth basemaps, GNSS, PRAVE, F22, QR, KML, and future live field integrations.

The master identity became:

# **Offline GeoStack**

**QGIS → TPKX → ArcGIS Earth + Live Field Positioning**

`TPKX Map Factory` remains the map-manufacturing subsystem. `ArcGIS Earth` remains the primary runtime. The older Google Earth naming is preserved as lineage rather than current branding.
