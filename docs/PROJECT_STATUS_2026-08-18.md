# Offline GeoStack — Project Status — 2026-08-18

## Executive state

The project has reached a simpler deployment architecture than the router/server explorations that preceded it.

The current four-project family is:

1. **Offline GeoStack** — master field-mapping / TPKX manufacturing system.
2. **Rasta Pyramid Factory** — giant-raster / deep-zoom pyramid manufacturing.
3. **Map Fountain** — LIVE-PROVEN router/storage delivery experiments; now PARKED from the primary personal-phone path, with a possible future Starlink/basecamp NAS role.
4. **Android Field Maps + ArcGIS Earth** — current personal-phone / microSD deployment and normal-user procedure.

The active mobile deployment direction is:

```text
Factory-built TPKX
→ microSD card
→ Android phone
→ ArcGIS Field Maps / ArcGIS Earth
```

The field user should not need to learn QGIS, Python, projections, tile-pyramid internals, or converter mechanics.

---

## Frozen manufacturing baseline

### TPKX Map Factory v1.0.0

**Status: RELEASE-ACCEPTED / FROZEN**

Known-good environment:

- Windows 10/11 64-bit;
- QGIS 3.44.9;
- Python 3.14.5;
- PNG raster tiles;
- 96 DPI;
- antialiasing ON;
- metatile 4;
- Z0–Z20 operator-selectable.

Frozen normal source choices:

1. Google Earth
2. Google Hybrid
3. Esri World
4. Esri World / Google Labels

Frozen core chain:

```text
QGIS
→ raster MBTiles
→ custom Compact Cache V2 converter
→ TPKX
```

The exact accepted v1.0.0 archive must not be silently reconstructed or replaced by a later TEST package.

---

## Current map-card sizing experiment

The goal is not to make every user a GIS operator. The goal is to manufacture useful geography once, place it on removable storage, and let the phone read local bytes.

Current menu direction:

- **District — Z17**
- **County — Z18**
- **State Forests / selected high-value areas — Z20**
- Google Hybrid and Esri imagery/labels where both are useful and card capacity permits

Exact capacity tiers are not frozen. Real finished byte counts from Factory builds decide the card menu.

The storage strategy should support smaller personal cards as well as large cards; highest-value coverage goes on first.

---

## ArcGIS Earth status

### Windows local TPKX

**LIVE-PROVEN**.

### Android local TPKX

**LIVE-PROVEN on multiple project packages**.

### Native GNSS

**LIVE-OBSERVED** with actual receiver input at 9600 baud, GLL + RMC present, showing the operator's own-position blue dot.

### PRAVE

PRAVE → ArcGIS Earth Automation API is **LIVE-PROVEN** with native unit drawings and the established RSSI fire-truck icon family.

---

## ArcGIS Field Maps status

Esri documents sideloaded `.tpk` / `.tpkx` basemaps on Android device storage or microSD.

Documented Android basemap folder:

```text
\Android\data\com.esri.fieldmaps\files\basemaps
```

Current evidence state:

- vendor documentation: **DOCUMENTED BY ESRI**;
- Offline GeoStack / Android deployment project real-phone acceptance: **PENDING**.

The next real target test must prove:

1. a known-good Factory TPKX on microSD appears as an available local basemap;
2. the user can select it;
3. Field Maps is restricted to Wi-Fi only at the Android app level;
4. Wi-Fi is turned off;
5. imagery continues to pan and zoom from local storage;
6. own-position behavior is useful;
7. close/reopen behavior remains acceptable.

Do not call this project LIVE-PROVEN until the actual phone passes.

---

## Personal cellular-data rule

The deployment project treats protection of personal cellular data as a primary user requirement.

The Field Maps in-app Cellular Data setting is not treated as a complete app-level block. The practical Android procedure is to restrict ArcGIS Field Maps to **Wi-Fi only** using the phone's app network settings.

This allows ordinary phone cellular service to remain available while preventing Field Maps from consuming the user's personal cellular data plan.

The one-page printable quick guide is stored in the Android deployment repository.

---

## Map Fountain — successful proof, now parked

### Windows router path

**LIVE-PROVEN**:

```text
native TPKX on USB SSD
→ GL.iNet Flint 2
→ Samba / SMB
→ Wi-Fi
→ ArcGIS Earth Windows
```

Accepted large specimen:

- `ESG1N.tpkx`
- 26,174,899,216 bytes by benchmark script
- 25,561,426 KB in Windows File Explorer

### Android router path

**LIVE-PROVEN**:

```text
Static REST WMTS
→ USB SSD
→ Flint 2 local HTTPS/WebDAV
→ Wi-Fi
→ ArcGIS Earth Mobile
```

Cache-clear / force-stop / reopen retest also passed.

### Current disposition

**PARKED from the primary personal-phone deployment path.**

Reason: direct removable TPKX storage is simpler for the target user.

Possible future role:

```text
Starlink
→ Flint 2 WAN
→ USB SSD
→ SMB / Wi-Fi / Ethernet
→ basecamp laptops / clients
```

That would be a poor-man's NAS / local incident map reservoir, not mandatory phone infrastructure.

---

## Factory REST exploration status

The Map Fountain Android proof led to Static REST WMTS manufacturing experiments.

A production-scale v1.3 branch exposed the cost of giant expanded file trees and packaging/copying them.

`TPKX_MAP_FACTORY_v1_4_0_TEST` changed the experimental transport to:

```text
verified MBTiles
→ compact <map>_REST.restmap seed
→ move one file
→ expand Static REST WMTS at final SSD
```

Small lifecycle fixture: **SELF-TESTED**.

This branch remains experimental and is no longer the current mobile priority while direct local TPKX / microSD deployment is being pursued.

---

## Rasta Pyramid Factory status

### v0.1.3 TEST

**LIVE-PROVEN baseline**.

Major proofs include Montreal, Tower Bridge, London gigapixel-class imagery, and Barcelona.

### v0.1.4 TEST

**BUILT / SELF-TESTED**, not yet the live-proven baseline.

Adds independent finished-product choices:

```text
TPKX
MBTiles
REST
```

The REST branch is experimental downstream work. Rasta's core mission remains general raster-pyramid manufacturing.

Possible Android-card use: spare card capacity can carry Rasta-generated deep-zoom imagery, historical scans, specialty maps, or other useful large rasters.

---

## Rejected production path

### TPKX → MBTiles recovery

**REJECTED**.

A controlled fixture could recover exact raster tile bytes, but a recovered production MBTiles later showed blurred/missing regions on ArcGIS Earth Mobile.

Production rule:

- preserve direct QGIS-built MBTiles if MBTiles is needed;
- do not reverse-recover important production MBTiles from TPKX.

---

## Human-factors rule

The public/user-facing workflow should stay short.

For the Android deployment audience:

> **Call Gaddy for a card. Read the cheat sheet. Go to work.**

Advanced overlays, MMPKs, geofences, forms, or other GIS features should be added only when real users demonstrate a need. Do not turn a useful map viewer into a training burden merely because the platform exposes more capability.

---

## Hard doctrine

> **There can be no operational dependence on public Internet connectivity. Period.**

Private local networking remains allowed when useful. Direct local storage is preferred when it solves the job more simply.

---

## Current next gates

1. Finish real district Z17 size measurement.
2. Finish real county Z18 size measurement.
3. Build representative State Forest / high-value Z20 products.
4. Compare Google Hybrid and Esri imagery/labels finished sizes and visual usefulness.
5. Run the first controlled ArcGIS Field Maps + microSD TPKX acceptance test.
6. Verify the Android Wi-Fi-only procedure protects the personal data plan while local imagery and GPS remain useful.
7. Freeze practical card tiers only after those real byte counts and phone tests exist.

---

## Governing principle

> **Manufacture the geography once. Put it where the field user can reach it without asking the network for permission.**
