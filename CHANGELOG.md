# Offline GeoStack — Changelog

This file records public architecture milestones. It intentionally distinguishes major design pivots from ordinary code edits and preserves the older Google Maps Dispatch System / Google Earth work as lineage rather than current branding.

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

This converts the earlier Map Fountain concept from architecture candidate to a real local mobile map-delivery mechanism.

### TPKX → MBTiles recovery experiment rejected

A reverse Compact Cache V2 recovery tool was prototyped. Controlled testing showed exact tile-byte recovery on a Thames Bridge fixture, but a recovered production map displayed blurred/missing regions on ArcGIS Earth Mobile.

Decision:

- do not use TPKX recovery as the production MBTiles path;
- remove recovery from the next Factory branch;
- rebuild important MBTiles directly from QGIS;
- preserve MBTiles going forward when Map Fountain use is expected.

### TPKX Map Factory v1.2.0 TEST built

v1.2 changes normal output choice to:

```text
TPKX
MBTiles
Both
```

`Both` is the current TEST default. The accepted v1.0.0 baseline remains frozen. v1.2 is BUILT / SELF-TESTED and entered Windows live acceptance on 2026-08-16.

---

## 2026-08-15 — Master project renamed **Offline GeoStack**

The project had grown beyond the original repository name. The current master identity is:

**Offline GeoStack — QGIS → TPKX → ArcGIS Earth + Live Field Positioning**

`TPKX Map Factory` remains the map-manufacturing subsystem. ArcGIS Earth remains the primary runtime. GNSS, PRAVE, F22, QR, and KML are field/live/interoperability inputs around that runtime.

Public documentation was reorganized around the new identity, the required QGIS projects were published, a professional GIS/future-AI engineering record was added, and the former Google Earth architecture was retained as historical lineage.

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

- ArcGIS Earth is the primary viewer/runtime.
- TPKX is the primary raster basemap deployment format in the frozen v1.0 workflow.
- MBTiles is the QGIS manufacturing intermediate.
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

ArcGIS Earth proved to provide a better modern fit through:

- native TPKX support;
- native KML/KMZ and NetworkLinks;
- native GNSS/NMEA support;
- local Automation API;
- native drawings / markers;
- modern 3D globe operation;
- session restoration.

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
