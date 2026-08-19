# Offline GeoStack Roadmap

## Current Factory product line

**Offline Map Factory 1.0** is the current clean product direction.

Status: **BUILT / SELF-TESTED — LIVE ACCEPTANCE PENDING**.

Current operator feature set:

- 4 sources: Google Earth, Google Hybrid, Esri World, Esri World / Google Labels;
- map area by HOME EXTENT, Clipboard History diagonal points, or two manual GPS points;
- Z0–Z20;
- output choice: TPKX / MBTiles / Both;
- one Advanced Tool: existing MBTiles → TPKX;
- no REST / Static WMTS output in the current Factory.

The prior **TPKX Map Factory v1.0.0** remains a RELEASE-ACCEPTED / FROZEN historical milestone. Do not erase or relabel that acceptance record.

---

## Immediate Factory gate

Run Offline Map Factory 1.0 on the real Windows/QGIS target.

Acceptance sequence:

1. launch from `RUN OFFLINE MAP FACTORY.bat`;
2. verify both required QGZ references are found;
3. build a small **MBTiles-only** map;
4. build a small **TPKX-only** map;
5. build a small **Both** map;
6. run **Advanced MBTiles → TPKX**;
7. open the produced TPKX in ArcGIS Earth;
8. confirm expected location, cartography, zoom behavior, navigation, cleanup, and final output state.

Only after that passes should Offline Map Factory 1.0 be promoted to LIVE-PROVEN / RELEASE-ACCEPTED.

### Fortification after acceptance

Fortify only where evidence says it is useful. Candidates:

- failed/cancelled-build cleanup;
- existing-output protection;
- conservative free-space preflight for large jobs;
- final output verification;
- clear completion state only after publication/verification.

Do not redesign the proven manufacturing architecture while doing reliability work.

---

## Finished distribution standard

The public package top level is intentionally limited to:

```text
OFFLINE MAP FACTORY 1.0 - Installation Guide.pdf
OFFLINE MAP FACTORY 1.0 - User Guide.pdf
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
RUN OFFLINE MAP FACTORY.bat
System Files\
```

All internal implementation files stay behind `System Files`.

---

## REST / Static WMTS exploration — PARKED HISTORY

The Map Fountain Android proof triggered a series of REST/Static WMTS Factory experiments.

Those experiments established useful engineering lessons about giant file trees, packaging overhead, and compact `.restmap` transport seeds.

Current decision:

- preserve the history;
- do not include REST in Offline Map Factory 1.0;
- do not revive REST in the normal Factory unless a real target again demonstrates the need.

---

## Current primary field direction — local removable deployment

```text
Offline Map Factory TPKX
→ microSD card
→ Android
→ ArcGIS Field Maps / ArcGIS Earth
```

Deployment work lives in:

**[Android Field Maps + ArcGIS Earth](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-)**

### Map-size gates

Measure real finished products before freezing card tiers:

1. district-wide Z17;
2. county-level Z18;
3. selected State Forest / high-value Z20 areas;
4. Google Hybrid versus Esri imagery/labels where both are useful.

Record exact finished sizes and elapsed build times.

### Field Maps gate

Esri documents sideloaded TPKX basemaps on Android/device microSD. Project acceptance still requires a real-phone test proving local basemap selection, Wi-Fi-only app restriction, offline pan/zoom, own position, and close/reopen behavior.

---

## Map Fountain — proven / parked

Windows native TPKX-over-SMB and Android Static REST WMTS router paths are both LIVE-PROVEN.

Map Fountain remains proof/reference, not mandatory personal-phone infrastructure.

Possible future role: Starlink-connected basecamp storage / poor-man's NAS.

---

## Rasta Pyramid Factory

Rasta remains the sibling project for arbitrary giant rasters and deep-zoom imagery.

Current live-proven baseline: v0.1.3.

The v0.1.4 REST branch remains TEST history tied to Map Fountain exploration; Rasta's core value does not depend on REST.

---

## Field integration

- Native GNSS: **LIVE-OBSERVED**, 9600 baud, GLL + RMC present.
- PRAVE → ArcGIS Earth Automation API: **LIVE-PROVEN**.
- F22 / QR / KML: retain as bounded field/live/interoperability paths and expand only when real use demands it.

---

## Non-goals

- forcing ordinary field users to run the Factory;
- restoring REST to the clean Factory without a demonstrated need;
- requiring router/server infrastructure for normal personal-phone deployment;
- rebuilding QGIS;
- making public Internet mandatory;
- reviving Raspberry Pi / Pi-server architecture by default;
- using rejected TPKX recovery as a shortcut;
- adding features because they exist rather than because users need them.

## Governing rules

> **The real target decides acceptance.**

> **Keep the Factory simple. Keep the user-facing folder clean.**
