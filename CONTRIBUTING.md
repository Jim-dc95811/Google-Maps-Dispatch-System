# Contributing

Contributions, testing, technical review, and interoperability work are welcome.

## Current baseline

Before proposing a change, read:

- `README.md`
- `docs/TECHNICAL_ARCHITECTURE.md`
- `docs/AI_CONTINUITY_RESTART_NOTE.md`
- `CHANGELOG.md`

The current architecture is **QGIS → temporary raster MBTiles → TPKX → ArcGIS Earth**.

## Do not regress the public workflow

The normal-user Factory is intentionally simple. Advanced functionality should not force ordinary operators to understand GIS internals.

In particular:

- do not reintroduce Neighbor Extent or Grid-ID complexity into the normal GUI;
- do not make temporary MBTiles a normal public deliverable;
- do not casually rewrite the proven MBTiles → TPKX converter;
- do not restore Google Earth Pro as the primary viewer merely because historical code exists;
- do not add an operational Internet dependency to essential map use.

## Advanced GIS work

The supported escape hatch for advanced cartography is the **existing MBTiles → TPKX** path. Build the desired raster layer stack in QGIS, export suitable MBTiles, then convert/package it.

## Evidence language

Please distinguish clearly between:

- **DESIGNED** — architecture or behavior has been specified;
- **BUILT** — implementation exists;
- **BENCH-PROVEN** — controlled/synthetic testing passed;
- **LIVE-PROVEN** — accepted on the real target system or field hardware.

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

## Project character

The project favors:

- offline-first operation;
- locally controlled files;
- simple operator controls;
- reproducible behavior;
- open technical documentation;
- practical field proof over theoretical claims.
