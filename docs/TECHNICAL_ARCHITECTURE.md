# Offline GeoStack — Technical Architecture

## Purpose

This document records the **current** Offline GeoStack architecture after the 2026-08-17 router-only Map Fountain breakthrough.

Master identity:

**Offline GeoStack — QGIS → MBTiles / TPKX → ArcGIS Earth Desktop + Mobile + Live Field Positioning**

Canonical system drawing:

**[Factory / PC / Android router-only flowchart](https://github.com/Jim-dc95811/Map-Fountain/blob/main/docs/arcgis_system_router_flowchart_2026-08-17.svg)**

The field router is deliberately dumb. It stores and shares finished native map products. ArcGIS Earth supplies the GIS intelligence.

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
        ├─→ preserve MBTiles
        └─→ frozen Compact Cache V2 converter → native TPKX

WINDOWS FIELD DELIVERY — LIVE-PROVEN
native TPKX
        ↓
USB SSD
        ↓
GL.iNet Flint 2
        ↓
Samba / SMB
        ↓
private Wi-Fi or Ethernet
        ↓
Windows
        ↓
ArcGIS Earth

LIVE FIELD INPUTS
GNSS / PRAVE / F22 / QR / KML
        ↓
ArcGIS Earth native inputs / Automation API
```

No outside Internet connection is required for the proven Windows field map path.

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

MBTiles contains the already-rendered raster pyramid. It remains useful as both manufacturing material and a deliberate finished product.

The frozen forward converter changes the addressing/container structure without rerendering the map:

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

Current finished-product choices in later TEST branches:

```text
TPKX
MBTiles
Both
```

The accepted v1.0.0 Factory baseline remains frozen and separate from later TEST work.

---

## 4. Router-only Map Fountain

Current proven field appliance:

- GL.iNet Flint 2 (`GL-MT6000`);
- USB-attached SSD;
- stock Samba network storage;
- private Ethernet/Wi-Fi LAN;
- DHCP for ordinary clients.

The router does **not**:

- parse TPKX;
- understand map projections;
- query MBTiles SQLite;
- generate tiles;
- run Python;
- run a GIS server;
- rerender imagery.

Its job is:

```text
storage + local network + file sharing
```

ArcGIS Earth opens the native file through the normal Windows file interface.

---

## 5. 2026-08-17 large-file proof

Specimen:

- `ESG1N.tpkx`
- benchmark-observed size: **26,174,899,216 bytes**
- Windows File Explorer identification: **25,561,426 KB**
- accepted share path: `\\192.168.8.1\New TPKX\Esri and Label\ESG1N.tpkx`

### Ethernet benchmark

- random seek: **25.33 MiB/s**
- random average latency: **9.34 ms**
- random p95: **9.98 ms**
- four-client aggregate: **51.21 MiB/s**
- sequential sample: **42.58 MiB/s**

### Wi-Fi benchmark

- random seek: **5.19 MiB/s**
- random average latency: **46.36 ms**
- random p95: **50.56 ms**
- four-client aggregate: **5.31 MiB/s**
- sequential sample: **6.14 MiB/s**

Wi-Fi was substantially slower but completed cleanly.

The decisive proof was not the benchmark: **ArcGIS Earth opened the same TPKX directly from the router share over Wi-Fi and rendered/navigated the Jacksonville map.**

---

## 6. Packet-analysis boundary

The tested SMB session uses SMB3 encryption.

Wireshark can still validate:

- endpoints;
- timing;
- traffic volume;
- connection continuity;
- resets;
- TCP-visible retransmission behavior;
- overall traffic shape.

Without SMB session keys it cannot decode individual encrypted file-read commands.

The controlled benchmark supplies logical request timing; Wireshark validates the transport; ArcGIS Earth decides application acceptance.

---

## 7. DHCP / addressing rule

Normal consumers use DHCP.

Do not manually assign static IP addresses simply to consume maps.

The router supplies a predictable LAN/share address. If a future client needs a stable address for a separate service, prefer a router-side DHCP reservation over manual Windows static configuration.

---

## 8. ArcGIS Earth runtime

ArcGIS Earth is the current terrestrial chart plotter and primary operational viewer.

Live-proven / observed project capabilities include:

- native local TPKX;
- native TPKX opened directly from router Samba storage;
- local TPKX on ArcGIS Earth Mobile for compatible packages;
- KML / KMZ / NetworkLinks;
- native GNSS/NMEA own-position display;
- local Automation API;
- native drawings/markers;
- session restoration of loaded desktop TPKX files.

---

## 9. Live field positioning

### Native GNSS

Known-good live observation:

- 9600 baud;
- GLL and RMC NMEA sentences;
- ArcGIS Earth native blue-dot own position.

### PRAVE

The `$PRAVE` decoder has a LIVE-PROVEN ArcGIS Earth Automation API path. Controlled traffic displayed six native ArcGIS Earth unit drawings using the established RSSI fire-truck icon family.

### F22

F22 remains a designed input to the same common live-position abstraction.

### QR

QR remains useful for bounded dispatch/data input. Historical Map Fountain work also proved QR service loading, but that is not the current field map-delivery architecture.

---

## 10. Android — immediate next gate

ArcGIS Earth Mobile is the next router-only acceptance target.

Current truth:

- local-file TPKX on Android is LIVE-PROVEN on multiple packages;
- historical Windows HTTPS WMTS → Android USB tether is LIVE-PROVEN history;
- **router-only Android consumption from the Flint 2 SSD is not yet accepted.**

The next investigation should begin with the simplest client-compatible path available from the router-attached SSD over private Wi-Fi.

Do **not** revive Raspberry Pi / Pi-server architecture or the historical Windows WMTS server as the default solution. Add compatibility logic only if the real Android target demonstrates that it is necessary.

---

## 11. Historical Windows WMTS path

On 2026-08-16, before the router-only proof, the project demonstrated:

```text
MBTiles on Windows
→ local HTTPS WMTS
→ Android USB tether
→ ArcGIS Earth Mobile
```

That experiment established useful lessons about:

- local mobile networking;
- WMTS/TMS row handling;
- HTTPS acceptance;
- QR ingestion;
- per-map service identity and cache isolation;
- deliberate versus rapid navigation;
- operation with outside Internet removed.

Preserve those lessons as lineage and fallback reference material. Do not present that software path as the active field appliance.

---

## 12. Offline boundary

There can be no operational dependence on public Internet connectivity.

Private local networking is allowed and useful:

```text
local SSD
→ private router LAN
→ Samba
→ ArcGIS Earth
```

Online services may assist preparation or optional enhancement, but the core field map path must remain functional when outside connectivity disappears.

---

## 13. Do-not-regress rules

1. Keep the field appliance router-only unless real target evidence proves more is necessary.
2. Do not revive Raspberry Pi / Pi-server architecture in the active system.
3. Do not make public Internet part of the core map path.
4. Preserve native map products; do not rerender them in the router.
5. Keep the frozen MBTiles → TPKX converter stable unless a verified defect is established.
6. Do not revive rejected TPKX → MBTiles recovery as a shortcut.
7. Keep ordinary Eaters on DHCP.
8. Do not confuse Windows cache/read-ahead throughput with raw network speed.
9. Change one major variable at a time during controlled acceptance tests.
10. Let packet evidence validate the network and the real ArcGIS Earth runtime decide acceptance.

> **Keep the router dumb. Keep the maps native. Let ArcGIS Earth do the GIS work.**
