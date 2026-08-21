# Offline GeoStack — Technical Architecture

## Purpose

This document records the current architecture after the 2026-08-20 ArcGIS Field Maps TPKX control test.

Master identity:

**Offline GeoStack — QGIS -> verified MBTiles -> target-conformant TPKX -> offline field deployment + live field positioning**

---

## 1. Current architectural summary

```text
MAP MANUFACTURING
source imagery / QGIS layer stack
        |
        v
Offline Map Factory 1.0
        |
        v
QGIS 3.44.9 rendering engine
        |
        v
verified raster MBTiles
        |\
        | `-> publish MBTiles
        `----> TPKX packaging bridge
                 |
                 +-> historical converter: ArcGIS Earth-proven
                 `-> Esri-canonical repair: Field Maps acceptance pending

PERSONAL MOBILE DEPLOYMENT AFTER REPAIR
corrected TPKX
        |
        +-> ArcGIS Pro MMPK wrapper where needed
        |
        v
physical microSD
        |
        v
ArcGIS Field Maps + ArcGIS Earth Mobile

LIVE FIELD INPUTS
GNSS / PRAVE / F22 / QR / KML
        |
        v
ArcGIS Earth native inputs / Automation API
```

No public Internet connection is required for prepared local-map display.

---

## 2. Current TPKX conformance boundary

A strict Field Maps control test proved:

```text
same physical microSD
same Designer map
same basemaps folder

project converter TPKX -> REJECTED
Esri official Usa.tpkx -> ACCEPTED
```

The physical-card path and Field Maps configuration are therefore live-proven.

The current defect is the historical TPKX package construction.

### Status language

- historical converter -> ArcGIS Earth: **LIVE-PROVEN**;
- historical converter -> ArcGIS Field Maps: **FAILED / NEEDS REPAIR**;
- Esri official `Usa.tpkx` -> Field Maps: **LIVE-PROVEN**;
- Esri-canonical v0.2.0 repair branch: **BUILT / SELF-TESTED — FIELD MAPS PENDING**.

---

## 3. Offline Map Factory 1.0 contract

Normal operator capability remains:

- Google Earth;
- Google Hybrid;
- Esri World;
- Esri World / Google Labels;
- HOME EXTENT / Clipboard History / two manual GPS points;
- Z0-Z20;
- TPKX / MBTiles / Both;
- Advanced existing MBTiles -> TPKX.

REST / Static WMTS is not part of the clean Factory.

Current status:

**BUILT / SELF-TESTED — RELEASE ACCEPTANCE BLOCKED ON TPKX CONFORMANCE.**

The QGIS -> MBTiles portion remains valid. The TPKX packaging stage must be replaced by the accepted canonical construction before the Factory is promoted for the current Field Maps deployment mission.

---

## 4. Why QGIS remains the rendering engine

QGIS already solves:

- projection/reprojection;
- source access;
- layer composition;
- labels/symbology;
- antialiasing;
- zoom-dependent rendering;
- tile-pyramid generation;
- MBTiles output.

Known-good render baseline:

- QGIS 3.44.9;
- EPSG:3857 / Web Mercator;
- PNG;
- 96 DPI;
- antialiasing ON;
- metatile 4;
- Z0-Z20.

The current Field Maps defect is downstream of this rendering stage.

---

## 5. MBTiles and TPKX roles

MBTiles contains the already-rendered raster pyramid.

The forward packaging bridge changes addressing/container structure without rerendering imagery:

```text
MBTiles raster tiles
-> TMS row conversion
-> Compact Cache V2 bundles/indexes
-> metadata/package structure
-> .tpkx
```

Critical row conversion:

```text
y_arcgis = (2^z - 1) - y_tms
```

Production rules:

- preserve direct QGIS-built MBTiles when MBTiles is wanted;
- do not reverse-recover important production MBTiles from TPKX;
- do not assume a TPKX is target-conformant merely because ArcGIS Earth opens it.

---

## 6. Historical converter versus canonical repair

### Historical converter

The historical converter handled large production tile counts and was accepted by ArcGIS Earth. It also produced project packages opened by ArcGIS Earth Mobile and ArcGIS Pro.

Field Maps later rejected its output.

### Concrete deviation

The old code calculated Web Mercator LOD resolution/scale values.

Example:

```text
LOD 0 scale
historical converter: 591657527.5917094
Esri native sample:    591657527.591555
```

The difference repeats through the table.

### Esri-canonical v0.2.0 TEST

The repair branch copies Esri's canonical:

- LOD 0-23 resolutions/scales;
- origin;
- spatial-reference structure;
- `root.json` conventions;
- `iteminfo.json` field types.

Bench package/bundle checks passed. Field Maps is the pending acceptance target.

Do not claim the LOD table is the sole root cause until the target proves the repaired package.

---

## 7. Factory product lineage

### Historical TPKX Map Factory v1.0.0

**RELEASE-ACCEPTED / FROZEN — 2026-08-15 — ArcGIS Earth target.**

Preserve the exact artifact and original acceptance evidence.

The 2026-08-20 Field Maps result narrows compatibility claims but does not erase the original release.

### Offline Map Factory 1.0

Current clean product line.

Release promotion waits for the converter repair and then a real product acceptance sequence.

### REST / Static WMTS

Parked engineering history under Map Fountain. Not part of the current Factory.

---

## 8. Finished-package architecture

User-facing top level remains:

```text
OFFLINE MAP FACTORY 1.0 - Installation Guide.pdf
OFFLINE MAP FACTORY 1.0 - User Guide.pdf
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
RUN OFFLINE MAP FACTORY.bat
System Files\
```

Internal machinery belongs behind `System Files`.

Required QGIS project placement:

```text
C:\Google Earth Project\QGIS\
```

---

## 9. Personal Android deployment

### Field Maps now proven at the storage/configuration layer

LIVE-PROVEN:

- Field Maps Designer map;
- Offline enabled;
- File on the device;
- public sharing of the test map;
- physical `basemaps` directory;
- Esri official `Usa.tpkx`.

FAILED:

- project historical converter TPKX.

### ArcGIS Earth Mobile

Local project TPKX remains **LIVE-PROVEN on multiple packages**.

Do not generalize the stricter Field Maps rejection into an Earth Mobile failure.

---

## 10. ArcGIS Pro MMPK bridge

ArcGIS Pro 3.7 successfully packaged both small and approximately 52 GB district MMPKs.

For the small specimen:

- 0 errors / 0 warnings / 0 messages;
- version 3.0;
- source TPKX preserved under `commondata/new_tpkx/`;
- local `.mmap` reference;
- no HTTP/HTTPS URLs found;
- Windows ArcGIS Earth PASS while Not signed in.

Architectural consequence:

**MMPK wrapping is not a TPKX repair mechanism.**

Rebuild the district MMPK after corrected TPKX acceptance.

---

## 11. Intended final district-card architecture

```text
corrected district TPKX
        |
        +-> ArcGIS Earth Mobile direct local viewer
        |
        `-> ArcGIS Pro minimal MMPK
                 |
                 v
physical microSD
  +-- Field Maps mappackages\DISTRICT.mmpk
  `-- Field Maps basemaps\DISTRICT.tpkx
```

Redundancy is acceptable. Reliability outranks storage elegance.

---

## 12. Map Fountain

Map Fountain remains LIVE-PROVEN / PARKED.

Windows proof: native TPKX on Flint 2 USB SSD -> SMB -> ArcGIS Earth.

Android proof: Static REST WMTS -> Flint 2 local HTTPS/WebDAV -> Wi-Fi -> ArcGIS Earth Mobile.

It is not a converter workaround. Reopen only for a real shared-storage need.

---

## 13. ArcGIS Earth runtime and live positioning

Live-proven / observed capabilities include:

- local native TPKX;
- router-hosted TPKX over SMB;
- local TPKX on ArcGIS Earth Mobile;
- KML / KMZ / NetworkLinks;
- native GNSS/NMEA own-position display;
- Automation API;
- native drawings/markers;
- PRAVE remote-unit display.

Known-good GNSS: 9600 baud, GLL + RMC present.

PRAVE -> ArcGIS Earth Automation API remains **LIVE-PROVEN**.

---

## 14. Four-project separation

- **Offline GeoStack** — master manufacturing/integration and TPKX conformance repair.
- **Rasta Pyramid Factory** — giant-raster manufacturing; inherits accepted converter only after target proof.
- **Map Fountain** — proven shared-storage/network reference; parked.
- **Android Field Maps + ArcGIS Earth** — real Android deployment and acceptance evidence.

---

## 15. Do-not-regress rules

1. Keep Offline Map Factory free of REST unless a real need reopens it.
2. Preserve historical TPKX Map Factory v1.0.0 as frozen accepted evidence.
3. The historical converter is now legitimately reopened only through a new repair lineage because a verified defect exists.
4. Use Esri's official working TPKX as the construction reference.
5. Do not patch metadata by guesswork.
6. Do not use ArcGIS Pro MMPK wrapping as a sanitizer.
7. Prove a tiny canonical specimen before rebuilding district-scale products.
8. Do not revive reverse TPKX -> MBTiles recovery.
9. Do not require Map Fountain for normal personal-phone deployment.
10. Do not make public Internet part of the core field path.
11. Let the real target decide acceptance.

> **Keep the Factory simple. Conform to the real standard. Let the target prove the release.**
