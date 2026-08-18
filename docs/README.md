# Offline GeoStack Documentation

![Offline GeoStack](offline_geostack_banner.svg)

## Current architecture

```text
MAP MANUFACTURING
QGIS / Factory
→ MBTiles / TPKX

PERSONAL MOBILE DEPLOYMENT
TPKX
→ microSD
→ Android
→ ArcGIS Field Maps / ArcGIS Earth

OPTIONAL SHARED STORAGE HISTORY
TPKX / Static REST WMTS
→ Map Fountain router/SSD proof
```

The current normal-user mobile direction is **local removable storage**, not mandatory router infrastructure.

## Four-project family

- **[Offline GeoStack](../README.md)** — master field-mapping and TPKX manufacturing system.
- **[Rasta Pyramid Factory](https://github.com/Jim-dc95811/Rasta-Pyramid-Factory)** — giant raster / deep-zoom pyramid manufacturing.
- **[Map Fountain](https://github.com/Jim-dc95811/Map-Fountain)** — LIVE-PROVEN router/storage delivery experiments; parked from the primary personal-phone path, possible future Starlink/basecamp NAS.
- **[Android Field Maps + ArcGIS Earth](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-)** — microSD deployment, Field Maps acceptance work, cellular-data protection, and operator handoff.

## Current state

### TPKX manufacturing — LIVE-PROVEN / frozen baseline

```text
QGIS 3.44.9
→ raster MBTiles
→ frozen Compact Cache V2 converter
→ TPKX
```

TPKX Map Factory v1.0.0 remains RELEASE-ACCEPTED / FROZEN.

### ArcGIS Earth — LIVE-PROVEN / observed

- local native TPKX: LIVE-PROVEN;
- local TPKX on ArcGIS Earth Mobile: LIVE-PROVEN on multiple packages;
- PRAVE → AE Automation API: LIVE-PROVEN;
- native GNSS own-position: LIVE-OBSERVED.

### ArcGIS Field Maps + microSD — next real target gate

Esri documents TPKX basemaps copied directly to Android/device microSD. Project-specific live acceptance is still pending.

Current card-menu experiment:

- district Z17;
- county Z18;
- selected State Forest / high-value Z20;
- Google Hybrid and Esri imagery/labels where useful.

### Map Fountain — LIVE-PROVEN / PARKED REFERENCE

Both Windows native TPKX-over-SMB and Android Static REST WMTS router paths passed real-target acceptance. They remain engineering proof, not required personal-phone infrastructure.

## Start here

- **[Current Project Status — 2026-08-18](PROJECT_STATUS_2026-08-18.md)** — the fastest complete checkpoint for the four-project architecture, current deployment direction, and next gates.
- **[Offline GeoStack README](../README.md)** — current public architecture and status.
- **[Android deployment repository](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-)** — current personal-phone deployment direction.
- **[Software & Downloads](SOFTWARE_AND_DOWNLOADS.md)** — pinned QGIS 3.44.9, Python 3.14.5, ArcGIS Earth, required QGIS projects, and release records.
- [Quick Start](QUICK_START.md) — normal-user and advanced-user operation for the frozen v1.0 Factory baseline.
- [Professional GIS Engineering Record](professional_report/README.md) — long-form record frozen at the v1.0.0 milestone; historical baseline, not a substitute for current README/roadmap.
- [Technical Architecture](TECHNICAL_ARCHITECTURE.md) — current Factory/converter/runtime/deployment engineering record.
- [Technical FAQ](FAQ.md) — direct answers for GIS developers.
- [Notes for GIS Professionals](NOTES_FOR_GIS_PROFESSIONALS.md) — condensed converter/cartography interpretation.
- [Offline Operation and Persistent Geographic Context](OFFLINE_OPERATION_AND_PERSISTENT_GEOGRAPHIC_CONTEXT.md) — offline doctrine.
- [PRAVE → ArcGIS Earth Integration](PRAVE_ARCGIS_EARTH_INTEGRATION.md) — live-proven Automation API path and RSSI display rules.
- [AI-Assisted Engineering Method](AI_ENGINEERING_METHOD.md) — human/AI closed-loop method.
- [AI Continuity / Restart Note](AI_CONTINUITY_RESTART_NOTE.md) — current baseline and do-not-regress rules.
- [Historical Timeline](HISTORICAL_TIMELINE.md) — project lineage.
- [Source and Licensing Note](SOURCE_AND_LICENSING_NOTE.md) — technical capability versus source-data rights.
- [Roadmap](../ROADMAP.md) — current mobile/card gates and later work.

## Historical mobile/router material

The 2026-08-16 Windows-hosted WMTS documents and the 2026-08-17 router-only Map Fountain documents remain useful engineering evidence.

They are not the default personal-phone deployment architecture.

Do not delete them merely because the project simplified afterward. Clearly label history rather than erasing chronology.

## Current deployment principle

```text
Factory makes the map
→ local storage carries it
→ the target app consumes it
```

> **Have the data ready before the user asks the screen to move.**
