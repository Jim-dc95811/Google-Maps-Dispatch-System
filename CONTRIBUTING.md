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

Master project identity:

**Offline GeoStack — QGIS → TPKX → ArcGIS Earth + Live Field Positioning**

Current map architecture:

**QGIS → temporary raster MBTiles → TPKX → ArcGIS Earth**

`TPKX Map Factory v1.0.0` is RELEASE-ACCEPTED. New functionality should normally land in v1.1+ rather than destabilizing the accepted v1.0 baseline.

## Do not regress the public workflow

The normal-user Factory is intentionally simple. Advanced functionality should not force ordinary operators to understand GIS internals.

In particular:

- do not reintroduce Neighbor Extent or Grid-ID complexity into the normal GUI;
- do not make temporary MBTiles a normal public deliverable;
- do not casually rewrite the proven MBTiles → TPKX converter;
- do not restore Google Earth Pro as the primary viewer merely because historical code exists;
- do not add an operational Internet dependency to essential map use;
- do not modify locked QGIS reference projects in place during production;
- do not invent protocol metadata that the source protocol did not actually provide.

## Advanced GIS work

The supported escape hatch for advanced cartography is the **existing MBTiles → TPKX** path. Build the desired raster layer stack in QGIS, export suitable raster MBTiles, then convert/package it.

A proposed new cartographic recipe should be tested first on a small geographic area and visually accepted in ArcGIS Earth before being treated as a production source.

## Live-position / protocol work

The preferred architecture for PRAVE, F22, QR, and future live inputs is:

```text
protocol-specific decoder
        ↓
normalized unit / command state
        ↓
ArcGIS Earth live-position / Automation API layer
```

Do not create a second map renderer merely because the transport differs.

## Evidence language

Please distinguish clearly between:

- **CONCEPTUAL** — candidate idea only;
- **DESIGNED** — architecture or behavior has been specified;
- **BUILT** — implementation exists;
- **BENCH-PROVEN** — controlled/synthetic testing passed;
- **LIVE-PROVEN** — accepted on the real target system or field hardware;
- **RELEASE-ACCEPTED** — exact release package passed the defined live smoke test and was frozen.

Do not promote a feature to LIVE-PROVEN merely because it compiles or passes a synthetic fixture.

## Finished TPKX acceptance

ArcGIS Earth is the project’s final operational acceptance authority for TPKX output. A package should:

- open without complaint;
- land in the correct geographic location;
- expose the expected zoom behavior;
- render the expected cartography;
- behave normally during navigation.

## Source-data rights

Code contributions and map-source configuration are separate issues. Contributors are responsible for respecting licensing, caching, attribution, export, and redistribution requirements that apply to any source data they configure or demonstrate.

The MIT license in this repository applies to original Offline GeoStack code/documentation, not to third-party imagery or vendor software. See `NOTICE.md`.

## Project character

Offline GeoStack favors:

- offline-first operation;
- locally controlled files;
- simple operator controls;
- advanced-user escape hatches instead of beginner complexity;
- reproducible behavior;
- open technical documentation;
- practical field proof over theoretical claims;
- preserving live-proven components until replacements earn the same acceptance status.
