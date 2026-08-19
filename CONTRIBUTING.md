# Contributing to Offline GeoStack

Contributions, testing, technical review, interoperability work, and controlled field validation are welcome.

## Current Factory product line

**Offline Map Factory 1.0** is the current clean product direction.

Status: **BUILT / SELF-TESTED — LIVE ACCEPTANCE PENDING**.

Current normal operator feature set:

- four map sources;
- Z0–Z20;
- TPKX / MBTiles / Both;
- one Advanced Tool: existing MBTiles → TPKX;
- no REST / Static WMTS output.

The prior **TPKX Map Factory v1.0.0** remains RELEASE-ACCEPTED / FROZEN history. Do not transfer that release status automatically to the new product line.

## User-facing package rule

The public package root is intentionally limited to:

```text
OFFLINE MAP FACTORY 1.0 - Installation Guide.pdf
OFFLINE MAP FACTORY 1.0 - User Guide.pdf
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
RUN OFFLINE MAP FACTORY.bat
System Files\
```

Do not add loose Python files, test BATs, internal notes, or developer clutter to the operator-facing root. Internal support material belongs behind `System Files`.

## Do not regress the Factory

- do not reintroduce REST because historical branches contain it;
- do not reintroduce Neighbor Extent or Grid-ID complexity into the normal GUI;
- do not casually rewrite the proven MBTiles → TPKX converter;
- do not revive rejected TPKX → MBTiles recovery;
- do not add public-Internet dependence to essential field map use;
- do not modify reference QGZ projects in place during production;
- do not add features merely because QGIS/ArcGIS exposes them.

## Factory acceptance

Offline Map Factory 1.0 must pass the real target before release promotion:

- MBTiles-only build;
- TPKX-only build;
- Both build;
- Advanced MBTiles → TPKX;
- ArcGIS Earth display of the finished TPKX;
- correct location/cartography/zoom/navigation;
- correct cleanup and final-output state.

Fortification should follow observed defects or reliability needs rather than redesign the architecture preemptively.

## Evidence language

Use these labels literally:

- **DESIGNED**
- **BUILT / SELF-TESTED**
- **LIVE-OBSERVED**
- **LIVE-PROVEN**
- **RELEASE-ACCEPTED / FROZEN**

Do not promote a feature because it compiles, passes a fixture, or appears in vendor documentation.

## Android deployment

Current normal mobile direction:

```text
Factory-built TPKX
→ microSD
→ Android
→ ArcGIS Field Maps / ArcGIS Earth
```

Vendor documentation establishes plausibility. The real phone establishes project acceptance.

## Map Fountain

Map Fountain remains LIVE-PROVEN router/storage history and a parked reference, with a possible future Starlink/basecamp NAS role.

Do not make it mandatory phone infrastructure without a current operational reason.

## Source-data rights

The MIT license applies to original project code/documentation, not third-party imagery, labels, basemaps, vendor software, or services. Contributors remain responsible for source-specific licensing, caching, export, attribution, and redistribution rules.

> **Keep the Factory simple. Keep the package clean. Let evidence drive changes.**
