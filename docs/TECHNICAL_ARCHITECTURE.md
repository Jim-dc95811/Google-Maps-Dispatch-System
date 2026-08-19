# Offline GeoStack — Technical Architecture

## Purpose

This document records the current Offline GeoStack architecture after the product-line cleanup that created **Offline Map Factory 1.0**.

Master identity:

**Offline GeoStack — QGIS → MBTiles / TPKX → offline field deployment + live field positioning**

---

## 1. Current architectural summary

```text
MAP MANUFACTURING
source imagery / QGIS layer stack
        ↓
Offline Map Factory 1.0
        ↓
QGIS 3.44.9 rendering engine
        ↓
verified raster MBTiles
        ↓
        ├─→ publish MBTiles
        └─→ proven Compact Cache V2 converter → native TPKX

PERSONAL MOBILE DEPLOYMENT
native TPKX
        ↓
microSD
        ↓
Android
        ↓
ArcGIS Field Maps / ArcGIS Earth

LIVE FIELD INPUTS
GNSS / PRAVE / F22 / QR / KML
        ↓
ArcGIS Earth native inputs / Automation API
```

No public Internet connection is required for prepared local-map display.

---

## 2. Offline Map Factory 1.0 contract

Current normal operator capability:

- Google Earth;
- Google Hybrid;
- Esri World;
- Esri World / Google Labels;
- area from HOME EXTENT, Clipboard History diagonal points, or two manual GPS points;
- Z0–Z20;
- output: TPKX / MBTiles / Both;
- one Advanced Tool: existing MBTiles → TPKX.

REST / Static WMTS is not part of the current Factory.

Current status: **BUILT / SELF-TESTED — LIVE ACCEPTANCE PENDING**.

---

## 3. Why QGIS remains the rendering engine

QGIS already solves:

- projection/reprojection;
- source access;
- layer composition;
- labels/symbology;
- antialiasing;
- zoom-dependent rendering;
- tile-pyramid generation;
- MBTiles output.

Offline Map Factory uses QGIS as the rendering engine rather than rebuilding GIS behavior.

Known-good render baseline:

- QGIS 3.44.9;
- EPSG:3857 / Web Mercator tile scheme;
- PNG;
- 96 DPI;
- antialiasing ON;
- metatile 4;
- Z0–Z20.

---

## 4. MBTiles and TPKX roles

MBTiles contains the already-rendered raster pyramid.

The forward converter changes addressing/container structure without rerendering the map:

```text
MBTiles raster tiles
→ TMS row conversion
→ Compact Cache V2 bundles/indexes
→ native .tpkx
```

Critical row conversion:

```text
y_arcgis = (2^z - 1) - y_tms
```

Production rule:

- preserve direct QGIS-built MBTiles when MBTiles is wanted;
- use the proven forward MBTiles → TPKX converter for TPKX;
- do not use reverse TPKX → MBTiles recovery as a production shortcut.

---

## 5. Factory product lineage

### Historical TPKX Map Factory v1.0.0

**RELEASE-ACCEPTED / FROZEN — 2026-08-15**.

It established the four-source QGIS workflow, Z0–Z20 manufacturing, the custom converter, advanced existing-MBTiles conversion, and ArcGIS Earth acceptance.

Preserve that record exactly as history.

### Offline Map Factory 1.0

New clean product line with reset numbering.

Current status: **BUILT / SELF-TESTED — LIVE ACCEPTANCE PENDING**.

The live gate must separately prove:

- MBTiles-only;
- TPKX-only;
- Both;
- Advanced MBTiles → TPKX;
- ArcGIS Earth acceptance of the produced TPKX;
- cleanup/finalization behavior.

### REST / Static WMTS experiments

The v1.3/v1.4 REST branches are **PARKED ENGINEERING HISTORY**.

They produced useful lessons around large directory trees, packaging overhead, Static REST WMTS, and `.restmap` transport seeds, but they do not define the current Factory.

---

## 6. Finished-package architecture

User-facing top level:

```text
OFFLINE MAP FACTORY 1.0 - Installation Guide.pdf
OFFLINE MAP FACTORY 1.0 - User Guide.pdf
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
RUN OFFLINE MAP FACTORY.bat
System Files\
```

Internal implementation/support files belong behind `System Files`.

Required QGIS project placement:

```text
C:\Google Earth Project\QGIS\
```

with exact filenames:

```text
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
```

This separation is deliberate human-factors engineering: the operator sees only what the operator needs.

---

## 7. Personal Android deployment

Preferred normal-user path:

```text
TPKX
→ microSD
→ Android
→ map application
```

### ArcGIS Earth Mobile

Local TPKX is **LIVE-PROVEN on multiple project packages**.

### ArcGIS Field Maps

Esri documents sideloaded TPKX basemaps on Android device storage or microSD.

Project status: **LIVE TEST PENDING**.

Acceptance must verify local basemap visibility/selection, offline pan/zoom, own position, and restart behavior.

---

## 8. Card-sizing model

Current practical coverage ladder:

```text
district → Z17
county → Z18
State Forests / selected hotspots → Z20
```

Where storage permits, Google Hybrid and Esri imagery/labels may coexist.

Final card tiers are chosen from real finished byte counts, not theory.

---

## 9. Map Fountain — accepted proof / parked deployment

Map Fountain proved:

### Windows

```text
native TPKX
→ USB SSD
→ GL.iNet Flint 2
→ SMB / Wi-Fi
→ Windows ArcGIS Earth
```

Status: **LIVE-PROVEN**.

### Android

```text
Static REST WMTS
→ USB SSD
→ Flint 2 local HTTPS/WebDAV
→ Wi-Fi
→ ArcGIS Earth Mobile
```

Status: **LIVE-PROVEN**.

Current disposition: parked from the primary personal-phone path.

Possible future role: Starlink-connected basecamp storage / poor-man's NAS.

---

## 10. ArcGIS Earth runtime and live positioning

Live-proven / observed capabilities include:

- local native TPKX;
- router-hosted TPKX over SMB;
- local TPKX on ArcGIS Earth Mobile;
- KML / KMZ / NetworkLinks;
- native GNSS/NMEA own-position display;
- Automation API;
- native drawings/markers;
- PRAVE remote-unit display.

Known-good GNSS observation:

- 9600 baud;
- GLL and RMC present.

PRAVE → ArcGIS Earth Automation API remains **LIVE-PROVEN**.

---

## 11. Four-project separation

- **Offline GeoStack** — master field-mapping / Factory architecture.
- **Rasta Pyramid Factory** — general giant-raster pyramid manufacturing.
- **Map Fountain** — router/network-storage proof history and possible shared-storage revival.
- **Android Field Maps + ArcGIS Earth** — final personal-phone / microSD deployment workflow.

This prevents yesterday's experiment from becoming tomorrow's accidental baseline.

---

## 12. Offline boundary

There can be no operational dependence on public Internet connectivity.

Online services may assist map manufacture, imagery refresh, or optional enhancements. Prepared field maps must remain available when outside connectivity disappears.

---

## 13. Do-not-regress rules

1. Keep Offline Map Factory 1.0 free of REST unless a real target demonstrates the need.
2. Preserve historical TPKX Map Factory v1.0.0 as a frozen accepted milestone.
3. Keep the proven MBTiles → TPKX converter stable unless a verified defect is established.
4. Do not revive reverse TPKX → MBTiles recovery as a production shortcut.
5. Keep the user-facing package root clean; internal machinery belongs behind `System Files`.
6. Do not require Map Fountain/router infrastructure for normal personal-phone deployment.
7. Do not make public Internet part of the core map path.
8. Do not confuse vendor documentation or self-test success with project live proof.
9. Change one major test variable at a time.
10. Let the real target decide acceptance.

> **Keep the Factory simple. Keep the package clean. Let the target prove the release.**
