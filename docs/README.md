# Offline GeoStack Documentation

![Offline GeoStack](offline_geostack_banner.svg)

This folder is the technical record for the current 2026 **Offline GeoStack** architecture:

**QGIS → verified raster MBTiles → native TPKX and/or local HTTPS WMTS → ArcGIS Earth Windows / Mobile → live field-position inputs.**

For the current block diagram, see [current_architecture.svg](current_architecture.svg).

## Start here

- **[Software & Downloads](SOFTWARE_AND_DOWNLOADS.md)** — official links for pinned QGIS 3.44.9, pinned Python 3.14.5, ArcGIS Earth, required QGIS projects, and the v1.0.0 release record.
- [Quick Start](QUICK_START.md) — clean-machine normal-user and advanced-user operation for the frozen baseline.
- **[ArcGIS Earth Mobile + USB Map Fountain](ARCGIS_EARTH_MOBILE_MAP_FOUNTAIN.md)** — live-proven Android local-TPKX and MBTiles→HTTPS-WMTS→USB-tether paths.
- [USB Map Fountain live proof — 2026-08-16](mobile_map_fountain_live_proof_2026-08-16.md) — concise evidence note.
- [Professional GIS Engineering Record](professional_report/README.md) — long-form architecture, implementation, validation, operational doctrine, appendices, and future-AI continuity reference.
- [Technical Architecture](TECHNICAL_ARCHITECTURE.md) — converter mechanics, TMS/Compact Cache V2 structure, workflows, acceptance evidence, and do-not-regress rules.
- [Technical FAQ](FAQ.md) — direct answers to the questions GIS developers are most likely to ask first.
- [Notes for GIS Professionals](NOTES_FOR_GIS_PROFESSIONALS.md) — condensed interoperability interpretation.
- [Project Status — 2026-08-15](PROJECT_STATUS_2026-08-15.md) — frozen v1.0 release checkpoint; use the root README/roadmap for 2026-08-16 mobile developments.
- [Offline Operation and Persistent Geographic Context](OFFLINE_OPERATION_AND_PERSISTENT_GEOGRAPHIC_CONTEXT.md) — why local maps are operational inventory rather than a fallback cache.
- [PRAVE → ArcGIS Earth Integration](PRAVE_ARCGIS_EARTH_INTEGRATION.md) — live-proven native Automation API path and RSSI display rules.
- [AI-Assisted Engineering Method](AI_ENGINEERING_METHOD.md) — how the human/AI closed-loop workflow compressed cross-domain engineering work.
- [AI Continuity / Restart Note](AI_CONTINUITY_RESTART_NOTE.md) — current baseline for future maintainers and future AI systems.
- [Historical Timeline](HISTORICAL_TIMELINE.md) — how the project moved from terrestrial chartplotter work through Google Earth and into Offline GeoStack.
- [Source and Licensing Note](SOURCE_AND_LICENSING_NOTE.md) — technical capability versus source-data rights.
- [Roadmap](../ROADMAP.md) — frozen baseline plus current mobile / v1.2 next gates.

## Current deployment split

The QGIS-manufactured MBTiles stage can now feed two proven families of use:

```text
MBTiles
  ├─→ frozen converter → TPKX → ArcGIS Earth local file
  └─→ local HTTPS WMTS → USB tether → ArcGIS Earth Mobile
```

The accepted v1.0.0 product remains TPKX. The later v1.2 TEST branch exposes `TPKX / MBTiles / Both` because MBTiles became useful as a deployment product for Map Fountain.

## Required production assets

The current QGIS reference projects are stored under [`../required_qgis_projects/`](../required_qgis_projects/).

The exact release-accepted Factory archive remains preserved in the canonical project archive. See [`../releases/README.md`](../releases/README.md) for the binary-release status. A connector-truncated GitHub copy was deliberately removed instead of leaving a bad public download.

## Legacy architecture

- [Legacy Google Earth README — 2026-07-23](LEGACY_GOOGLE_EARTH_README_2026-07-23.md)
- `legacy/` — preserved visual/history material from the earlier project phase.

The legacy material is intentionally preserved as engineering lineage. It is not the current baseline.

## Current operating rule

> **There can be no operational dependence on Internet connectivity. Period.**

Private local links such as USB tether / local WMTS are compatible with this rule; the live Map Fountain path was proven with outside Internet removed.

## Current engineering shorthand

> **QGIS makes the pixels. TPKX carries them locally; Map Fountain can serve them locally. ArcGIS Earth displays them.**
