# Offline GeoStack — Project Status — 2026-08-18

## Executive state

The project now has a clean current Factory product line:

**OFFLINE MAP FACTORY 1.0**

Status: **BUILT / SELF-TESTED — LIVE ACCEPTANCE PENDING**.

The older **TPKX Map Factory v1.0.0** remains a separate RELEASE-ACCEPTED / FROZEN historical milestone.

Current four-project family:

1. **Offline GeoStack** — master field-mapping / Factory project.
2. **Rasta Pyramid Factory** — giant-raster / deep-zoom manufacturing.
3. **Map Fountain** — LIVE-PROVEN router/storage delivery experiments; PARKED reference / possible future Starlink NAS.
4. **Android Field Maps + ArcGIS Earth** — current personal-phone / microSD deployment.

---

## Offline Map Factory 1.0

Current operator capability:

- Google Earth;
- Google Hybrid;
- Esri World;
- Esri World / Google Labels;
- Z0–Z20;
- TPKX / MBTiles / Both;
- one Advanced Tool: existing MBTiles → TPKX.

REST / Static WMTS has been deliberately removed from the current Factory.

Known-good environment:

- Windows 10/11 64-bit;
- QGIS 3.44.9;
- Python 3.14.5;
- PNG;
- 96 DPI;
- antialiasing ON;
- metatile 4.

### Finished distribution standard

```text
OFFLINE MAP FACTORY 1.0 - Installation Guide.pdf
OFFLINE MAP FACTORY 1.0 - User Guide.pdf
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
RUN OFFLINE MAP FACTORY.bat
System Files\
```

The user-facing package root is intentionally clean. Internal machinery stays behind `System Files`.

### QGIS project placement

```text
C:\Google Earth Project\QGIS\
```

with:

```text
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
```

---

## Next Factory gate

The new product line must earn its own acceptance.

Real target sequence:

1. launch the packaged Factory;
2. MBTiles-only build;
3. TPKX-only build;
4. Both build;
5. Advanced MBTiles → TPKX;
6. open finished TPKX in ArcGIS Earth;
7. verify location, cartography, zoom behavior, navigation, cleanup, and final-output state.

After that passes, promote Offline Map Factory 1.0 to LIVE-PROVEN / RELEASE-ACCEPTED and freeze the exact package.

Fortification comes after acceptance and should address observed reliability needs without redesigning the architecture.

---

## REST exploration disposition

The v1.3/v1.4 REST/Static WMTS work remains engineering history.

It established useful lessons about giant file trees, packaging overhead, Static REST WMTS, and compact `.restmap` transport seeds.

Current decision: **PARKED**. REST is not part of Offline Map Factory 1.0.

---

## Current map-card sizing experiment

```text
Factory-built TPKX
→ microSD
→ Android
→ ArcGIS Field Maps / ArcGIS Earth
```

Current menu direction:

- District — Z17;
- County — Z18;
- State Forests / selected high-value areas — Z20;
- Google Hybrid and Esri imagery/labels where capacity permits.

Capacity tiers remain unfrozen until real finished byte counts exist.

---

## ArcGIS Earth status

- Windows local TPKX: **LIVE-PROVEN**.
- Android local TPKX: **LIVE-PROVEN on multiple packages**.
- Native GNSS: **LIVE-OBSERVED**, 9600 baud, GLL + RMC present.
- PRAVE → Automation API: **LIVE-PROVEN**.

---

## ArcGIS Field Maps status

Esri documents sideloaded `.tpk` / `.tpkx` basemaps on Android device storage or microSD.

Project status: **LIVE TEST PENDING**.

Acceptance must prove local basemap selection, Wi-Fi-only app restriction, offline pan/zoom, useful own position, and acceptable close/reopen behavior.

---

## Map Fountain

Windows TPKX-over-SMB and Android Static REST WMTS router paths are both **LIVE-PROVEN**.

Current disposition: **PARKED from the primary personal-phone path**.

Possible future role: Starlink-connected basecamp storage / poor-man's NAS.

---

## Rasta Pyramid Factory

- v0.1.3: **LIVE-PROVEN baseline**.
- v0.1.4 REST selection branch: **BUILT / SELF-TESTED history**, not the current Rasta baseline.

Rasta remains general raster-pyramid manufacturing.

---

## Rejected production path

TPKX → MBTiles recovery remains **REJECTED** after production visual defects on the mobile target.

Production rule: preserve direct QGIS-built MBTiles when MBTiles is needed.

---

## Hard doctrine

> **There can be no operational dependence on public Internet connectivity. Period.**

> **Keep the Factory simple. Keep the package clean. Let the real target decide acceptance.**
