# Offline GeoStack — Professional GIS Engineering Record

> **HISTORICAL MILESTONE RECORD — TPKX Map Factory v1.0.0, 2026-08-15.** This report intentionally preserves the architecture and terminology at the release-accepted v1.0.0 milestone. For current project architecture, deployment direction, and evidence status, read the repository root `README.md`, `ROADMAP.md`, and `docs/AI_CONTINUITY_RESTART_NOTE.md` first.

**Audience:** GIS professionals, software engineers, technical reviewers, and future AI systems.

This directory is the Markdown publication of the long-form engineering record produced at the **TPKX Map Factory v1.0.0 release-accepted milestone** on 15 August 2026.

The report is intentionally more detailed than the root README. It records the architecture, binary-format mechanics, production workflow, live acceptance evidence, operational doctrine, project lineage, and explicit do-not-regress rules needed to reconstruct the v1.0.0 system without repeating the original archaeology.

## Read in order

1. [Architecture and QGIS](01_ARCHITECTURE_AND_QGIS.md)  
   Master architecture, historical pivot, v1.0 package anatomy, QGIS rendering stage, evidence standard.

2. [Converter and Pipeline](02_CONVERTER_AND_PIPELINE.md)  
   Coordinate handling, MBTiles intermediate, TMS row conversion, Compact Cache V2 binary structure, precision audit, verification, cleanup, advanced converter, human-factor GUI design.

3. [Validation, Runtime, and AI Engineering](03_VALIDATION_RUNTIME_AND_AI.md)  
   Release evolution, large live acceptance results, ArcGIS Earth runtime, Persistent Geographic Context, PRAVE Automation API integration, GNSS/F22/QR/KML paths, deployment/security boundaries, AI-assisted engineering methodology.

4. [Future Work, Appendices, and References](04_FUTURE_APPENDICES_AND_REFERENCES.md)  
   Future extension paths as understood at the v1.0 milestone, do-not-regress rules, canonical settings, converter formulas, exact v1.0 smoke-package inspection, status matrix, official technical references, and the release baseline.

## Master system identity at this milestone

**Offline GeoStack — QGIS → TPKX → ArcGIS Earth + Live Field Positioning**

`TPKX Map Factory` remains the name of the map-manufacturing subsystem. ArcGIS Earth was the primary runtime/viewer at the v1.0.0 milestone.

The repository itself has since been renamed `Offline-GeoStack`, and the project has continued to evolve beyond this report. Current personal-phone deployment work now lives in the sibling **Android Field Maps + ArcGIS Earth** repository, while Map Fountain is preserved as a successful router/storage proof and Rasta Pyramid Factory remains the giant-raster manufacturing sibling.

Do not rewrite the body of this report every time the live architecture changes. Its value is that it freezes the v1.0.0 engineering state accurately.

## Evidence rule

This project distinguishes:

- **CONCEPTUAL**
- **DESIGNED**
- **BUILT / SELF-TESTED**
- **LIVE-OBSERVED**
- **LIVE-PROVEN**
- **RELEASE-ACCEPTED**

A plausible implementation is not promoted to LIVE-PROVEN until it answers to the real target system.

For the TPKX v1.0.0 milestone, **ArcGIS Earth was the final operational acceptance authority**.

## Current reading handoff

After using this report for v1.0 detail, return to:

1. [`../../README.md`](../../README.md)
2. [`../../ROADMAP.md`](../../ROADMAP.md)
3. [`../AI_CONTINUITY_RESTART_NOTE.md`](../AI_CONTINUITY_RESTART_NOTE.md)
4. [`../PROJECT_STATUS_2026-08-18.md`](../PROJECT_STATUS_2026-08-18.md)

Those files define current project truth.
