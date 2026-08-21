# Contributing to Offline GeoStack

Contributions, testing, technical review, interoperability work, and controlled field validation are welcome.

## Current Factory product line

**Offline Map Factory 1.0** is the current clean product direction.

Status: **BUILT / SELF-TESTED — RELEASE ACCEPTANCE BLOCKED ON TPKX CONFORMANCE**.

Current normal operator feature set:

- four map sources;
- Z0-Z20;
- TPKX / MBTiles / Both;
- one Advanced Tool: existing MBTiles -> TPKX;
- no REST / Static WMTS output.

The prior **TPKX Map Factory v1.0.0** remains RELEASE-ACCEPTED / FROZEN for its actual ArcGIS Earth acceptance target.

## Current verified defect

On 2026-08-20 ArcGIS Field Maps rejected a project-converter TPKX while accepting Esri's official `Usa.tpkx` through the same physical microSD and Designer workflow.

This is sufficient evidence to reopen the converter in a new repair line.

Do not edit or repackage the frozen historical release to hide the defect.

See:

- `docs/TPKX_FIELD_MAPS_CONFORMANCE_2026-08-20.md`

## Reference-first rule

For the repair:

> **Esri's official working TPKX is the reference implementation. Reproduce/conform to it before inventing an alternative.**

Avoid speculative metadata changes. Field Maps is the acceptance target for Field Maps compatibility.

## User-facing package rule

The public package root remains intentionally limited to:

```text
OFFLINE MAP FACTORY 1.0 - Installation Guide.pdf
OFFLINE MAP FACTORY 1.0 - User Guide.pdf
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
RUN OFFLINE MAP FACTORY.bat
System Files\
```

Do not add loose Python files, test BATs, internal notes, or developer clutter to the operator-facing root. Internal support material belongs behind `System Files` or in repository development directories.

## Do not regress the Factory

- do not reintroduce REST because historical branches contain it;
- do not reintroduce Neighbor Extent or Grid-ID complexity into the normal GUI;
- do not rewrite the frozen historical converter artifact in place;
- do repair the converter in a new lineage because a verified Field Maps defect now exists;
- do not revive rejected TPKX -> MBTiles recovery;
- do not add public-Internet dependence to essential field map use;
- do not modify reference QGZ projects in place during production;
- do not add features merely because QGIS/ArcGIS exposes them;
- do not call ArcGIS Earth acceptance proof of Field Maps conformance.

## Current converter repair gate

`ESRI_CANONICAL_TPKX_TEST_v0_2_0` is BUILT / SELF-TESTED and copies Esri's canonical Web Mercator LOD values and metadata conventions.

The next acceptance is deliberately tiny:

```text
small MBTiles
-> canonical test converter
-> small TPKX
-> physical microSD basemaps folder
-> Field Maps
```

Only after that passes should the corrected converter be integrated into the Factory and Rasta.

## Factory acceptance after repair

Offline Map Factory 1.0 must pass the real target before release promotion:

- MBTiles-only build;
- TPKX-only build;
- Both build;
- Advanced MBTiles -> TPKX;
- ArcGIS Earth display of finished TPKX;
- representative Field Maps acceptance when that compatibility is claimed;
- correct location/cartography/zoom/navigation;
- correct cleanup/final-output state.

## Evidence language

Use these labels literally:

- **DESIGNED**
- **BUILT / SELF-TESTED**
- **LIVE-OBSERVED**
- **LIVE-PROVEN**
- **FAILED / NEEDS REPAIR**
- **RELEASE-ACCEPTED / FROZEN**

Do not promote a feature because it compiles, passes a fixture, appears in vendor documentation, or works in a more permissive consumer than the actual target.

## Android deployment

Current intended mobile direction after converter repair:

```text
corrected TPKX
-> ArcGIS Pro MMPK wrapper where needed
-> physical microSD
-> Android
-> ArcGIS Field Maps + ArcGIS Earth Mobile
```

The physical-card `basemaps` path and Esri official `Usa.tpkx` are now LIVE-PROVEN in Field Maps.

## Map Fountain

Map Fountain remains LIVE-PROVEN router/storage history and a parked reference, with a possible future Starlink/basecamp NAS role.

Do not make it mandatory phone infrastructure without a current operational reason.

## Source-data rights

The MIT license applies to original project code/documentation, not third-party imagery, labels, basemaps, vendor software, or services. Contributors remain responsible for source-specific licensing, caching, export, attribution, and redistribution rules.

> **Keep the Factory simple. Conform to the real standard. Let evidence drive changes.**
