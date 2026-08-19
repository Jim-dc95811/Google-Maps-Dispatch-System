# Offline Map Factory 1.0 — Acceptance Checklist

Current status: **BUILT / SELF-TESTED — LIVE ACCEPTANCE PENDING**.

Use this checklist before promoting the exact package to LIVE-PROVEN / RELEASE-ACCEPTED.

## Installation / launch

- [ ] Python 3.14.5 installed.
- [ ] QGIS 3.44.9 installed.
- [ ] `C:\Google Earth Project\QGIS\` exists.
- [ ] `REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz` present.
- [ ] `ESRI and Google Labels.qgz` present.
- [ ] `RUN OFFLINE MAP FACTORY.bat` launches the Factory.
- [ ] `System Files\` remains beside the BAT.

## Normal build modes

- [ ] MBTiles-only build completes.
- [ ] MBTiles output opens structurally/contains expected raster tiles.
- [ ] TPKX-only build completes.
- [ ] TPKX opens in ArcGIS Earth.
- [ ] Both build completes.
- [ ] Both outputs use the expected shared map name.

## Advanced Tool

- [ ] Existing MBTiles → TPKX completes.
- [ ] Advanced TPKX opens in ArcGIS Earth.

## ArcGIS Earth acceptance

- [ ] Correct geographic location.
- [ ] Expected cartography/source.
- [ ] Expected zoom range.
- [ ] Normal pan/zoom/navigation.
- [ ] No obvious missing/blurred/corrupt regions attributable to packaging.

## Reliability / cleanup

- [ ] COMPLETE appears only after final publication/verification.
- [ ] Success leaves only intended finished output(s) in the selected destination.
- [ ] Cancel does not leave misleading finished products.
- [ ] Failed build does not leave misleading finished products.
- [ ] Existing destination files are handled safely.

## Packaging / human factors

- [ ] Top level contains only the two PDF guides, two QGZ files, one BAT, and `System Files\`.
- [ ] No loose Python files at the package root.
- [ ] No test BATs at the package root.
- [ ] No developer README/test clutter at the package root.

## Promotion rule

When every required live gate passes, freeze the exact package and record:

- exact archive filename;
- exact Windows File Explorer size;
- SHA-256 if desired for archival identification;
- test map/source/extent/zoom/output mode;
- elapsed time;
- ArcGIS Earth result;
- date of acceptance.

Only then change the status to:

**RELEASE-ACCEPTED / FROZEN**.
