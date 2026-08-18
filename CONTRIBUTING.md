# Contributing to Offline GeoStack

Contributions, testing, technical review, interoperability work, and controlled field validation are welcome.

## Current baseline

Before proposing a change, read:

- `README.md`
- `docs/README.md`
- `docs/TECHNICAL_ARCHITECTURE.md`
- `docs/AI_CONTINUITY_RESTART_NOTE.md`
- `CHANGELOG.md`
- `ROADMAP.md`
- the Android deployment repository
- Map Fountain only when router/network-storage history is relevant

Master project identity:

**Offline GeoStack — QGIS → MBTiles / TPKX → offline field deployment + live field positioning**

Current normal-user mobile direction:

```text
Factory-built TPKX
→ microSD card
→ Android
→ ArcGIS Field Maps / ArcGIS Earth
```

`TPKX Map Factory v1.0.0` remains RELEASE-ACCEPTED and frozen. New Factory functionality belongs in later TEST branches until it earns live target acceptance.

## Current deployment boundary

Local TPKX in ArcGIS Earth Mobile is LIVE-PROVEN on multiple project packages.

Esri documents sideloaded TPKX basemaps on Android/device microSD for ArcGIS Field Maps, but Offline GeoStack's own Field Maps phone acceptance is still pending.

Map Fountain's Windows TPKX-over-SMB and Android Static REST WMTS paths are both LIVE-PROVEN, but Map Fountain is parked from the primary personal-phone deployment direction.

Do not make yesterday's successful experiment tomorrow's mandatory architecture without a current operational reason.

## Do not regress the public workflow

The normal-user Factory and deployment procedure are intentionally simple. Advanced functionality should not force ordinary operators to understand GIS internals.

In particular:

- do not reintroduce Neighbor Extent or Grid-ID complexity into the normal GUI;
- do not casually rewrite the proven MBTiles → TPKX converter;
- do not revive rejected TPKX → MBTiles recovery as a shortcut;
- do not restore Google Earth Pro as the primary viewer merely because historical code exists;
- do not add an operational Internet dependency to essential map use;
- do not modify locked QGIS reference projects in place during production;
- do not invent protocol metadata the source protocol did not provide;
- do not require router/server infrastructure for the normal personal-phone map path;
- do not add Field Maps features merely because they exist if the target users do not need them.

## Advanced GIS work

The supported escape hatch for advanced cartography remains the **existing raster MBTiles → TPKX** path. Build the desired raster layer stack in QGIS, export suitable raster MBTiles, then convert/package it.

A proposed new cartographic recipe should be tested first on a small geographic area and visually accepted in the intended target application before being treated as production-ready.

## Android deployment work

The deployment repository is:

`Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-`

For microSD / Field Maps changes, record as applicable:

- phone model and Android version;
- Field Maps / ArcGIS Earth version;
- card capacity/filesystem;
- exact TPKX identity and Windows File Explorer size;
- whether the file was internal or microSD storage;
- whether Field Maps was restricted to Wi-Fi only;
- whether Wi-Fi was physically off during the proof;
- own-position behavior;
- close/reopen behavior;
- what was directly observed versus inferred.

Vendor documentation establishes a supported path. The real phone establishes project acceptance.

## Map Fountain work

Map Fountain is currently parked as proof/reference, with a possible future Starlink/basecamp NAS role.

If reopened, record:

- router model / relevant firmware state;
- storage device;
- exact Windows File Explorer map size;
- Ethernet versus Wi-Fi;
- DHCP/static-address state;
- Wireshark evidence when network behavior matters;
- real target application behavior;
- what was observed versus inferred.

## Live-position / protocol work

Preferred architecture for PRAVE, F22, QR, and future live inputs:

```text
protocol-specific decoder
        ↓
normalized unit / command state
        ↓
ArcGIS Earth live-position / Automation API layer
```

Do not create a second map renderer merely because the transport differs.

## Evidence language

Use explicit labels:

- **CONCEPTUAL** — candidate idea only;
- **DESIGNED** — architecture or behavior has been specified;
- **BUILT / SELF-TESTED** — implementation exists and internal tests pass;
- **LIVE-OBSERVED** — seen on the real target but not yet a frozen acceptance gate;
- **LIVE-PROVEN** — accepted on the real target system or field hardware;
- **RELEASE-ACCEPTED** — exact release package passed the defined live smoke test and was frozen.

Do not promote a feature because it merely compiles, passes a synthetic fixture, or appears in vendor documentation.

## Finished TPKX acceptance

A package should:

- open without complaint in the intended target;
- land in the correct geographic location;
- expose the expected zoom behavior;
- render the expected cartography;
- behave normally during navigation.

## Source-data rights

Code contributions and map-source configuration are separate issues. Contributors are responsible for respecting licensing, caching, attribution, export, and redistribution requirements that apply to any source data they configure or demonstrate.

The MIT license applies to original Offline GeoStack code/documentation, not third-party imagery or vendor software. See `NOTICE.md`.

## Project character

Offline GeoStack favors:

- offline-first operation;
- local control;
- simple operator controls;
- advanced-user escape hatches instead of beginner complexity;
- reproducible behavior;
- open technical documentation;
- practical field proof over theoretical claims;
- preserving live-proven components without making every proven component mandatory forever.
