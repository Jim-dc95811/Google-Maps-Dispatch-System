# Offline GeoStack — Changelog

This file records public architecture milestones and preserves explored branches as lineage without confusing them with the current product.

## 2026-08-20 — strict Field Maps TPKX conformance failure isolated; canonical repair branch opened

A real ArcGIS Field Maps control test exposed a compatibility defect in the historical MBTiles -> TPKX converter lineage.

### Decisive control

Using the same physical microSD, same Field Maps Designer map, and same `basemaps` folder:

- project converter-built District 7 TPKX: **REJECTED** as spatial-reference incompatible;
- Esri official `Usa.tpkx`: **ACCEPTED**.

This proves the Field Maps Designer workflow, public web map, physical-card path, and general Web Mercator setup are good. The defect is isolated to the project's TPKX package construction.

### Converter status correction

The historical converter remains **LIVE-PROVEN for ArcGIS Earth** and has also produced packages accepted by ArcGIS Earth Mobile and ArcGIS Pro.

It is **not currently Field Maps-conformant**.

One concrete deviation was found: the old converter calculated Web Mercator LOD resolution/scale values instead of copying Esri's canonical values. Example LOD 0 scale:

```text
historical converter: 591657527.5917094
Esri native sample:    591657527.591555
```

The difference repeats through the LOD table. This is a verified package difference but is not yet claimed as the sole cause.

### Esri-canonical test branch

Created `ESRI_CANONICAL_TPKX_TEST_v0_2_0` as a separate TEST line while preserving the frozen historical converter.

The test converter copies Esri's canonical:

- LOD 0-23 resolutions/scales;
- Web Mercator origin;
- spatial-reference structure;
- `root.json` conventions;
- `iteminfo.json` field types.

Synthetic MBTiles conversion, package/ZIP checks, and Compact Cache V2 bundle/index checks passed.

**Field Maps acceptance remains pending.**

Immediate next gate: small MBTiles -> v0.2.0 canonical TPKX -> physical microSD -> Field Maps. Only after that passes should district-scale TPKX/MMPK products be regenerated.

### ArcGIS Pro MMPK implication

ArcGIS Pro's MMPK bridge remains a successful packaging proof, but Pro preserves the source TPKX intact under `commondata/new_tpkx/`. Therefore an MMPK built from the old converter is not a repair path for the Field Maps defect.

### New engineering doctrine

> **When an official working reference implementation exists, reproduce/conform to it first. Do not invent an alternative until the reference path has been exhausted.**

See `docs/TPKX_FIELD_MAPS_CONFORMANCE_2026-08-20.md`.

---

## 2026-08-18 — Offline Map Factory 1.0 product reset

A new clean finished-product line was created:

**OFFLINE MAP FACTORY 1.0**

Status at creation: **BUILT / SELF-TESTED — LIVE ACCEPTANCE PENDING**.

Current operator feature set:

- four map sources: Google Earth, Google Hybrid, Esri World, Esri World / Google Labels;
- Z0–Z20;
- output choice: TPKX / MBTiles / Both;
- one Advanced Tool: existing MBTiles → TPKX.

The experimental REST / Static WMTS output path was removed from the current Factory.

### Packaging standard

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

Offline Map Factory 1.0 must earn its own live acceptance on the real target before release promotion. After the 2026-08-20 Field Maps result, that acceptance must not reuse the historical converter for Field Maps deployment claims until conformance is repaired.

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
- local TPKX on ArcGIS Earth Mobile remains LIVE-PROVEN on multiple project packages.

### Map Fountain disposition

Map Fountain's router-only Windows and Android paths remain **LIVE-PROVEN**, but the project parked Map Fountain from the primary personal-phone deployment path.

Preserved proof:

- native TPKX → Flint 2 / SMB → ArcGIS Earth Windows;
- Static REST WMTS → Flint 2 HTTPS/WebDAV → ArcGIS Earth Mobile.

Possible future role: Starlink-connected basecamp storage / poor-man's NAS.

---

## 2026-08-17 — router-only Map Fountain proofs

The field map appliance was simplified to a consumer router plus USB SSD and live-proven on both Windows and Android.

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

### Compatibility boundary added later

The release remains accepted for the target actually tested on 2026-08-15: Factory manufacture plus ArcGIS Earth rendering. On 2026-08-20, the historical converter lineage failed strict Field Maps TPKX acceptance. Do not retroactively broaden the original release claim into Field Maps compatibility.

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

The standalone converter was live-proven in ArcGIS Earth before Factory integration. Field Maps conformance was not tested at that time and later failed in the 2026-08-20 control test.

---

## ArcGIS Earth pivot — August 2026

The project moved away from Google Earth Pro as the primary viewer after extensive offline/cache/local-server/Enterprise exploration.

ArcGIS Earth provided native TPKX support, KML/KMZ/NetworkLinks, GNSS/NMEA, local Automation API, drawings/markers, 3D globe operation, and session restoration.

---

## Google Earth / KML Super Overlay era — legacy lineage

Earlier architecture included QGIS MBTiles manufacturing, MBTiles → KML Super Overlay conversion, KML forest/Blooming Onion deployment, warm-cache recovery, Network Earth local serving, Google Earth Enterprise exploration, and packet-capture diagnostics.

These remain engineering history, not the current primary viewer/deployment baseline.
