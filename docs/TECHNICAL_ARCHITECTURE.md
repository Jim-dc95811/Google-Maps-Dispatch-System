# Offline GeoStack — Technical Architecture

## Purpose

This document records the **current** Offline GeoStack architecture after the router-only Map Fountain proofs and the subsequent simplification toward direct local mobile storage.

Master identity:

**Offline GeoStack — QGIS → MBTiles / TPKX → offline field deployment + live field positioning**

---

## 1. Current architectural summary

```text
MAP MANUFACTURING
source imagery / QGIS layer stack
        ↓
QGIS 3.44.9 rendering engine
        ↓
verified raster MBTiles
        ↓
        ├─→ preserve MBTiles when useful
        └─→ frozen Compact Cache V2 converter → native TPKX

PERSONAL MOBILE DEPLOYMENT — CURRENT DIRECTION
native TPKX
        ↓
microSD card
        ↓
Android
        ↓
ArcGIS Field Maps / ArcGIS Earth

WINDOWS / SHARED-STORAGE PROOF
native TPKX
        ↓
USB SSD → Flint 2 → SMB
        ↓
Windows ArcGIS Earth

LIVE FIELD INPUTS
GNSS / PRAVE / F22 / QR / KML
        ↓
ArcGIS Earth native inputs / Automation API
```

No outside Internet connection is required for the local TPKX display path.

---

## 2. Why QGIS remains the rendering engine

QGIS already solves the GIS/cartographic work:

- reprojection;
- raster/vector compositing;
- label rendering;
- antialiasing;
- source access;
- zoom-dependent cartography;
- tile-pyramid generation;
- MBTiles output.

The Factory uses QGIS as a headless rendering engine rather than rebuilding GIS behavior.

Current known-good render baseline:

- QGIS 3.44.9;
- EPSG:3857 / Web Mercator tile scheme;
- PNG raster tiles;
- 96 DPI;
- antialiasing ON;
- metatile 4;
- operator-selectable Z0–Z20.

---

## 3. MBTiles and TPKX roles

MBTiles contains the already-rendered raster pyramid.

The frozen forward converter changes addressing/container structure without rerendering the map:

```text
MBTiles raster tiles
→ TMS row conversion
→ Compact Cache V2 bundles/indexes
→ native .tpkx
```

Critical row conversion:

```text
y_arcgis = (2^z - 1) - y_tms
```

The raster image bytes produced by QGIS are preserved.

Production rule:

- preserve direct QGIS MBTiles when MBTiles is needed;
- do not use reverse TPKX → MBTiles recovery as the production shortcut.

---

## 4. Frozen Factory baseline versus TEST branches

### v1.0.0

TPKX Map Factory v1.0.0 is **RELEASE-ACCEPTED / FROZEN**.

Do not silently modify or reconstruct that exact accepted package.

### Later output-choice branches

Later TEST branches introduced combinations of:

```text
TPKX
MBTiles
REST
```

These branches do not redefine the frozen baseline until they pass the applicable live target acceptance.

### v1.4.0 REST-seed experiment

A production-scale v1.3 Static REST WMTS run exposed the cost of handling hundreds of thousands of loose files and then packaging/copying them.

v1.4.0 TEST changed the experimental REST transport to:

```text
verified MBTiles
→ <map>_REST.restmap
→ move one compact seed
→ expand runtime Static REST WMTS tree at final SSD
```

The `.restmap` seed remains internally a valid SQLite/MBTiles-style database with unchanged raster payloads. The small lifecycle fixture passed self-test.

This remains a TEST branch and is no longer the primary mobile deployment path.

---

## 5. Personal Android deployment

The current preferred human-facing path is local removable storage.

```text
TPKX
→ microSD
→ Android
→ map app
```

### ArcGIS Earth Mobile

Local TPKX has been **LIVE-PROVEN on multiple project packages**.

### ArcGIS Field Maps

Esri documents sideloaded TPKX basemaps on Android device storage or microSD.

Documented Android basemap folder:

```text
\Android\data\com.esri.fieldmaps\files\basemaps
```

Project status:

- vendor support: **DOCUMENTED**;
- Offline GeoStack real-phone Field Maps acceptance: **PENDING**.

A Field Maps live test must verify local basemap visibility/selection, offline pan/zoom, own position, and restart behavior on the intended phone.

### Cellular-data boundary

The target audience may use personal phones and personal data plans.

Esri documents that the Field Maps in-app Cellular Data option does not block every cellular-data use. To block Field Maps cellular traffic entirely on Android, use the device app-level network control and set Field Maps to Wi-Fi only.

The normal phone can retain cellular service while Field Maps is prevented from consuming the personal data plan.

---

## 6. Card-sizing model

Do not estimate the final deployment menu from source file megabytes alone.

Current practical coverage ladder:

```text
district      → Z17
county        → Z18
State Forests / selected hotspots → Z20
```

Where card capacity permits, Google Hybrid and Esri imagery/labels may coexist as alternate views.

Final tiers are chosen from real finished byte counts.

The underlying scaling matters: over the same ground area, one additional raster zoom level can create roughly four times as many deepest-level tile positions.

---

## 7. Map Fountain — accepted proof, parked deployment

Map Fountain proved that a deliberately dumb consumer router could serve useful map bytes without becoming a GIS server.

### Windows — LIVE-PROVEN

```text
native TPKX
→ USB SSD
→ GL.iNet Flint 2
→ Samba / SMB
→ private Wi-Fi or Ethernet
→ Windows
→ ArcGIS Earth
```

Production-scale specimen:

- `ESG1N.tpkx`;
- benchmark-observed size: **26,174,899,216 bytes**;
- Windows File Explorer identification: **25,561,426 KB**.

Ethernet benchmark:

- random seek: 25.33 MiB/s;
- random average latency: 9.34 ms;
- random p95: 9.98 ms;
- four-client aggregate: 51.21 MiB/s;
- sequential sample: 42.58 MiB/s.

Wi-Fi benchmark:

- random seek: 5.19 MiB/s;
- random average latency: 46.36 ms;
- random p95: 50.56 ms;
- four-client aggregate: 5.31 MiB/s;
- sequential sample: 6.14 MiB/s.

The decisive proof was application behavior: ArcGIS Earth opened and rendered the same TPKX directly from the router share over Wi-Fi.

### Android — LIVE-PROVEN

```text
Static REST WMTS
→ USB SSD
→ Flint 2 local HTTPS/WebDAV
→ Wi-Fi
→ ArcGIS Earth Mobile
```

That path passed, including cache-clear/restart retesting.

### Current disposition

Map Fountain is **parked from the primary personal-phone path**.

Potential future role: Starlink-connected basecamp storage / poor-man's NAS.

---

## 8. Packet-analysis boundary

The tested Windows SMB session used SMB3 encryption.

Wireshark can still validate:

- endpoints;
- timing;
- traffic volume;
- connection continuity;
- resets;
- TCP-visible retransmission behavior;
- overall traffic shape.

Without SMB session keys it cannot decode individual encrypted file-read commands.

The controlled benchmark supplies logical request timing; Wireshark validates transport; the real viewer decides application acceptance.

---

## 9. ArcGIS Earth runtime

ArcGIS Earth remains the current terrestrial chart plotter and one of the primary operational viewers.

Live-proven / observed capabilities include:

- native local TPKX;
- native TPKX opened directly from router Samba storage;
- local TPKX on ArcGIS Earth Mobile for compatible packages;
- KML / KMZ / NetworkLinks;
- native GNSS/NMEA own-position display;
- local Automation API;
- native drawings/markers;
- session restoration of loaded desktop TPKX files.

---

## 10. Live field positioning

### Native GNSS

Known-good live observation:

- 9600 baud;
- GLL and RMC NMEA sentences;
- ArcGIS Earth native blue-dot own position.

### PRAVE

The `$PRAVE` decoder has a LIVE-PROVEN ArcGIS Earth Automation API path. Controlled traffic displayed six native ArcGIS Earth unit drawings using the established RSSI fire-truck icon family.

### F22 / QR / KML

Remain designed or interoperable input paths around the same runtime. Do not create a second viewer merely because the transport differs.

---

## 11. Four-project separation

### Offline GeoStack

Owns the master field-mapping architecture and TPKX manufacturing lineage.

### Rasta Pyramid Factory

Owns general arbitrary-raster pyramid manufacturing.

### Map Fountain

Owns the historical/proven router/network-storage delivery evidence and any future shared-storage/basecamp revival.

### Android Field Maps + ArcGIS Earth

Owns the final personal-phone/microSD deployment workflow and normal-user procedure.

This separation prevents yesterday's exploration branch from becoming tomorrow's accidental architecture.

---

## 12. Offline boundary

There can be no operational dependence on public Internet connectivity.

Private local networking is allowed when useful. Direct local storage is preferred when it solves the job more simply.

Online services may assist manufacturing, imagery refresh, or optional enhancements. They must not be the only place the prepared field basemap exists.

---

## 13. Do-not-regress rules

1. Keep TPKX Map Factory v1.0.0 frozen.
2. Keep the proven MBTiles → TPKX converter stable unless a verified defect is established.
3. Do not revive rejected TPKX → MBTiles recovery as a production shortcut.
4. Do not require Map Fountain/router infrastructure for the normal personal-phone path.
5. Do not make public Internet part of the core map path.
6. Do not confuse vendor documentation with project live proof.
7. Do not bury the normal user under GIS features they did not ask for.
8. Keep exact file sizes/build evidence for deployment planning.
9. Do not confuse cache/read-ahead throughput with raw network speed.
10. Change one major test variable at a time.
11. Let the real target application decide acceptance.

> **Manufacture the geography once. Put the bytes where the user will need them.**
