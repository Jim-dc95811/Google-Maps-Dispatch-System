# Offline Map Factory 1.0 — Quick Start

**Status: BUILT / SELF-TESTED — RELEASE ACCEPTANCE BLOCKED ON TPKX CONFORMANCE**

## Important current warning

The QGIS -> MBTiles manufacturing path remains valid, but the historical MBTiles -> TPKX converter lineage failed a strict ArcGIS Field Maps test on 2026-08-20.

Field Maps rejected a project-built TPKX while accepting Esri's official `Usa.tpkx` through the same physical-card/Designer workflow.

Therefore:

- MBTiles output remains a valid current product/test path;
- historical TPKX output remains proven in ArcGIS Earth;
- do **not** treat the current Factory's historical converter as Field Maps-conformant;
- the Esri-canonical replacement converter is still awaiting Field Maps acceptance.

See `TPKX_FIELD_MAPS_CONFORMANCE_2026-08-20.md`.

## Install once

1. Install **Python 3.14.5 (64-bit)**.
2. Install **QGIS 3.44.9 (64-bit)**.
3. Create:

```text
C:\Google Earth Project\QGIS\
```

4. Copy these two supplied files into that folder with their exact names:

```text
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
```

5. Keep the Factory launcher and `System Files` folder together.

## Make a map

1. Double-click **RUN OFFLINE MAP FACTORY.bat**.
2. Choose one of four sources:
   - Google Earth
   - Google Hybrid
   - Esri World
   - Esri World / Google Labels
3. Choose the map area using HOME EXTENT, Clipboard History diagonal points, or two manual Latitude,Longitude points.
4. Choose minimum and maximum zoom, **Z0-Z20**.
5. Choose finished output: **TPKX**, **MBTiles**, or **Both**.
6. Click **BUILD MAP**.
7. Choose destination/name.
8. Review the build summary and begin.
9. Wait for **COMPLETE**.

## Output meaning

- **MBTiles** — verified raster tile master/interchange file; current manufacturing foundation.
- **TPKX** — Compact Cache V2 package; historical converter output is ArcGIS Earth-proven but currently under Field Maps conformance repair.
- **Both** — preserves the MBTiles and creates a matching TPKX with the converter currently in the build.

## Advanced Tool

The clean Factory has one Advanced Tool:

**existing MBTiles -> TPKX**

Until the canonical converter repair is integrated and accepted, use the same compatibility warning above.

## Current converter repair test

```text
small MBTiles
-> ESRI_CANONICAL_TPKX_TEST_v0_2_0
-> small new TPKX
-> physical microSD
-> ArcGIS Field Maps
```

Only after Field Maps accepts this small specimen should the new converter be integrated into the production Factory.

## Current boundary

Offline Map Factory 1.0 deliberately does **not** include REST / Static WMTS output. That remains parked Map Fountain history.

## Operational rule

> **Build or refresh maps before they are needed. Essential map use must not depend on public Internet connectivity.**

> **For compatibility claims, let the real target decide.**
