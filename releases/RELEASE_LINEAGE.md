# Offline GeoStack — Release Lineage

## Current accepted baseline

**TPKX Map Factory v1.0.0 — RELEASE-ACCEPTED — 2026-08-15**

This is the frozen map-manufacturing baseline inside **Offline GeoStack**.

## Test lineage

The v0.1.x builds were controlled development / burn-in packages used to prove the architecture and should not be redistributed as though they are the current public release.

```text
standalone MBTiles → TPKX converter
        ↓
v0.1.0 integrated Factory proof
        ↓
v0.1.1–v0.1.3 source / GUI / recipe simplification
        ↓
v0.1.4 TEMP and destination-cleanup hardening
        ↓
v0.1.5 advanced existing-MBTiles path introduced
        ↓
v0.1.6 both normal + advanced large-run paths LIVE-PROVEN
        ↓
v1.0.0 public polish + exact release smoke test
        ↓
RELEASE-ACCEPTED
```

## Release discipline

v1.0.0 is feature-frozen. New capabilities belong in v1.1+ unless a verified defect requires a maintenance release.

Do not silently rebuild, re-zip, or modify the accepted source tree and call the result v1.0.0. The exact accepted Windows archive remains the canonical binary release artifact.

## Master project lineage

The map subsystem now belongs to:

**Offline GeoStack — QGIS → TPKX → ArcGIS Earth + Live Field Positioning**

Earlier Google Maps Dispatch System / Google Earth Pro material remains project history, not the current runtime baseline.
