# Offline GeoStack — TPKX Map Factory v1.0.0 Release Notes

**Release status: LIVE-PROVEN / RELEASE-ACCEPTED**

Date: 2026-08-15

## Compatibility notice added 2026-08-20

This release remains fully accepted for the target actually tested at release time: **Factory manufacture + ArcGIS Earth rendering**.

A later strict ArcGIS Field Maps control test exposed a compatibility defect in the historical MBTiles -> TPKX converter lineage. Field Maps rejected a project-converter TPKX while accepting Esri's official `Usa.tpkx` through the same physical-card/Designer workflow.

Therefore:

- do **not** revoke or rewrite this historical release;
- do **not** describe v1.0.0 output as Field Maps-conformant;
- repair belongs in a new converter/product lineage;
- the exact accepted v1.0.0 archive remains frozen.

See `../docs/TPKX_FIELD_MAPS_CONFORMANCE_2026-08-20.md`.

---

`TPKX Map Factory v1.0.0` is the first release-accepted map-manufacturing baseline inside **Offline GeoStack**.

Master project identity:

**Offline GeoStack — QGIS → TPKX → ArcGIS Earth + Live Field Positioning**

## What v1.0.0 does

The Factory provides two workflows from one Windows GUI.

### Build a TPKX map from a supported Factory source

```text
Choose source
   ↓
Choose map area
   ↓
Choose zoom range
   ↓
QGIS renders temporary MBTiles
   ↓
historical converter builds TPKX
   ↓
operator receives one .tpkx
```

### Convert an existing raster MBTiles

```text
Existing MBTiles
   ↓
ADVANCED: MBTILES → TPKX
   ↓
TPKX proven on ArcGIS Earth
```

The advanced path is intended for QGIS/GIS users who want to create their own layer stack and use the Factory only as the TPKX packaging bridge.

## Frozen v1.0.0 map recipe

- QGIS 3.44.9
- Python 3.14.5 established known-good
- PNG
- 96 DPI
- antialiasing ON
- metatile 4
- zoom range Z0–Z20

## Factory sources

- Google Earth
- Google Hybrid
- Esri World
- Esri World / Google Labels

Source-data licensing/export/caching rules are source-specific. The Factory is a format and workflow tool; users are responsible for permitted use of source data.

## Map-area input

The normal workflow supports:

- pasted HOME EXTENT
- two diagonal points from Windows Clipboard History
- two manually entered diagonal GPS coordinate pairs in decimal degrees

The Factory normalizes the two corners and converts GPS coordinates internally to the EPSG:3857 extent used by QGIS.

## Human-interface changes in the release build

v1.0.0 freezes the proven v0.1.6 mechanics and adds the public-facing GUI treatment:

- colored map-source icons
- clear map-area icons
- large visual BUILD control
- visually separated advanced converter
- progress bar
- explicit completion state
- activity indication for long-running work

## Proven acceptance results

### Large advanced MBTiles conversion

- Tiles: 271,497
- Bundles: 47
- Zooms: Z8–Z18
- Windows File Explorer size: 25,561,426 KB
- Elapsed: 0:17:59
- ArcGIS Earth: PASS

### Large Esri World / Google Labels Factory run

- Area: approximately 1,378.89 sq mi
- Tiles: 271,242
- Zooms: Z8–Z18
- Windows File Explorer size: 24,291,406 KB
- Elapsed: 2:51:52
- ArcGIS Earth: PASS

### v1.0.0 release smoke test

- Area: approximately 0.12 sq mi
- Input: two manual decimal-degree GPS diagonal points
- Output: `test2 small.tpkx`
- Windows File Explorer size reported by Factory: 12,852 KB
- Elapsed: 0:00:12
- ArcGIS Earth: PASS

## Binary-release status

The exact release-accepted Windows archive is named:

`TPKX_MAP_FACTORY_v1_0_0.zip`

It remains preserved in the canonical project archive. During the GitHub repository rebuild, the available connector truncated the binary archive when transmitting it. The bad public copy was removed rather than being left in place. The exact accepted ZIP should be attached directly to GitHub before public binary distribution.

## Release rule

v1.0.0 is feature-frozen.

New features and verified converter repairs belong in later/new product lines. Do not alter the accepted v1.0.0 binary and call it the same release.

## Operational doctrine

> **There can be no operational dependence on Internet connectivity. Period.**

Internet connectivity may be used during map preparation or for optional enhancements, but essential field/command use must not depend on cellular coverage, a hotspot, or a live map service.

## Project authorship

Developed and published by **Jim Gaddy** with **ChatGPT / Tool Master** serving as technical design, coding, GIS research, documentation, packaging, and diagnostic partner.
