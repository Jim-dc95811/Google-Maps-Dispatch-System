# Offline GeoStack

## Offline map manufacturing + field-system integration

**Offline GeoStack is the master manufacturing and integration project for the four-repository family.**

> **QGIS makes the pixels. The Factory packages them. The deployment project puts the finished capability in the user's hands.**

**Keywords:** offline GIS, offline maps, QGIS, ArcGIS Earth, ArcGIS Field Maps, MMPK, TPKX, MBTiles, Compact Cache V2, microSD, cellular-data protection, map rationing, GNSS, PRAVE, wildland fire, human AI engineering

---

## Current priority — strict Field Maps TPKX conformance

A live ArcGIS Field Maps control test on 2026-08-20 changed the immediate engineering priority.

The project-built District 7 TPKX was found by Field Maps but rejected as spatial-reference incompatible. Esri's official `Usa.tpkx`, copied to the **same physical microSD folder** and referenced through the **same Field Maps Designer map**, worked.

That isolates the current defect to the project's historical MBTiles -> TPKX package construction rather than the SD-card path, Designer workflow, public map, or general Web Mercator setup.

**Current rule:** Esri's working TPKX is the construction reference. Field Maps is the judge.

- [TPKX / Field Maps Conformance — 2026-08-20](docs/TPKX_FIELD_MAPS_CONFORMANCE_2026-08-20.md)
- [Current Project Status — 2026-08-20](docs/PROJECT_STATUS_2026-08-20.md)
- [Android Field Maps + ArcGIS Earth](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-)

---

## Current status

| Subsystem | Status |
| --- | --- |
| **Offline Map Factory 1.0** | 🟡 **BUILT / SELF-TESTED — RELEASE ACCEPTANCE BLOCKED ON TPKX CONFORMANCE** |
| QGIS -> raster MBTiles manufacturing | ✅ **LIVE-PROVEN** |
| Historical MBTiles -> TPKX converter in ArcGIS Earth | ✅ **LIVE-PROVEN** |
| Historical converter output in ArcGIS Field Maps | ❌ **FAILED / NEEDS REPAIR** |
| Esri official `Usa.tpkx` in Field Maps from physical microSD | ✅ **LIVE-PROVEN** |
| Esri-canonical converter v0.2.0 test branch | 🟡 **BUILT / SELF-TESTED — FIELD MAPS TEST PENDING** |
| ArcGIS Pro existing TPKX -> minimal MMPK | ✅ **PASS — small and district-scale packages created** |
| Pro-created MMPK in Windows ArcGIS Earth | ✅ **PASS — rendered while Earth showed Not signed in** |
| ArcGIS Earth Windows native TPKX | ✅ **LIVE-PROVEN** |
| ArcGIS Earth Mobile local TPKX | ✅ **LIVE-PROVEN on multiple project packages** |
| Field Maps Designer + physical `basemaps` path | ✅ **LIVE-PROVEN** |
| Corrected district TPKX + MMPK cold-card acceptance | 🟡 **PENDING CANONICAL SMALL-TPKX PASS** |
| Native ArcGIS Earth GNSS | ✅ **LIVE-OBSERVED** |
| PRAVE -> ArcGIS Earth Automation API | ✅ **LIVE-PROVEN** |
| Map Fountain network delivery proofs | ✅ **LIVE-PROVEN / PARKED REFERENCE** |
| Historical TPKX Map Factory v1.0.0 | ✅ **RELEASE-ACCEPTED / FROZEN FOR ARCGIS EARTH TARGET** |
| TPKX -> MBTiles recovery | ❌ **REJECTED as production path** |
| Operational public-Internet dependency | **NONE BY DESIGN** |

---

## Offline Map Factory 1.0

The current clean Factory product line remains deliberately simple:

- four map sources:
  1. Google Earth
  2. Google Hybrid
  3. Esri World
  4. Esri World / Google Labels
- area from HOME EXTENT, Clipboard History diagonal points, or two manually entered GPS points;
- Z0-Z20;
- output choice: TPKX / MBTiles / Both;
- Advanced Tool: existing MBTiles -> TPKX;
- no REST / Static WMTS output in the clean product.

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

### Important release correction

The Factory's QGIS -> MBTiles manufacturing remains valid, but the historical TPKX converter now has a verified strict-Field-Maps compatibility defect.

Therefore **Offline Map Factory 1.0 must not be release-promoted with the old converter merely because its TPKX opens in ArcGIS Earth.**

The converter stage is reopened under a verified defect while the historical accepted release itself remains frozen.

---

## TPKX conformance repair branch

The old converter calculated Web Mercator LOD values. Esri's official TPKX uses fixed canonical values.

Example LOD 0 scale:

```text
historical converter: 591657527.5917094
Esri native sample:    591657527.591555
```

A separate test converter, `ESRI_CANONICAL_TPKX_TEST_v0_2_0`, now copies Esri's canonical LOD table and native metadata conventions instead of recalculating them.

Bench checks passed. **Field Maps has not accepted it yet.**

Immediate test:

```text
small MBTiles
-> Esri-canonical v0.2.0 test converter
-> small TPKX
-> physical microSD basemaps folder
-> Field Maps Designer exact filename
-> Field Maps
```

If that passes, the corrected converter is integrated into the Factory and Rasta before rebuilding district-scale deployment products.

---

## District-card mission

> **A Field Maps user must be able to open the app with zero public Internet and use a district-wide Esri Hybrid map through Z17. The same local map should stop the heavy basemap from burning cellular data when service exists.**

The user-facing value is freedom from **map rationing**.

The intended architecture remains:

```text
Offline Map Factory
-> corrected district TPKX
-> ArcGIS Pro minimal MMPK wrapper
-> physical microSD
   +-- Field Maps mappackages\DISTRICT.mmpk
   +-- Field Maps basemaps\DISTRICT.tpkx
-> Android
-> ArcGIS Field Maps + ArcGIS Earth Mobile
```

The duplicate TPKX remains intentional redundancy. Storage efficiency ranks below field reliability.

### ArcGIS Pro bridge remains valid

ArcGIS Pro 3.7 successfully created small and approximately 52 GB district MMPKs from existing TPKX files. The small package had 0 errors / 0 warnings / 0 messages and rendered in Windows ArcGIS Earth while Earth showed Not signed in.

However, Pro preserved the source TPKX intact under `commondata/new_tpkx/`. Therefore Pro packaging does **not** repair a nonconformant TPKX. Rebuild the district MMPK only after the corrected TPKX passes Field Maps.

---

## ArcGIS Earth integration

Live-proven / observed capabilities include:

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

- [PRAVE -> ArcGIS Earth engineering record](docs/PRAVE_ARCGIS_EARTH_INTEGRATION.md)
- [PRAVE Live user feature](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-/tree/main/features/prave-live)

---

## Historical Factory lineage

### TPKX Map Factory v1.0.0

**RELEASE-ACCEPTED / FROZEN — 2026-08-15**

Its actual acceptance target was Factory manufacture plus ArcGIS Earth rendering, and that history remains valid.

The 2026-08-20 Field Maps test adds a new compatibility boundary: do not describe historical converter output as universally ArcGIS/Field-Maps compatible.

The accepted ZIP remains frozen and must not be silently rebuilt or altered.

### REST / Static WMTS exploration

REST experiments remain useful history under Map Fountain but are not part of Offline Map Factory 1.0.

---

## Four-project family

1. **Offline GeoStack** — master map manufacturing + field-system integration.
2. **[Rasta Pyramid Factory](https://github.com/Jim-dc95811/Rasta-Pyramid-Factory)** — giant-raster / deep-zoom manufacturing; TPKX output inherits the current conformance repair boundary.
3. **[Map Fountain](https://github.com/Jim-dc95811/Map-Fountain)** — LIVE-PROVEN shared-storage/network delivery reference; parked from normal personal-phone use.
4. **[Android Field Maps + ArcGIS Earth](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-)** — deployment to the user and current Field Maps acceptance evidence.

---

## Hard doctrine

> **There can be no operational dependence on public Internet connectivity. Period.**

Online services may assist manufacturing or imagery refresh. At showtime, essential prepared-map use must survive loss of outside connectivity.

## Engineering doctrine added 2026-08-20

> **When an official working reference implementation exists, reproduce/conform to it first. Do not invent an alternative until the reference path has been exhausted.**

And always:

> **The real target decides acceptance.**

---

## Start here

- **[TPKX / Field Maps Conformance — 2026-08-20](docs/TPKX_FIELD_MAPS_CONFORMANCE_2026-08-20.md)**
- **[Current Project Status — 2026-08-20](docs/PROJECT_STATUS_2026-08-20.md)**
- **[The Journey of Ideas](docs/JOURNEY_OF_IDEAS.md)**
- **[The Bridges We Had to Build](docs/THE_BRIDGES_WE_HAD_TO_BUILD.md)**
- [Software & Downloads](docs/SOFTWARE_AND_DOWNLOADS.md)
- [Quick Start](docs/QUICK_START.md)
- [Release / candidate records](releases/README.md)
- [Android deployment + ArcGIS Earth user features](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-)
- [Map Fountain proof archive](https://github.com/Jim-dc95811/Map-Fountain)

---

## Licensing boundary

The MIT license covers original project code/documentation unless a file says otherwise. It does **not** grant rights to third-party imagery, labels, basemaps, vendor software, or external services.

---

# Offline GeoStack

> **Manufacture the geography once. Conform to the real standard. Put the heavy map on the card. Let the real field application decide acceptance.**
