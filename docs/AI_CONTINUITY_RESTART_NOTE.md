# OFFLINE GEOSTACK — AI CONTINUITY / RESTART NOTE

This repository is intended to be understandable by future human maintainers and future AI systems without silently reviving superseded architecture.

## Master identity

**Offline GeoStack — QGIS → MBTiles / TPKX → ArcGIS Earth Desktop + Mobile + Live Field Positioning**

The repository is now actually named `Offline-GeoStack`. Older Google Maps Dispatch System names are lineage only.

## Current truth — 2026-08-16

The accepted v1.0.0 desktop map baseline remains frozen:

```text
QGIS 3.44.9
→ raster MBTiles
→ custom MBTiles → TPKX converter
→ Esri Compact Cache V2 / .tpkx
→ ArcGIS Earth Windows
```

A second local mobile delivery path is now **LIVE-PROVEN**:

```text
raster MBTiles on Windows PC / SSD
→ local HTTPS WMTS
→ Android USB tether / Remote NDIS
→ ArcGIS Earth Mobile
```

ArcGIS Earth is abbreviated **AE** throughout current project work.

## Evidence-status snapshot

- TPKX Map Factory v1.0.0: **RELEASE-ACCEPTED / LIVE-PROVEN**.
- MBTiles → TPKX frozen converter: **LIVE-PROVEN**.
- ArcGIS Earth Windows local TPKX: **LIVE-PROVEN**.
- ArcGIS Earth Mobile local TPKX: **LIVE-PROVEN on multiple packages**.
- USB Map Fountain v0.2.1 TEST: **LIVE-PROVEN**.
- Map Fountain with outside Internet removed: **LIVE-PROVEN**.
- Three different substantial MBTiles through Map Fountain: **LIVE-PROVEN**.
- Native Windows AE GNSS with actual receiver: **LIVE-OBSERVED**, known-good 9600 baud with GLL + RMC present.
- PRAVE → AE Automation API: **LIVE-PROVEN**.
- TPKX Map Factory v1.2.0 TEST: **BUILT / SELF-TESTED; Windows live acceptance underway**.
- TPKX → MBTiles recovery: **REJECTED as production path** after mobile visual defects in a recovered production map.

## Hard requirement

> There can be no operational dependence on Internet connectivity. Period.

This means **outside/public Internet dependency**. It does not prohibit a private local data link.

Both of these satisfy the doctrine:

```text
local TPKX already on device
```

and

```text
local map depot
→ private USB/local link
→ local WMTS
→ ArcGIS Earth Mobile
```

The USB Map Fountain path was specifically observed working after outside Internet connectivity was removed.

## Current desktop/mobile map architecture

The MBTiles stage has become a useful branch point rather than merely disposable manufacturing material:

```text
QGIS
→ verified raster MBTiles
    ├─→ frozen converter → TPKX → ArcGIS Earth local file
    └─→ Map Fountain → HTTPS WMTS → Android USB tether → ArcGIS Earth Mobile
```

## TPKX Map Factory v1.2 direction

v1.2 TEST exposes normal output choices:

```text
TPKX
MBTiles
Both
```

`Both` is the current TEST default so one QGIS-manufactured tile pyramid can support both local TPKX use and Map Fountain use.

The accepted v1.0.0 baseline remains separate and frozen. Do not silently overwrite history and call v1.2 accepted until the real Windows target accepts it.

## Map Fountain operator lesson

v0.2.1 fixed a stale-cache problem by assigning each selected MBTiles a unique service/map ID and unique tile URL namespace.

Live operator behavior:

> Deliberate pan/zoom is smooth and reliable. Rapid repeated zooming or whipping the view around can outrun the current mobile delivery/render path.

Do not erase this observation merely because later hardware seems faster; re-test before changing operator guidance.

## TPKX recovery lesson

A reverse Compact Cache V2 recovery experiment could reproduce exact tile bytes in a controlled fixture. That did **not** establish production suitability.

A recovered production MBTiles later showed blurred/missing regions on ArcGIS Earth Mobile.

Decision:

- recovery is not the production path;
- the tool was removed from v1.2;
- rebuild important MBTiles directly from QGIS;
- preserve MBTiles going forward when mobile Map Fountain use is expected.

This is an important example of why byte-level internal success does not replace target-viewer acceptance.

## Acceptance authority

For TPKX, the intended ArcGIS Earth runtime remains the operational authority.

For mobile Map Fountain, acceptance requires all of the following:

- selected MBTiles is actually the map being served;
- ArcGIS Earth Mobile consumes the service;
- requested tiles return correctly;
- visual result is correct through useful zoom/pan;
- outside Internet removal does not break the local path.

## Do not regress

- Do not return Google Earth Pro to primary-viewer status by inertia.
- Do not present KML Super Overlay / Blooming Onion as the current basemap architecture.
- Do not casually rewrite the frozen MBTiles→TPKX converter.
- Do not revive TPKX→MBTiles recovery as a production shortcut without solving and live-proving the defect.
- Do not discard MBTiles automatically when the operator may need Map Fountain deployment.
- Do not reintroduce removed Neighbor Extent/Grid-ID complexity into the normal-user Factory.
- Keep advanced GIS freedom through existing-MBTiles → TPKX.
- Retain KML for interoperability, NetworkLinks, external feeds, and saved content.
- Do not turn incidental multi-client capability into a supported multi-user product claim.
- Do not show `FINISHED`, a full progress bar, or `COMPLETE` before final verification/publishing is actually done.

## Current known-good environment

- Windows 10/11 64-bit
- Python 3.14.5
- QGIS 3.44.9
- ArcGIS Earth Windows
- ArcGIS Earth Mobile Android
- Factory raster recipe: PNG, 96 DPI, antialiasing ON, metatile 4, Z0–Z20

No additional Python libraries are required by the frozen TPKX converter path.

## Proven paths

1. Frozen normal Factory: source → area → zoom → QGIS → MBTiles → TPKX → AE Windows.
2. Advanced Factory: existing raster MBTiles → TPKX → AE Windows.
3. Local Android file: compatible TPKX → ArcGIS Earth Mobile.
4. Mobile Map Fountain: MBTiles → HTTPS WMTS → USB tether → ArcGIS Earth Mobile.
5. PRAVE → ArcGIS Earth Automation API with native drawings / RSSI fire-truck icons.
6. Native AE GNSS own-position on Windows.

## Persistent Geographic Context

Current operational language uses **Persistent Geographic Context**: keeping position, surroundings, routes, and terrain continuously visible and available without relying on a public-network request at showtime.

## Historical archive rule

Legacy Google Earth, KML forest/Blooming Onion, Network Earth, and Google Earth Enterprise work is technically valuable lineage. Preserve it as history. Do not treat old material as current merely because it exists.

## Binary-release truth

The exact accepted `TPKX_MAP_FACTORY_v1_0_0.zip` remains preserved in the canonical project archive. A connector-truncated GitHub copy was removed. Do not mistake v1.2 TEST, a reconstructed archive, or a partial upload for the release-accepted binary.

## Cold-start reading order

1. `README.md`
2. `docs/ARCGIS_EARTH_MOBILE_MAP_FOUNTAIN.md`
3. `ROADMAP.md`
4. `CHANGELOG.md`
5. `docs/TECHNICAL_ARCHITECTURE.md`
6. `docs/PRAVE_ARCGIS_EARTH_INTEGRATION.md`
7. `releases/README.md`
8. newest commits / issues

Report the current status before changing behavior.
