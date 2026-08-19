# Offline GeoStack

## Offline map manufacturing + field-system integration

**Offline GeoStack is the master manufacturing and integration project for the four-repository family.**

> **QGIS makes the pixels. The Factory packages them. The deployment project puts the finished capability in the user’s hands.**

**Keywords:** offline GIS, offline maps, field mapping, QGIS, ArcGIS Earth, ArcGIS Field Maps, TPKX, MBTiles, Compact Cache V2, raster tiles, GNSS, PRAVE, microSD, Windows GIS

---

## Current status

| Subsystem | Status |
| --- | --- |
| **Offline Map Factory 1.0** | 🟡 **BUILT / SELF-TESTED — LIVE ACCEPTANCE PENDING** |
| QGIS → raster MBTiles manufacturing | ✅ **LIVE-PROVEN** |
| MBTiles → TPKX / Compact Cache V2 converter | ✅ **LIVE-PROVEN** |
| ArcGIS Earth Windows native TPKX | ✅ **LIVE-PROVEN** |
| ArcGIS Earth Mobile local TPKX | ✅ **LIVE-PROVEN on multiple packages** |
| Android Field Maps TPKX on microSD | 🟡 **VENDOR-DOCUMENTED / PROJECT LIVE TEST PENDING** |
| Native ArcGIS Earth GNSS | ✅ **LIVE-OBSERVED** |
| PRAVE → ArcGIS Earth Automation API | ✅ **LIVE-PROVEN** |
| Map Fountain network delivery proofs | ✅ **LIVE-PROVEN / PARKED REFERENCE** |
| Historical TPKX Map Factory v1.0.0 | ✅ **RELEASE-ACCEPTED / FROZEN MILESTONE** |
| TPKX → MBTiles recovery | ❌ **REJECTED as production path** |
| Operational public-Internet dependency | **NONE BY DESIGN** |

---

## Offline Map Factory 1.0

The current Factory product line is deliberately simple:

- four map sources:
  1. Google Earth
  2. Google Hybrid
  3. Esri World
  4. Esri World / Google Labels
- map area from HOME EXTENT, Clipboard History diagonal points, or two manually entered GPS points;
- operator-selectable **Z0–Z20**;
- output choice: **TPKX / MBTiles / Both**;
- one Advanced Tool: **existing MBTiles → TPKX**;
- no REST / Static WMTS output in the current Factory.

Known-good environment:

```text
Windows 10/11 64-bit
QGIS 3.44.9
Python 3.14.5
PNG raster tiles
96 DPI
antialiasing ON
metatile 4
Z0–Z20
```

**Evidence status:** BUILT / SELF-TESTED. The new product line still needs its own real Windows/QGIS acceptance run before promotion to RELEASE-ACCEPTED.

### Finished-package standard

```text
OFFLINE MAP FACTORY 1.0 - Installation Guide.pdf
OFFLINE MAP FACTORY 1.0 - User Guide.pdf
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
RUN OFFLINE MAP FACTORY.bat
System Files\
```

The operator sees a finished product, not a developer dump.

---

## Manufacturing chain

```text
source imagery / QGIS layer stack
→ QGIS 3.44.9
→ verified raster MBTiles
→ preserve MBTiles when useful
→ Compact Cache V2 converter
→ native TPKX
```

Production rule:

> **If MBTiles is needed, preserve the direct QGIS-built MBTiles. Do not reverse-recover important production MBTiles from TPKX.**

---

## Current field direction

```text
Offline Map Factory
→ finished TPKX
→ microSD / local storage
→ Android
→ ArcGIS Field Maps / ArcGIS Earth
```

The map maker owns the complicated side. The field user should receive prepared geography and a short procedure.

Current card-planning direction:

- District — Z17
- County — Z18
- State Forests / selected high-value areas — Z20
- Google Hybrid and Esri imagery/labels where useful and storage permits

The user-facing deployment work lives in:

**[Android Field Maps + ArcGIS Earth](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-)**

That repository now owns both **Android offline-map deployment** and **user-facing Windows ArcGIS Earth features** such as PRAVE Live and QR Command Bridge.

---

## ArcGIS Earth integration

Live-proven / observed project capabilities include:

- local native TPKX;
- router-hosted native TPKX over SMB;
- ArcGIS Earth Mobile local TPKX;
- KML / KMZ / NetworkLinks;
- native GNSS/NMEA own-position display;
- local Automation API;
- native drawings / markers;
- PRAVE remote-unit display.

Known-good GNSS observation:

```text
9600 baud
GLL + RMC present
```

The detailed PRAVE engineering record remains here, while the user-facing package lives in the deployment repository:

- [PRAVE → ArcGIS Earth engineering record](docs/PRAVE_ARCGIS_EARTH_INTEGRATION.md)
- [PRAVE Live user feature](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-/tree/main/features/prave-live)

---

## Historical Factory lineage

### TPKX Map Factory v1.0.0

**RELEASE-ACCEPTED / FROZEN — 2026-08-15**

This previous product line established the proven four-source QGIS workflow, Z0–Z20 manufacturing, the custom MBTiles → TPKX converter, and ArcGIS Earth acceptance.

It remains a historical milestone and is not silently rewritten to impersonate Offline Map Factory 1.0.

### REST / Static WMTS exploration

Later TEST branches explored REST output for Map Fountain. Those experiments remain useful engineering history, but REST is not part of the current Offline Map Factory product.

---

## Four-project family

1. **Offline GeoStack** — master map manufacturing + field-system integration.
2. **[Rasta Pyramid Factory](https://github.com/Jim-dc95811/Rasta-Pyramid-Factory)** — giant-raster / deep-zoom pyramid manufacturing.
3. **[Map Fountain](https://github.com/Jim-dc95811/Map-Fountain)** — LIVE-PROVEN shared-storage/network delivery evidence; currently parked from the normal personal-phone path.
4. **[Android Field Maps + ArcGIS Earth](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-)** — deployment to the user: Android offline maps + Windows ArcGIS Earth field features.

---

## Hard doctrine

> **There can be no operational dependence on public Internet connectivity. Period.**

Online services may assist manufacturing or imagery refresh. At showtime, essential prepared-map use must survive loss of outside connectivity.

---

## Evidence discipline

Use these labels literally:

- **DESIGNED**
- **BUILT / SELF-TESTED**
- **LIVE-OBSERVED**
- **LIVE-PROVEN**
- **RELEASE-ACCEPTED / FROZEN**

The real target decides acceptance.

---

## Start here

- [Current Project Status](docs/PROJECT_STATUS_2026-08-18.md)
- [Software & Downloads](docs/SOFTWARE_AND_DOWNLOADS.md)
- [Quick Start](docs/QUICK_START.md)
- [Required QGIS Projects](required_qgis_projects/)
- [Release / candidate records](releases/README.md)
- [Technical Architecture](docs/TECHNICAL_ARCHITECTURE.md)
- [Android deployment + ArcGIS Earth user features](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-)
- [Map Fountain proof archive](https://github.com/Jim-dc95811/Map-Fountain)

---

## Licensing boundary

The MIT license covers original project code/documentation unless a file says otherwise. It does **not** grant rights to third-party imagery, labels, basemaps, vendor software, or external services. Source licensing, caching, export, attribution, and redistribution remain source-specific.

---

# Offline GeoStack

> **Manufacture the geography once. Put it where the field user can reach it without asking the network for permission.**
