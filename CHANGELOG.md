# Offline GeoStack — Changelog

This file records public architecture milestones. It intentionally distinguishes major design pivots from ordinary code edits and preserves older experiments as lineage rather than silently treating every explored branch as current.

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

The actual-user-MBTiles lifecycle fixture passed self-test with byte-for-byte tile comparison and no temporary restored MBTiles. v1.4.0 remains a TEST branch and does not replace the frozen v1.0.0 baseline.

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

A second offline deployment path was proven alongside local TPKX.

### ArcGIS Earth Mobile local TPKX

- ArcGIS Earth Mobile opened multiple locally stored TPKX packages on Android.
- Successful examples included a Rasta Thames Bridge package and smaller Esri / Google Hybrid map packages.
- One larger Google Hybrid package returned `spatial reference not supported`; package-level compatibility remains a controlled test item.

### USB Map Fountain

`Rasta USB Map Fountain v0.2.1 TEST` was live-proven serving raster MBTiles from Windows to ArcGIS Earth Mobile over the Android USB-tether network.

Proven chain:

```text
MBTiles on PC / SSD
→ local HTTPS WMTS
→ Android USB tether / Remote NDIS
→ ArcGIS Earth Mobile
```

Live observations:

- outside Internet removed: **PASS**;
- HTTPS: **PASS**;
- QR service loading: **PASS**;
- selectable MBTiles GUI: **PASS**;
- unique per-map WMTS identity fixed stale test-map reuse;
- three different substantial MBTiles: **PASS**;
- large Lago panorama streamed and navigated smoothly on Android;
- deliberate pan/zoom is reliable; rapid repeated zoom/pan can outrun the current mobile delivery/render path.

This branch remains useful engineering history but is no longer the default deployment direction.

### TPKX → MBTiles recovery experiment rejected

A reverse Compact Cache V2 recovery tool was prototyped. Controlled testing showed exact tile-byte recovery on a Thames Bridge fixture, but a recovered production map displayed blurred/missing regions on ArcGIS Earth Mobile.

Decision:

- do not use TPKX recovery as the production MBTiles path;
- rebuild important MBTiles directly from QGIS;
- preserve MBTiles going forward when MBTiles is needed.

### TPKX Map Factory v1.2.0 TEST built

v1.2 changed normal output choice to TPKX / MBTiles / Both. The accepted v1.0.0 baseline remained frozen.

---

## 2026-08-15 — Master project renamed **Offline GeoStack**

The project had grown beyond the original repository name. The current master identity became **Offline GeoStack**.

`TPKX Map Factory` remains the map-manufacturing subsystem. ArcGIS Earth remains a primary runtime. GNSS, PRAVE, F22, QR, and KML are field/live/interoperability inputs around that runtime.

---

## v1.0.0 — 2026-08-15 — RELEASE ACCEPTED

First frozen public baseline of the **TPKX Map Factory + ArcGIS Earth** architecture now carried by Offline GeoStack.

### Added

- Four-source normal-user Factory workflow.
- Manual decimal-degree GPS diagonal-point entry.
- Clipboard-history coordinate workflow.
- Direct HOME EXTENT input.
- Z0–Z20 operator zoom selection.
- QGIS 3.44.9 raster manufacturing stage.
- 96 DPI / PNG / antialiasing ON / metatile 4 frozen recipe.
- Custom MBTiles → TPKX converter using Esri Compact Cache V2.
- Advanced **MBTILES → TPKX** path for GIS professionals.
- Colored GUI icons and strong visual landmarks.
- Progress indication and clear completion state.
- One-finished-TPKX destination behavior.

### Live acceptance

- Small v1.0 smoke build accepted by ArcGIS Earth.
- Large Esri World / Google Labels Factory build accepted by ArcGIS Earth.
- Large existing-MBTiles advanced conversion accepted by ArcGIS Earth.

### Architecture

- ArcGIS Earth became the primary viewer/runtime.
- TPKX became the primary raster basemap deployment format in the frozen v1.0 workflow.
- MBTiles remained the QGIS manufacturing intermediate.
- Hard rule established: no operational dependence on Internet connectivity.

---

## v0.1.6 TEST — 2026-08-15

- Advanced MBTiles → TPKX control moved into an always-visible bottom command area.
- Large existing-MBTiles conversion live-proven.
- Large Esri World / Google Labels Factory run live-proven.
- Established the mechanics later frozen into v1.0.0.

## v0.1.5 TEST — 2026-08-15

- Added GUI access to the existing-MBTiles → TPKX converter.
- First advanced-user integration build.
- Initial control placement proved too low for the real target screen and was corrected in v0.1.6.

## v0.1.4 TEST — 2026-08-15

- Finalized temporary-work cleanup behavior.
- Moved manufacturing artifacts out of the user-selected destination.
- Established the requirement that the destination contain only the finished TPKX.
- First large production-style Factory run passed.

## v0.1.3 TEST — 2026-08-15

- Removed SHA/fingerprint gates from the public Factory workflow.
- Simplified source-project handling.
- Esri World / Google Labels small test passed in ArcGIS Earth.

## v0.1.2 TEST — 2026-08-15

- Removed Neighbor Extent from the beginner-facing Factory.
- Renamed map-area section for normal users.
- Added two manual diagonal GPS coordinate fields.
- Removed Grid ID.
- Removed automatic filename suggestions.
- Made the HOME EXTENT order visible to the operator.

## v0.1.1 TEST — 2026-08-14/15

- Switched current public raster recipe to 96 DPI.
- Added the Esri World / Google Labels source path.
- Removed unnecessary Factory behavior text from the GUI.
- Narrowed the source menu toward the final four-source design.

## v0.1.0 TEST — 2026-08-13/14

- First integrated QGIS → temporary MBTiles → custom converter → TPKX Factory.
- Google Hybrid acceptance run succeeded.
- Output opened directly in ArcGIS Earth.

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

The project moved away from Google Earth Pro as the primary viewer after extensive offline, cache, local-server, and Google Earth Enterprise exploration.

ArcGIS Earth provided a better modern fit through native TPKX support, KML/KMZ/NetworkLinks, GNSS/NMEA, local Automation API, drawings/markers, 3D globe operation, and session restoration.

PRAVE display was subsequently live-proven through the ArcGIS Earth Automation API.

---

## Google Earth / KML Super Overlay era — 2026 legacy lineage

Earlier architecture included:

- QGIS MBTiles manufacturing;
- direct MBTiles → KML Super Overlay conversion;
- KML forest / Blooming Onion deployment;
- map depot production;
- warm-cache recovery;
- Network Earth local serving;
- Google Earth Enterprise exploration;
- packet-capture diagnostics.

These branches remain important engineering history but are no longer the current primary viewer/deployment baseline.
