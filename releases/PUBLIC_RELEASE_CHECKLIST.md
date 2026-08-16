# Offline GeoStack — Public Release Checklist

This checklist records the release gates for the **TPKX Map Factory v1.0.0** baseline inside Offline GeoStack.

## Engineering / runtime gates — PASSED

- [x] GUI launches on Windows using the packaged BAT launcher.
- [x] Colored visual controls remain visible at the target screen size.
- [x] Manual decimal-degree GPS diagonal points populate a valid HOME EXTENT.
- [x] Normal Factory path completes a map build.
- [x] QGIS produces temporary raster MBTiles.
- [x] Proven converter builds TPKX.
- [x] Destination receives the finished TPKX product.
- [x] Advanced existing-MBTiles → TPKX path completes.
- [x] Large advanced conversion accepted by ArcGIS Earth.
- [x] Large Esri World / Google Labels Factory run accepted by ArcGIS Earth.
- [x] v1.0.0 small release smoke package accepted by ArcGIS Earth.
- [x] Version 1.0.0 feature freeze declared.
- [x] Required QGIS reference projects preserved and published.
- [x] Professional GIS/future-AI technical record published.
- [x] Offline GeoStack master project identity established.

## GitHub publication gates

- [x] Public README rewritten around current 2026 architecture.
- [x] Legacy Google Earth architecture clearly separated from current baseline.
- [x] MIT code/documentation license and third-party notice added.
- [x] Roadmap, changelog, contribution rules, and AI continuity notes published.
- [ ] **Exact release-accepted `TPKX_MAP_FACTORY_v1_0_0.zip` attached directly to GitHub.**
- [ ] Repository slug/About metadata renamed from historical `Google-Maps-Dispatch-System` to `Offline-GeoStack`.

The two unchecked items require GitHub UI capabilities not exposed by the connector used during the repository rebuild. They are tracked as repository issues.

## Acceptance rule

**ArcGIS Earth is the final operational acceptance authority for finished TPKX packages.**

## Change rule

New features belong in v1.1 or later unless a verified defect requires a maintenance release.
