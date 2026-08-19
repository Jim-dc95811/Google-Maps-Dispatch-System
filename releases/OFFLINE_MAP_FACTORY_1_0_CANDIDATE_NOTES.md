# Offline Map Factory 1.0 — Candidate Notes

**Status: BUILT / SELF-TESTED — LIVE ACCEPTANCE PENDING**

Offline Map Factory 1.0 begins a new clean product line after the TPKX Map Factory / REST exploration era.

## Current operator feature set

- Google Earth
- Google Hybrid
- Esri World
- Esri World / Google Labels
- Z0–Z20
- TPKX / MBTiles / Both
- Advanced Tool: existing MBTiles → TPKX

## Deliberately removed

- REST / Static WMTS output
- QR/service generation
- router/Map Fountain runtime logic
- reverse TPKX → MBTiles recovery

## Finished distribution layout

```text
OFFLINE MAP FACTORY 1.0 - Installation Guide.pdf
OFFLINE MAP FACTORY 1.0 - User Guide.pdf
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
RUN OFFLINE MAP FACTORY.bat
System Files\
```

## Packaging standard

The user-facing root contains only the files the operator needs to see. Internal implementation/support material stays behind `System Files`.

## Internal validation completed

- Python compile checks;
- output-mode logic checks;
- controlled MBTiles → TPKX conversion test.

## Live acceptance still required

Before release promotion, prove on the real Windows/QGIS target:

1. MBTiles-only build;
2. TPKX-only build;
3. Both build;
4. Advanced MBTiles → TPKX;
5. produced TPKX opens/renders correctly in ArcGIS Earth;
6. cleanup/final-output behavior is correct.

Only then promote the exact package to LIVE-PROVEN / RELEASE-ACCEPTED.

## Historical distinction

The earlier **TPKX Map Factory v1.0.0** remains a separate RELEASE-ACCEPTED / FROZEN milestone from 2026-08-15. Its evidence status is preserved; it is not silently renamed into this new product line.
