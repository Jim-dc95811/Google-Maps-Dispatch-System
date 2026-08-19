# Offline GeoStack — Public Summary

**Offline GeoStack** is a Windows-first offline geospatial stack built around QGIS, raster MBTiles, native TPKX packages, and field deployment without operational dependence on the public Internet.

The current clean map-manufacturing product is **Offline Map Factory 1.0**.

Status: **BUILT / SELF-TESTED — LIVE ACCEPTANCE PENDING**.

It uses **QGIS 3.44.9** as the rendering engine and a proven Python **MBTiles → Esri Compact Cache V2 / TPKX** bridge.

Current Factory capability:

```text
4 map sources
Z0–Z20
TPKX / MBTiles / Both
Advanced MBTiles → TPKX
```

REST / Static WMTS output is not part of the current Factory.

The prior **TPKX Map Factory v1.0.0** remains a separate RELEASE-ACCEPTED / FROZEN historical milestone.

Current personal-phone deployment direction:

```text
Offline Map Factory TPKX
→ microSD
→ Android
→ ArcGIS Field Maps / ArcGIS Earth
```

ArcGIS Earth is already a live-proven runtime for local TPKX. Esri documents sideloaded TPKX basemaps for Field Maps on Android/microSD; Offline GeoStack's own Field Maps acceptance test remains pending.

Sibling projects:

- **Rasta Pyramid Factory** — giant-raster / deep-zoom pyramid manufacturing.
- **Map Fountain** — live-proven router/storage delivery experiments, now parked from the primary personal-phone path.
- **Android Field Maps + ArcGIS Earth** — final microSD deployment and normal-user workflow.

> **Manufacture the geography once. Put it where the field user can reach it without asking the network for permission.**
