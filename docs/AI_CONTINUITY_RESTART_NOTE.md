# OFFLINE GEOSTACK — AI CONTINUITY / RESTART NOTE

This repository is intended to be understandable by future human maintainers and future AI systems without silently reviving superseded architecture.

## Master identity

**Offline GeoStack — QGIS → MBTiles / TPKX → offline field deployment + live field positioning**

The repository is named `Offline-GeoStack`. Older Google Maps Dispatch System / Google Earth names are lineage only.

ArcGIS Earth is abbreviated **AE** throughout project work.

---

## Current truth — 2026-08-18

The accepted desktop map-manufacturing baseline remains frozen:

```text
QGIS 3.44.9
→ raster MBTiles
→ custom MBTiles → TPKX converter
→ Esri Compact Cache V2 / .tpkx
→ ArcGIS Earth Windows
```

The current personal-phone deployment direction is now simpler than the router experiments:

```text
finished TPKX
→ microSD card
→ Android
→ ArcGIS Field Maps / ArcGIS Earth
```

The complicated work belongs on the map-maker side. The field user should receive a prepared card and a very short procedure.

The Android deployment work has its own repository:

`Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-`

---

## Evidence-status snapshot

- TPKX Map Factory v1.0.0: **RELEASE-ACCEPTED / LIVE-PROVEN**.
- MBTiles → TPKX frozen converter: **LIVE-PROVEN**.
- ArcGIS Earth Windows local TPKX: **LIVE-PROVEN**.
- ArcGIS Earth Mobile local TPKX: **LIVE-PROVEN on multiple packages**.
- Native Windows AE GNSS with actual receiver: **LIVE-OBSERVED**, known-good 9600 baud with GLL + RMC present.
- PRAVE → AE Automation API: **LIVE-PROVEN**.
- Router-only Map Fountain Windows TPKX-over-SMB: **LIVE-PROVEN / PARKED REFERENCE**.
- Router-only Map Fountain Android Static REST WMTS: **LIVE-PROVEN / PARKED REFERENCE**.
- Field Maps Android TPKX sideload to device/microSD: **DOCUMENTED BY ESRI; PROJECT LIVE TEST PENDING**.
- Later TPKX Map Factory output/REST branches: **TEST branches; do not confuse with frozen v1.0.0**.
- TPKX Map Factory v1.4.0 `.restmap` seed lifecycle fixture: **SELF-TESTED; NOT RELEASE-ACCEPTED**.
- TPKX → MBTiles recovery: **REJECTED as production path** after mobile visual defects in a recovered production map.

---

## Hard requirement

> There can be no operational dependence on Internet connectivity. Period.

This means outside/public Internet dependency. It does not prohibit private local networking when useful.

The personal-phone direction makes the map path even more direct:

```text
local microSD
→ Android map app
```

Online access may be useful during manufacturing, imagery refresh, optional live information, or basecamp work. Loss of outside connectivity must not remove the user's prepared basemap.

---

## Current card-sizing experiment

Do not freeze capacity tiers until actual finished byte counts exist.

Current menu direction:

- district — Z17;
- county — Z18;
- State Forests / selected high-value areas — Z20;
- Google Hybrid and Esri imagery/labels where useful and storage permits.

The user values a smooth aerial/road perspective much more than a feature-heavy GIS interface. Do not solve a simplicity problem by adding layers and controls nobody asked for.

---

## Field Maps boundary

Esri documents Android sideloading of `.tpk` / `.tpkx` basemaps to device storage or microSD, including this Android folder:

```text
\Android\data\com.esri.fieldmaps\files\basemaps
```

A vendor-documented feature is not automatically this project's LIVE-PROVEN result.

The next Field Maps acceptance test must prove on a real target phone:

- known-good Factory TPKX on microSD;
- Field Maps sees/selects the local basemap;
- Field Maps is set to Wi-Fi only at the Android app level;
- Wi-Fi is removed;
- local imagery continues to pan/zoom;
- own-position behavior is checked;
- close/reopen persistence is checked.

Esri also documents that the in-app Field Maps Cellular Data setting is not a complete cellular block. For complete app cellular blocking on Android, use the device network setting and set ArcGIS Field Maps to Wi-Fi only.

---

## Factory baseline and later TEST work

### Frozen v1.0.0

Do not reconstruct, repack, or silently modify the exact release-accepted baseline.

### Direct MBTiles preservation

If MBTiles is needed, preserve the direct QGIS-built MBTiles. Do not revive reverse TPKX → MBTiles recovery as a production shortcut.

### REST experimentation

The router-only Android Map Fountain proof led to Static REST WMTS factory experiments.

A production-scale v1.3 giant-tree/ZIP run demonstrated unacceptable file-count and packaging overhead.

`TPKX_MAP_FACTORY_v1_4_0_TEST` changed that experimental path to:

```text
verified MBTiles
→ compact <map>_REST.restmap seed
→ transport one file
→ expand runtime WMTS tree at final SSD
```

The small actual-user-MBTiles lifecycle fixture passed and preserved tile bytes. This branch remains TEST and is no longer the primary mobile deployment priority now that local removable TPKX deployment is being pursued.

---

## Map Fountain — preserve the proof, not the obligation

Map Fountain produced two important live proofs.

### Windows

```text
native TPKX on USB SSD
→ GL.iNet Flint 2
→ Samba / SMB
→ Wi-Fi
→ ArcGIS Earth Windows
```

A production-scale `ESG1N.tpkx` opened and rendered directly from router-attached storage.

### Android

```text
Static REST WMTS
→ USB SSD
→ Flint 2 HTTPS/WebDAV
→ Wi-Fi
→ ArcGIS Earth Mobile
```

This also passed, including cache-clear/restart retesting.

Current disposition: **PARKED from the primary personal-phone deployment path.**

Possible future role: Starlink-connected basecamp storage / poor-man's NAS.

Do not reintroduce Map Fountain as required phone infrastructure merely because the proof exists.

---

## Rasta Pyramid Factory

Rasta is an independent sibling project for general raster-pyramid manufacturing.

Current live-proven baseline is v0.1.3 with gigapixel-class city imagery and smooth deep navigation.

A v0.1.4 TEST branch added independent TPKX / MBTiles / REST output selections. Its REST branch is experimental and should not be allowed to redefine Rasta's core mission.

Rasta can also supply optional deep-zoom imagery or other single-raster pyramids for spare SD-card capacity, but Rasta itself does not own Android deployment.

---

## Acceptance authority

For TPKX, the intended runtime decides acceptance.

For new Field Maps work, vendor documentation establishes plausibility; the actual Android phone decides project acceptance.

Use evidence labels consistently:

- DESIGNED
- BUILT / SELF-TESTED
- LIVE-OBSERVED
- LIVE-PROVEN
- RELEASE-ACCEPTED / FROZEN

Do not promote a path because it merely works in a self-test or is described in vendor documentation.

---

## Do not regress

- Do not return Google Earth Pro to primary-viewer status by inertia.
- Do not present KML Super Overlay / Blooming Onion as the current basemap architecture.
- Do not casually rewrite the frozen MBTiles→TPKX converter.
- Do not revive TPKX→MBTiles recovery as a production shortcut.
- Do not require a router/server for the normal personal-phone map path.
- Do not make public Internet mandatory.
- Do not make normal users understand QGIS/Python/CRS internals.
- Do not add GIS features simply because Field Maps exposes them.
- Do not confuse vendor-documented support with a project live proof.
- Do not show `FINISHED`, a full progress bar, or `COMPLETE` before final verification/publishing is actually done.
- Do not confuse Windows cache/read-ahead throughput with raw network speed.

---

## Current known-good environment

- Windows 10/11 64-bit
- Python 3.14.5
- QGIS 3.44.9
- ArcGIS Earth Windows
- ArcGIS Earth Mobile Android
- Factory raster recipe: PNG, 96 DPI, antialiasing ON, metatile 4, Z0–Z20

No additional Python libraries are required by the frozen TPKX converter path.

---

## Four-project map

1. `Offline-GeoStack` — master manufacturing/field mapping system.
2. `Rasta-Pyramid-Factory` — general giant-raster pyramid manufacturing.
3. `Map-Fountain` — live-proven router/storage delivery experiments; parked reference / possible future Starlink NAS.
4. `Android-Field-Maps-and-ArcGIS-Earth-` — personal-phone / microSD deployment and user procedure.

---

## Cold-start reading order

1. `README.md`
2. `ROADMAP.md`
3. `docs/TECHNICAL_ARCHITECTURE.md`
4. Android deployment repository `README.md`
5. `CHANGELOG.md`
6. `docs/PRAVE_ARCGIS_EARTH_INTEGRATION.md`
7. `releases/README.md`
8. Map Fountain only when router/network proof history matters
9. newest commits/issues

Report the current evidence status before changing behavior.

---

## Governing principle

> **Manufacture the geography once. Put it where the field user can reach it without asking the network for permission.**
