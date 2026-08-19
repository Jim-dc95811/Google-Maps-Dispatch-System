# Offline GeoStack — Technical FAQ

## What is Offline GeoStack?

A Windows-first offline geospatial stack that uses QGIS for cartographic rendering, raster MBTiles as the tile-pyramid handoff/master, a custom MBTiles → TPKX bridge for native packaging, and local field deployment that does not depend on the public Internet at showtime.

## What is the current Factory?

**Offline Map Factory 1.0** is the current clean Factory product line.

Status: **BUILT / SELF-TESTED — LIVE ACCEPTANCE PENDING**.

Current feature set:

- Google Earth;
- Google Hybrid;
- Esri World;
- Esri World / Google Labels;
- Z0–Z20;
- TPKX / MBTiles / Both;
- Advanced existing MBTiles → TPKX.

REST / Static WMTS output is not part of the current Factory.

## What happened to TPKX Map Factory v1.0.0?

It remains a separate **RELEASE-ACCEPTED / FROZEN historical milestone** from 2026-08-15.

The new product line reset the name and numbering rather than pretending the later REST experiments were still part of the finished operator product.

## Why QGIS?

QGIS already handles source access, projection, layer composition, labels, symbols, blending, rasterization, zoom-dependent rendering, and MBTiles generation.

The Factory uses QGIS as the rendering engine instead of rebuilding GIS behavior.

## Why MBTiles?

MBTiles contains the already-rendered raster pyramid.

Offline Map Factory 1.0 can:

- publish MBTiles directly;
- convert the same MBTiles to TPKX;
- publish Both.

If MBTiles is wanted downstream, preserve the direct QGIS-built MBTiles.

Reverse TPKX → MBTiles recovery was rejected as a production shortcut after real mobile visual defects.

## Does the converter rerender the imagery?

No. In the proven raster PNG/JPEG path, it preserves the existing tile image bytes and changes addressing/container structure.

Critical row conversion:

```text
y_arcgis = (2^z - 1) - y_tms
```

## Does QGIS natively create the TPKX used here?

Not in this workflow. QGIS creates raster MBTiles. Offline GeoStack supplies the Compact Cache V2 / TPKX packaging bridge.

## What is the Advanced Tool?

The clean Factory has exactly one Advanced Tool:

**existing MBTiles → TPKX**

A GIS professional can build custom raster MBTiles in QGIS and use only the packaging stage.

## What does the finished package look like?

```text
OFFLINE MAP FACTORY 1.0 - Installation Guide.pdf
OFFLINE MAP FACTORY 1.0 - User Guide.pdf
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
RUN OFFLINE MAP FACTORY.bat
System Files\
```

Internal support material stays behind `System Files` so the operator-facing root remains clean.

## Where do the QGZ files go?

```text
C:\Google Earth Project\QGIS\
```

with exact filenames:

```text
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
```

## What versions are pinned?

- QGIS 3.44.9
- Python 3.14.5
- PNG
- 96 DPI
- antialiasing ON
- metatile 4
- Z0–Z20

## What still needs to be proven for Offline Map Factory 1.0?

The new product line must pass a real Windows/QGIS acceptance run proving:

1. MBTiles-only;
2. TPKX-only;
3. Both;
4. Advanced MBTiles → TPKX;
5. produced TPKX opens/renders correctly in ArcGIS Earth;
6. cleanup and final-output behavior are correct.

Self-test success does not automatically equal RELEASE-ACCEPTED.

## What happened to REST / Static WMTS?

It worked as an engineering branch and taught useful lessons, but it is now **parked history**.

The v1.3/v1.4 experiments explored giant Static REST WMTS trees and compact `.restmap` transport seeds for Map Fountain.

Current decision: keep the history, leave REST out of Offline Map Factory 1.0, and reopen it only if a real target again requires it.

## What is the current personal-phone direction?

```text
Factory-built TPKX
→ microSD
→ Android
→ ArcGIS Field Maps / ArcGIS Earth
```

Current card-sizing work is measuring district Z17, county Z18, and selected State Forest/high-value Z20 products using real finished byte counts.

## Does ArcGIS Field Maps support TPKX on Android/microSD?

Esri documents sideloaded `.tpk` / `.tpkx` basemaps on Android device storage or SD card.

Offline GeoStack's own Field Maps + microSD acceptance test is still pending. Vendor documentation is not the same as project LIVE-PROVEN status.

## Why restrict Field Maps to Wi-Fi only?

The target audience may be using personal phones and data plans. Android app-level network controls can restrict Field Maps to Wi-Fi while leaving ordinary phone cellular service available.

## What happened to Map Fountain?

Map Fountain worked.

It live-proved:

1. native TPKX on router-attached SSD → SMB/Wi-Fi → ArcGIS Earth Windows;
2. Static REST WMTS on router-attached SSD → local HTTPS/Wi-Fi → ArcGIS Earth Mobile.

It is now **proven / parked**, not failed. It may return as Starlink-connected basecamp storage / poor-man's NAS.

## How large has the TPKX path been tested?

Among the live acceptance runs:

- 271,497-tile advanced existing-MBTiles conversion → ArcGIS Earth PASS;
- 271,242-tile Esri World / Google Labels Factory build → PASS;
- historical v1.0.0 smoke build → PASS;
- production-scale `ESG1N.tpkx` at **25,561,426 KB** in Windows File Explorer → opened directly from router-attached SMB storage over Wi-Fi → PASS.

## What is Persistent Geographic Context?

The operating condition where prepared map content, own position, roads/terrain, and surrounding spatial context remain present instead of being repeatedly requested from a public network service.

## What is PRAVE doing here?

PRAVE is one of the live remote-position inputs in the larger field system. PRAVE → ArcGIS Earth Automation API is LIVE-PROVEN with native drawings, labels, and the RSSI fire-truck icon family.

## What are the four repositories?

1. **Offline GeoStack** — master Factory / field-mapping project.
2. **Rasta Pyramid Factory** — giant-raster / deep-zoom manufacturing.
3. **Map Fountain** — proven router/storage delivery reference.
4. **Android Field Maps + ArcGIS Earth** — personal-phone / microSD deployment.

## Does Offline GeoStack require Internet access in the field?

No.

> **There can be no operational dependence on public Internet connectivity. Period.**

Online access may help manufacture or refresh maps. Essential prepared-map use must survive loss of outside connectivity.

## What does the MIT license cover?

Original Offline GeoStack code/documentation unless a file states otherwise. It does not grant rights to third-party imagery, labels, basemaps, vendor software, or external services.

## What should a future maintainer read first?

1. `README.md`
2. `ROADMAP.md`
3. `docs/PROJECT_STATUS_2026-08-18.md`
4. `docs/AI_CONTINUITY_RESTART_NOTE.md`
5. `docs/TECHNICAL_ARCHITECTURE.md`
6. `releases/README.md`
7. newest commits/issues
