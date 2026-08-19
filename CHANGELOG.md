# Offline GeoStack — Changelog

This file records public architecture milestones and preserves explored branches as lineage without confusing them with the current product.

## 2026-08-18 — Offline Map Factory 1.0 product reset

A new clean finished-product line was created:

**OFFLINE MAP FACTORY 1.0**

Status: **BUILT / SELF-TESTED — LIVE ACCEPTANCE PENDING**.

Current operator feature set:

- four map sources: Google Earth, Google Hybrid, Esri World, Esri World / Google Labels;
- Z0–Z20;
- output choice: TPKX / MBTiles / Both;
- one Advanced Tool: existing MBTiles → TPKX.

The experimental REST / Static WMTS output path was removed from the current Factory.

### Packaging standard

The finished distribution root was simplified to exactly:

```text
OFFLINE MAP FACTORY 1.0 - Installation Guide.pdf
OFFLINE MAP FACTORY 1.0 - User Guide.pdf
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
RUN OFFLINE MAP FACTORY.bat
System Files\
```

Internal implementation/support files remain behind `System Files` rather than cluttering the operator-facing root.

### Documentation

- one-page Installation Guide created;
- one-page User Guide created;
- both PDFs published in `docs/guides/`;
- Quick Start, Software & Downloads, QGIS project placement, Technical Architecture, Roadmap, continuity, release records, and contribution rules updated to the new product line.

### Release discipline

The prior **TPKX Map Factory v1.0.0** remains a separate RELEASE-ACCEPTED / FROZEN historical milestone.

Offline Map Factory 1.0 must earn its own live acceptance on the real Windows/QGIS target before release promotion.

---

## 2026-08-18 — personal-phone / microSD deployment direction

A fourth sibling repository was established as the deployment end of the system:

**Android Field Maps + ArcGIS Earth**

Current personal-phone direction:

```text
Factory-built TPKX
→ microSD card
→ Android
→ ArcGIS Field Maps / ArcGIS Earth
```

Key decisions:

- normal field users should receive prepared cards rather than be expected to learn the Factory;
- card capacity planning is based on real finished byte counts;
- current menu direction is district Z17, county Z18, and selected State Forest/high-value Z20 coverage;
- Google Hybrid and Esri imagery/labels may both be carried when capacity permits;
- protecting personal cellular data plans is a first-class requirement;
- Esri documents Android/device-microSD TPKX sideloading in Field Maps, but this project's own Field Maps acceptance test is still pending;
- local TPKX on ArcGIS Earth Mobile remains LIVE-PROVEN on multiple project packages.

### Map Fountain disposition

Map Fountain's router-only Windows and Android paths remain **LIVE-PROVEN**, but the project has parked Map Fountain from the primary personal-phone deployment path.

Preserved proof:

- native TPKX → Flint 2 / SMB → ArcGIS Earth Windows;
- Static REST WMTS → Flint 2 HTTPS/WebDAV → ArcGIS Earth Mobile.

Possible future role: Starlink-connected basecamp storage / poor-man's NAS.

### TPKX Map Factory v1.3 / v1.4 REST exploration

Production-scale Static REST work exposed the cost of giant expanded tile trees.

A v1.3.2 specimen reached 271,506 REST tiles and spent hours in expansion/packaging/finalization work.

`TPKX_MAP_FACTORY_v1_4_0_TEST` reset the experimental REST transport around a compact `.restmap` seed:

```text
verified MBTiles
→ <map>_REST.restmap
→ move one file
→ deploy/expand the runtime WMTS tree at the final SSD
```

The actual-user-MBTiles lifecycle fixture passed self-test with byte-for-byte tile comparison and no temporary restored MBTiles. v1.4.0 remained a TEST branch and did not replace the frozen v1.0.0 baseline.

---

## 2026-08-17 — router-only Map Fountain proofs

The field map appliance was simplified to a consumer router plus USB SSD and then live-proven on both Windows and Android.

### Windows ArcGIS Earth

```text
native TPKX on USB SSD
→ GL.iNet Flint 2
→ Samba / SMB
→ private Ethernet or Wi-Fi
→ Windows
→ ArcGIS Earth
```

A production-scale `ESG1N.tpkx` remained on router-attached storage while ArcGIS Earth opened and rendered it over Wi-Fi.

### Android ArcGIS Earth Mobile

```text
Static REST WMTS folder
→ USB SSD
→ Flint 2 local HTTPS/WebDAV
→ Wi-Fi
→ Android
→ ArcGIS Earth Mobile
```

The Android map rendered, then rendered again after ArcGIS Earth app cache clear and force-stop/reopen.

No Python runtime, helper app, QGIS Server, Windows map server, or Raspberry Pi was required in the accepted Android router path.

---

## 2026-08-16 — ArcGIS Earth Mobile + local Map Fountain path LIVE-PROVEN

### ArcGIS Earth Mobile local TPKX

- ArcGIS Earth Mobile opened multiple locally stored TPKX packages on Android.
- Successful examples included a Rasta Thames Bridge package and smaller Esri / Google Hybrid map packages.
- One larger Google Hybrid package returned `spatial reference not supported`; package-level compatibility remained a controlled test item.

### USB Map Fountain

`Rasta USB Map Fountain v0.2.1 TEST` was live-proven serving raster MBTiles from Windows to ArcGIS Earth Mobile over the Android USB-tether network.

```text
MBTiles on PC / SSD
→ local HTTPS WMTS
→ Android USB tether / Remote NDIS
→ ArcGIS Earth Mobile
```

Live observations included outside-Internet removal PASS, HTTPS PASS, QR loading PASS, selectable MBTiles PASS, multiple substantial MBTiles PASS, and large Lago panorama PASS.

### TPKX → MBTiles recovery experiment rejected

A reverse Compact Cache V2 recovery tool worked on a controlled fixture, but a recovered production map displayed blurred/missing regions on ArcGIS Earth Mobile.

Decision: preserve direct QGIS-built MBTiles when MBTiles is needed; do not use reverse recovery as the production shortcut.

### TPKX Map Factory v1.2.0 TEST

v1.2 introduced TPKX / MBTiles / Both output choices while the accepted v1.0.0 baseline remained frozen.

---

## 2026-08-15 — Master project renamed Offline GeoStack

The master project identity became **Offline GeoStack**.

`TPKX Map Factory` remained the map-manufacturing subsystem. ArcGIS Earth became the primary runtime; GNSS, PRAVE, F22, QR, and KML remained field/live/interoperability inputs around that runtime.

---

## TPKX Map Factory v1.0.0 — 2026-08-15 — RELEASE ACCEPTED

First frozen public baseline of the TPKX Map Factory + ArcGIS Earth architecture.

### Added

- four-source normal-user Factory workflow;
- manual decimal-degree GPS diagonal-point entry;
- Clipboard History coordinate workflow;
- direct HOME EXTENT input;
- Z0–Z20;
- QGIS 3.44.9 raster manufacturing;
- 96 DPI / PNG / antialiasing ON / metatile 4;
- custom MBTiles → TPKX converter using Esri Compact Cache V2;
- Advanced MBTiles → TPKX path;
- progress indication and completion state;
- cleaned destination behavior.

### Live acceptance

- small v1.0 smoke build → ArcGIS Earth PASS;
- large Esri World / Google Labels Factory build → PASS;
- large existing-MBTiles advanced conversion → PASS.

### Architecture

- ArcGIS Earth became the primary viewer/runtime;
- TPKX became the primary raster deployment format in the frozen v1.0 workflow;
- MBTiles remained the QGIS manufacturing intermediate;
- hard rule established: no operational dependence on public Internet connectivity.

---

## Standalone MBTiles → TPKX converter — 2026-08-13

A custom Python converter was built to bridge raster MBTiles into Esri TPKX / Compact Cache V2.

Key properties:

- reads standard raster PNG/JPEG MBTiles;
- preserves existing raster tile bytes;
- flips TMS Y addressing to ArcGIS top-origin addressing;
- writes 128×128 Compact Cache V2 bundles;
- creates TPKX metadata and ZIP64 package structure;
- uses Python standard library only.

The standalone converter was live-proven in ArcGIS Earth before Factory integration.

---

## ArcGIS Earth pivot — August 2026

The project moved away from Google Earth Pro as the primary viewer after extensive offline/cache/local-server/Enterprise exploration.

ArcGIS Earth provided native TPKX support, KML/KMZ/NetworkLinks, GNSS/NMEA, local Automation API, drawings/markers, 3D globe operation, and session restoration.

---

## Google Earth / KML Super Overlay era — legacy lineage

Earlier architecture included QGIS MBTiles manufacturing, MBTiles → KML Super Overlay conversion, KML forest/Blooming Onion deployment, warm-cache recovery, Network Earth local serving, Google Earth Enterprise exploration, and packet-capture diagnostics.

These remain engineering history, not the current primary viewer/deployment baseline.
