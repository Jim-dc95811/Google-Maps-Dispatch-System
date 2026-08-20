# Offline GeoStack

## Offline map manufacturing + field-system integration

**Offline GeoStack is the master manufacturing and integration project for the four-repository family.**

> **QGIS makes the pixels. The Factory packages them. The deployment project puts the finished capability in the user's hands.**

**Keywords:** offline GIS, offline maps, field mapping, QGIS, ArcGIS Earth, ArcGIS Field Maps, MMPK, TPKX, MBTiles, Compact Cache V2, microSD, cellular-data protection, map rationing, GNSS, PRAVE, wildland fire, human AI engineering

---

## Why this exists

The machinery is only half the story.

This project grew from field and dispatch problems: getting useful geography to firefighters, keeping maps useful when coverage disappears, reducing cellular-data dependence, moving operational locations without forcing everyone into one proprietary platform, and teaching people how to interpret the imagery once they have it.

It is also a documented experiment in **human-led, AI-assisted engineering**: field experience and operational judgment define the mission; AI supplies much of the cross-domain coding, GIS, protocol, diagnostic, packaging, and documentation work; real-world testing decides what survives.

Start with:

- **[The Journey of Ideas](docs/JOURNEY_OF_IDEAS.md)**
- **[The Bridges We Had to Build](docs/THE_BRIDGES_WE_HAD_TO_BUILD.md)**
- **[Current Project Status — 2026-08-20](docs/PROJECT_STATUS_2026-08-20.md)**
- **[Android Field Maps + ArcGIS Earth](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-)**

---

## Current status

| Subsystem | Status |
| --- | --- |
| **Offline Map Factory 1.0** | 🟡 **BUILT / SELF-TESTED — LIVE ACCEPTANCE PENDING** |
| QGIS -> raster MBTiles manufacturing | ✅ **LIVE-PROVEN** |
| MBTiles -> TPKX / Compact Cache V2 converter | ✅ **LIVE-PROVEN** |
| ArcGIS Pro existing TPKX -> minimal MMPK | ✅ **PASS — small and district-scale packages created** |
| Pro-created MMPK in Windows ArcGIS Earth | ✅ **PASS — rendered while Earth showed Not signed in** |
| ArcGIS Earth Windows native TPKX | ✅ **LIVE-PROVEN** |
| ArcGIS Earth Mobile local TPKX | ✅ **LIVE-PROVEN on multiple packages** |
| Field Maps MMPK on physical microSD | 🟡 **VENDOR-DOCUMENTED / PROJECT LIVE TEST PENDING** |
| Field Maps standalone TPKX on physical microSD | 🟡 **VENDOR-DOCUMENTED / PROJECT LIVE TEST PENDING** |
| Native ArcGIS Earth GNSS | ✅ **LIVE-OBSERVED** |
| PRAVE -> ArcGIS Earth Automation API | ✅ **LIVE-PROVEN** |
| Map Fountain network delivery proofs | ✅ **LIVE-PROVEN / PARKED REFERENCE** |
| Historical TPKX Map Factory v1.0.0 | ✅ **RELEASE-ACCEPTED / FROZEN MILESTONE** |
| TPKX -> MBTiles recovery | ❌ **REJECTED as production path** |
| Operational public-Internet dependency | **NONE BY DESIGN** |

---

## Offline Map Factory 1.0

The current Factory product line remains deliberately simple:

- four map sources:
  1. Google Earth
  2. Google Hybrid
  3. Esri World
  4. Esri World / Google Labels
- map area from HOME EXTENT, Clipboard History diagonal points, or two manually entered GPS points;
- operator-selectable **Z0-Z20**;
- output choice: **TPKX / MBTiles / Both**;
- one Advanced Tool: **existing MBTiles -> TPKX**;
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
Z0-Z20
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
-> QGIS 3.44.9
-> verified raster MBTiles
-> preserve MBTiles when useful
-> Compact Cache V2 converter
-> native TPKX
```

Production rule:

> **If MBTiles is needed, preserve the direct QGIS-built MBTiles. Do not reverse-recover important production MBTiles from TPKX.**

---

## Current field direction — district card

The mission is now explicit:

> **A Field Maps user must be able to open the app with zero public Internet and use a district-wide Esri Hybrid map through Z17. The same local map should remove the need to burn cellular data on the heavy basemap when service exists.**

Current deployment chain:

```text
Offline Map Factory
-> district TPKX
-> ArcGIS Pro minimal MMPK wrapper
-> physical microSD
   +-- Field Maps mappackages\DISTRICT.mmpk
   +-- Field Maps basemaps\DISTRICT.tpkx
-> Android
-> ArcGIS Field Maps + ArcGIS Earth Mobile
```

The duplicate TPKX is intentional redundancy. Storage efficiency is lower priority than field reliability.

Current gold-test checkpoint:

- physical 128 GB exFAT microSD;
- approximately 52 GB district TPKX;
- approximately 52 GB matching district MMPK;
- first runtime target: Amazon Fire tablet;
- later GPS/own-position acceptance: GPS-capable personal Android phone.

The user-facing deployment work lives in:

**[Android Field Maps + ArcGIS Earth](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-)**

The strongest user-facing value is freedom from **map rationing**: keep the heavy district map local and preserve cellular data for communication.

---

## ArcGIS Pro MMPK bridge

On 2026-08-20, ArcGIS Pro 3.7 successfully created modern MMPKs from existing project TPKX files.

Small specimen observations:

- analyzer: 0 errors / 0 warnings / 0 messages;
- MMPK version 3.0;
- original TPKX preserved intact under `commondata/new_tpkx/`;
- no HTTP/HTTPS references found in the small specimen `.mmap` / `.mapx`;
- package rendered in Windows ArcGIS Earth while Earth showed **Not signed in**.

A district-scale approximately 52 GB MMPK then packaged successfully from the existing approximately 52 GB TPKX.

This proves the manufacturing bridge. **Field Maps runtime acceptance is still pending.**

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

- [PRAVE -> ArcGIS Earth engineering record](docs/PRAVE_ARCGIS_EARTH_INTEGRATION.md)
- [PRAVE Live user feature](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-/tree/main/features/prave-live)

---

## Historical Factory lineage

### TPKX Map Factory v1.0.0

**RELEASE-ACCEPTED / FROZEN — 2026-08-15**

This previous product line established the proven four-source QGIS workflow, Z0-Z20 manufacturing, the custom MBTiles -> TPKX converter, and ArcGIS Earth acceptance.

It remains a historical milestone and is not silently rewritten to impersonate Offline Map Factory 1.0.

### REST / Static WMTS exploration

Later TEST branches explored REST output for Map Fountain. Those experiments remain useful engineering history, but REST is not part of the current Offline Map Factory product.

---

## Four-project family

1. **Offline GeoStack** — master map manufacturing + field-system integration.
2. **[Rasta Pyramid Factory](https://github.com/Jim-dc95811/Rasta-Pyramid-Factory)** — giant-raster / deep-zoom pyramid manufacturing.
3. **[Map Fountain](https://github.com/Jim-dc95811/Map-Fountain)** — LIVE-PROVEN shared-storage/network delivery evidence; parked from the normal personal-phone path.
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

- **[Current Project Status — 2026-08-20](docs/PROJECT_STATUS_2026-08-20.md)**
- **[The Journey of Ideas](docs/JOURNEY_OF_IDEAS.md)**
- **[The Bridges We Had to Build](docs/THE_BRIDGES_WE_HAD_TO_BUILD.md)**
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

> **Manufacture the geography once. Put the heavy map on the card. Let the real field application decide acceptance.**
