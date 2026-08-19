# Offline GeoStack

## QGIS → MBTiles / TPKX → offline field maps

**Offline GeoStack** is the master field-mapping and offline deployment project.

> **QGIS makes the pixels. The Factory packages them. Local storage puts them where the user needs them.**

---

## Current status

| Subsystem | Status |
| --- | --- |
| **Offline Map Factory 1.0** | 🟡 **BUILT / SELF-TESTED — LIVE ACCEPTANCE PENDING** |
| Four-source QGIS map manufacturing | ✅ **LIVE-PROVEN lineage** |
| MBTiles → TPKX / Compact Cache V2 converter | ✅ **LIVE-PROVEN** |
| ArcGIS Earth Windows native TPKX | ✅ **LIVE-PROVEN** |
| ArcGIS Earth Mobile local TPKX | ✅ **LIVE-PROVEN on multiple packages** |
| Android Field Maps TPKX on microSD | 🟡 **VENDOR-DOCUMENTED / PROJECT LIVE TEST PENDING** |
| Native ArcGIS Earth GNSS | ✅ **LIVE-OBSERVED** |
| PRAVE → ArcGIS Earth Automation API | ✅ **LIVE-PROVEN** |
| Map Fountain Windows TPKX over SMB | ✅ **LIVE-PROVEN / PARKED REFERENCE** |
| Map Fountain Android Static REST WMTS | ✅ **LIVE-PROVEN / PARKED REFERENCE** |
| Historical TPKX Map Factory v1.0.0 | ✅ **RELEASE-ACCEPTED / FROZEN MILESTONE** |
| TPKX → MBTiles recovery | ❌ **REJECTED as production path** |
| Operational public-Internet dependency | **NONE BY DESIGN** |

---

# Offline Map Factory 1.0

The current Factory product line has been deliberately reset to a clean finished-product identity:

**OFFLINE MAP FACTORY 1.0**

It takes the proven map-manufacturing work and removes the experimental REST/WMTS branch from the normal Factory.

### Normal operator capability

- **4 map sources**
  1. Google Earth
  2. Google Hybrid
  3. Esri World
  4. Esri World / Google Labels
- map area from HOME EXTENT, Clipboard History diagonal points, or two manually entered GPS points;
- operator-selectable **Z0–Z20**;
- finished output choice:
  - **TPKX**
  - **MBTiles**
  - **Both**
- one Advanced Tool:
  - **existing MBTiles → TPKX**

### What is intentionally not in the current Factory

- REST output;
- Static REST WMTS manufacturing;
- QR/service generation;
- router configuration;
- Map Fountain runtime logic;
- reverse TPKX → MBTiles recovery.

Those experiments remain documented as engineering history where useful, but they no longer define the normal Factory.

### Known-good environment

- Windows 10/11 64-bit
- **QGIS 3.44.9**
- **Python 3.14.5**
- PNG raster tiles
- 96 DPI
- antialiasing ON
- metatile 4
- Z0–Z20

### Current evidence status

The new **Offline Map Factory 1.0** package is **BUILT / SELF-TESTED**. It has not yet been promoted to LIVE-PROVEN or RELEASE-ACCEPTED under the new product name.

The next gate is a real Windows/QGIS build using the packaged product, followed by opening the finished TPKX in the intended target.

---

## Finished distribution standard

The public package is intentionally clean. At the top level the user sees exactly:

```text
OFFLINE MAP FACTORY 1.0 - Installation Guide.pdf
OFFLINE MAP FACTORY 1.0 - User Guide.pdf
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
RUN OFFLINE MAP FACTORY.bat
System Files\
```

No developer dump. No test BAT collection. No loose Python files. Internal support material stays behind `System Files`.

Installation places the two supplied QGIS projects here:

```text
C:\Google Earth Project\QGIS\
```

The normal operator then runs only:

```text
RUN OFFLINE MAP FACTORY.bat
```

---

## Current field direction — carry the map

```text
Offline Map Factory
        ↓
finished TPKX
        ↓
microSD card
        ↓
Android
        ↓
ArcGIS Field Maps / ArcGIS Earth
```

The map maker owns the complicated side. The field user should receive prepared geography and a short procedure.

Current card planning:

- **District — Z17**
- **County — Z18**
- **State Forests / selected high-value areas — Z20**
- Google Hybrid and Esri imagery/labels where capacity permits

Deployment work lives in:

**[Android Field Maps + ArcGIS Earth](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-)**

---

## Historical Factory lineage

### TPKX Map Factory v1.0.0 — 2026-08-15

The previous product line remains an important frozen milestone:

**RELEASE-ACCEPTED / FROZEN**

It established the proven four-source QGIS workflow, Z0–Z20 manufacturing, the custom MBTiles → TPKX converter, and ArcGIS Earth acceptance.

It is preserved as history and should not be silently rewritten to impersonate Offline Map Factory 1.0.

### REST / Static WMTS exploration

Later TPKX Map Factory TEST branches explored MBTiles / TPKX / REST outputs for Map Fountain. Those experiments taught useful lessons about giant directory trees and compact transport seeds, but REST has now been removed from the current Factory direction.

Keep that work as lineage. Do not let it creep back into the normal operator product without a new demonstrated need.

---

## ArcGIS Earth and live field positioning

Live-proven / observed capabilities include:

- local native TPKX;
- router-hosted native TPKX over SMB;
- ArcGIS Earth Mobile local TPKX;
- KML / KMZ / NetworkLinks;
- native GNSS/NMEA own-position display;
- Automation API;
- native drawings/markers;
- PRAVE remote-unit display.

Known-good GNSS observation:

- 9600 baud;
- GLL + RMC present.

---

## Map Fountain — proven / parked

[Map Fountain](https://github.com/Jim-dc95811/Map-Fountain) proved two useful local-network delivery paths:

- native TPKX on router-attached SSD → SMB/Wi-Fi → ArcGIS Earth Windows;
- Static REST WMTS on router-attached SSD → local HTTPS/Wi-Fi → ArcGIS Earth Mobile.

Those remain valid engineering proofs. They are not required personal-phone infrastructure.

Possible future role: **Starlink-connected basecamp storage / poor-man's NAS**.

---

## Rasta Pyramid Factory

[Rasta Pyramid Factory](https://github.com/Jim-dc95811/Rasta-Pyramid-Factory) is the sibling project for giant flat images and georeferenced rasters. It turns one large raster into a true multiscale pyramid for smooth overview-to-detail navigation.

---

## Four-project family

1. **Offline GeoStack** — master field-mapping / manufacturing project.
2. **[Rasta Pyramid Factory](https://github.com/Jim-dc95811/Rasta-Pyramid-Factory)** — giant-raster pyramid manufacturing.
3. **[Map Fountain](https://github.com/Jim-dc95811/Map-Fountain)** — proven router/storage delivery reference.
4. **[Android Field Maps + ArcGIS Earth](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-)** — deployment to normal Android users and microSD cards.

---

## Hard doctrine

> **There can be no operational dependence on public Internet connectivity. Period.**

Online services may be used to manufacture or refresh maps. At showtime, essential map use must survive loss of outside connectivity.

---

## Evidence discipline

Use the status labels literally:

- **DESIGNED**
- **BUILT / SELF-TESTED**
- **LIVE-OBSERVED**
- **LIVE-PROVEN**
- **RELEASE-ACCEPTED / FROZEN**

The real target decides acceptance.

---

## Start here

- **[Current Project Status — 2026-08-18](docs/PROJECT_STATUS_2026-08-18.md)**
- **[Software & Downloads](docs/SOFTWARE_AND_DOWNLOADS.md)**
- **[Quick Start](docs/QUICK_START.md)**
- **[Required QGIS Projects](required_qgis_projects/)**
- **[Release / candidate records](releases/README.md)**
- **[Technical Architecture](docs/TECHNICAL_ARCHITECTURE.md)**
- **[Android deployment project](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-)**
- **[Map Fountain proof archive](https://github.com/Jim-dc95811/Map-Fountain)**

---

## Licensing boundary

The MIT license covers original project code/documentation unless a file says otherwise. It does **not** grant rights to third-party imagery, labels, basemaps, vendor software, or external services. Source licensing, caching, export, attribution, and redistribution remain source-specific.

---

# Offline GeoStack

**Manufacture the geography once. Put it where the field user can reach it without asking the network for permission.**
