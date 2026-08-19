# Offline GeoStack Documentation

![Offline GeoStack](offline_geostack_banner.svg)

## The story behind the engineering

Before diving into implementation details, these pages explain why the project exists and what the long chain of experiments produced:

- **[The Journey of Ideas](JOURNEY_OF_IDEAS.md)** — field problems, dispatch, offline imagery, terrain judgment, and the human + AI engineering model.
- **[The Bridges We Had to Build](THE_BRIDGES_WE_HAD_TO_BUILD.md)** — the cross-domain interoperability bridges that connected radio, GIS, QR, networks, raster pyramids, and ArcGIS Earth.
- **[Wildland Imagery University](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-/blob/main/training/WILDLAND_IMAGERY_UNIVERSITY.md)** — imagery-based terrain-judgment training for firefighters.
- **[Contributors / collaboration model](../CONTRIBUTORS.md)** — explicit human and AI engineering roles.

## Current architecture

```text
MAP MANUFACTURING
Offline Map Factory 1.0
→ MBTiles / TPKX / Both

PERSONAL MOBILE DEPLOYMENT
TPKX
→ microSD
→ Android
→ ArcGIS Field Maps / ArcGIS Earth

WINDOWS ARCGIS EARTH FIELD FEATURES
PRAVE Live / QR Command Bridge
→ local Automation API / controlled local actions

OPTIONAL SHARED STORAGE HISTORY
Map Fountain router/SSD proofs
```

## Current Factory state

**Offline Map Factory 1.0** is the current clean Factory product line.

Status: **BUILT / SELF-TESTED — LIVE ACCEPTANCE PENDING**.

Current Factory:

- 4 sources;
- Z0–Z20;
- TPKX / MBTiles / Both;
- one Advanced MBTiles → TPKX tool;
- no REST / Static WMTS output.

The prior **TPKX Map Factory v1.0.0** remains a RELEASE-ACCEPTED / FROZEN historical milestone.

## Operator guides

- **[Offline Map Factory 1.0 — Installation Guide (PDF)](guides/OFFLINE_MAP_FACTORY_1_0_INSTALLATION_GUIDE.pdf)**
- **[Offline Map Factory 1.0 — User Guide (PDF)](guides/OFFLINE_MAP_FACTORY_1_0_USER_GUIDE.pdf)**
- [Quick Start — Markdown](QUICK_START.md)

## Four-project family

- **[Offline GeoStack](../README.md)** — master map manufacturing + field-system integration.
- **[Rasta Pyramid Factory](https://github.com/Jim-dc95811/Rasta-Pyramid-Factory)** — giant-raster / deep-zoom pyramid manufacturing.
- **[Map Fountain](https://github.com/Jim-dc95811/Map-Fountain)** — LIVE-PROVEN shared-storage/network delivery evidence; parked from the normal personal-phone path.
- **[Android Field Maps + ArcGIS Earth](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-)** — deployment to the user: Android offline maps + Windows ArcGIS Earth field features + imagery training.

## Start here

- **[The Journey of Ideas](JOURNEY_OF_IDEAS.md)**
- **[The Bridges We Had to Build](THE_BRIDGES_WE_HAD_TO_BUILD.md)**
- **[Current Project Status — 2026-08-18](PROJECT_STATUS_2026-08-18.md)**
- **[Offline GeoStack README](../README.md)**
- **[Software & Downloads](SOFTWARE_AND_DOWNLOADS.md)**
- **[Required QGIS Projects](../required_qgis_projects/)**
- **[Release / candidate records](../releases/README.md)**
- **[Offline Map Factory 1.0 Candidate Notes](../releases/OFFLINE_MAP_FACTORY_1_0_CANDIDATE_NOTES.md)**
- **[Technical Architecture](TECHNICAL_ARCHITECTURE.md)**
- **[AI Continuity / Restart Note](AI_CONTINUITY_RESTART_NOTE.md)**
- **[Android deployment repository](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-)**
- [Professional GIS Engineering Record](professional_report/README.md) — frozen v1.0.0 milestone record, not the current product front door.
- [PRAVE → ArcGIS Earth Integration](PRAVE_ARCGIS_EARTH_INTEGRATION.md)
- [Offline Operation and Persistent Geographic Context](OFFLINE_OPERATION_AND_PERSISTENT_GEOGRAPHIC_CONTEXT.md)
- [Historical Timeline](HISTORICAL_TIMELINE.md)
- [Source and Licensing Note](SOURCE_AND_LICENSING_NOTE.md)
- [Roadmap](../ROADMAP.md)

## Historical REST / router material

The Windows-hosted WMTS work, router-only Map Fountain proof, and v1.3/v1.4 REST Factory experiments remain useful engineering history.

They are not part of the current normal Factory product.

Do not delete the history. Do not present it as today's operator workflow.

## Current principle

```text
Factory makes the map
→ local storage carries it
→ target application consumes it
→ trained human interprets it
```

> **Keep the Factory simple. Keep the package clean. Keep the purpose visible.**
