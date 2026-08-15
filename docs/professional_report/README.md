# Offline GeoStack — Professional GIS Engineering Record

**Audience:** GIS professionals, software engineers, technical reviewers, and future AI systems.

This directory is the Markdown publication of the long-form engineering record produced at the **TPKX Map Factory v1.0.0 release-accepted milestone** on 15 August 2026.

The report is intentionally more detailed than the root README. It records the architecture, binary-format mechanics, production workflow, live acceptance evidence, operational doctrine, project lineage, and explicit do-not-regress rules needed to reconstruct the system without repeating the original archaeology.

## Read in order

1. [Architecture and QGIS](01_ARCHITECTURE_AND_QGIS.md)  
   Master architecture, historical pivot, v1.0 package anatomy, QGIS rendering stage, evidence standard.

2. [Converter and Pipeline](02_CONVERTER_AND_PIPELINE.md)  
   Coordinate handling, MBTiles intermediate, TMS row conversion, Compact Cache V2 binary structure, precision audit, verification, cleanup, advanced converter, human-factor GUI design.

3. [Validation, Runtime, and AI Engineering](03_VALIDATION_RUNTIME_AND_AI.md)  
   Release evolution, large live acceptance results, ArcGIS Earth runtime, Persistent Geographic Context, PRAVE Automation API integration, GNSS/F22/QR/KML paths, deployment/security boundaries, AI-assisted engineering methodology.

4. [Future Work, Appendices, and References](04_FUTURE_APPENDICES_AND_REFERENCES.md)  
   Future extension paths, do-not-regress rules, canonical settings, converter formulas, exact v1.0 smoke-package inspection, status matrix, official technical references, and the release baseline.

## Master system identity

**Offline GeoStack — QGIS → TPKX → ArcGIS Earth + Live Field Positioning**

`TPKX Map Factory` remains the name of the map-manufacturing subsystem. `ArcGIS Earth` remains the primary runtime/viewer. The repository slug `Google-Maps-Dispatch-System` is historical lineage rather than the current master product identity.

## Evidence rule

This project distinguishes:

- **CONCEPTUAL**
- **DESIGNED**
- **BUILT / SELF-TESTED**
- **BENCH-PROVEN**
- **LIVE-PROVEN**
- **RELEASE-ACCEPTED**

A plausible implementation is not promoted to LIVE-PROVEN until it answers to the real target system.

For TPKX output, **ArcGIS Earth is the final operational acceptance authority**.
