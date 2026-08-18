# Offline GeoStack — Public Summary

**Offline GeoStack** is a Windows-first offline geospatial stack built around QGIS, raster MBTiles, native TPKX packages, and field deployment without operational dependence on the public Internet.

Its frozen TPKX Map Factory v1.0.0 uses **QGIS 3.44.9** as the rendering engine and a custom Python **MBTiles → Esri Compact Cache V2 / TPKX** bridge to manufacture native raster packages. ArcGIS Earth is a live-proven runtime, including local TPKX on Windows and multiple Android packages, native GNSS own-position, and a live-proven PRAVE Automation API path.

The current personal-phone deployment direction is deliberately simple:

```text
Factory-built TPKX
→ microSD card
→ Android
→ ArcGIS Field Maps / ArcGIS Earth
```

Esri documents sideloaded TPKX basemaps on Android/device microSD; Offline GeoStack's own Field Maps acceptance test is still pending. The target user does not need to learn QGIS or the Factory—the map maker manufactures and verifies the product, then hands over a prepared card and a short field procedure.

Sibling projects:

- **Rasta Pyramid Factory** — giant-raster / deep-zoom pyramid manufacturing.
- **Map Fountain** — live-proven router/storage delivery experiments, now parked from the primary personal-phone path and retained as proof / possible future Starlink-basecamp NAS work.
- **Android Field Maps + ArcGIS Earth** — final microSD deployment and normal-user workflow.

Operating doctrine:

> **Manufacture the geography once. Put it where the field user can reach it without asking the network for permission.**
