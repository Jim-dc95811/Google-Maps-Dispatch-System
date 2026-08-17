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
- the current Map Fountain repository

Master project identity:

**Offline GeoStack — QGIS → MBTiles / TPKX → router-only local delivery → ArcGIS Earth + Live Field Positioning**

Current field-map architecture:

```text
Factory makes native MBTiles / TPKX products
→ USB SSD stores them
→ consumer router shares them
→ ArcGIS Earth consumes them
```

`TPKX Map Factory v1.0.0` remains RELEASE-ACCEPTED and frozen. New Factory functionality belongs in later TEST branches until it earns live target acceptance.

## Current router-only boundary

Windows ArcGIS Earth direct network-hosted TPKX over Wi-Fi is LIVE-PROVEN.

ArcGIS Earth Mobile on the router-only architecture is the next acceptance gate.

Do not revive Raspberry Pi / Pi-server architecture or another active field GIS-server appliance by default. Add compatibility logic only after the real target demonstrates that a simpler client path is insufficient.

## Do not regress the public workflow

The normal-user Factory is intentionally simple. Advanced functionality should not force ordinary operators to understand GIS internals.

In particular:

- do not reintroduce Neighbor Extent or Grid-ID complexity into the normal GUI;
- do not casually rewrite the proven MBTiles → TPKX converter;
- do not revive rejected TPKX → MBTiles recovery as a shortcut;
- do not restore Google Earth Pro as the primary viewer merely because historical code exists;
- do not add an operational Internet dependency to essential map use;
- do not modify locked QGIS reference projects in place during production;
- do not invent protocol metadata the source protocol did not provide;
- do not turn the field router into a GIS computer;
- do not make ordinary Map Fountain Eaters use manual static IP configuration.

MBTiles and TPKX are both legitimate finished products in later TEST branches. Which one is useful depends on the accepted target workflow.

## Advanced GIS work

The supported escape hatch for advanced cartography remains the **existing raster MBTiles → TPKX** path. Build the desired raster layer stack in QGIS, export suitable raster MBTiles, then convert/package it.

A proposed new cartographic recipe should be tested first on a small geographic area and visually accepted in ArcGIS Earth before being treated as production-ready.

## Map Fountain work

For router/storage changes, record:

- router model / relevant firmware state;
- storage device;
- exact Windows File Explorer map size when identifying a production file;
- Ethernet versus Wi-Fi;
- DHCP/static-address state;
- Wireshark evidence when network behavior matters;
- real ArcGIS Earth behavior;
- what was observed versus inferred.

The intended viewer decides acceptance. A fast synthetic benchmark is not enough by itself.

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

Do not promote a feature because it merely compiles or passes a synthetic fixture.

## Finished TPKX acceptance

ArcGIS Earth is the project's final operational acceptance authority for TPKX output. A package should:

- open without complaint;
- land in the correct geographic location;
- expose the expected zoom behavior;
- render the expected cartography;
- behave normally during navigation.

For router-hosted TPKX, the file must remain on the router-attached SSD during the proof.

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
- preserving live-proven components until replacements earn the same acceptance status.
