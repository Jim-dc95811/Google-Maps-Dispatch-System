# Offline GeoStack — Notes for GIS Professionals

The shortest technical description of the current manufacturing system is:

> **QGIS performs the cartography. Raster MBTiles holds the finished tile pyramid. Offline Map Factory 1.0 either publishes that MBTiles directly or repackages the unchanged tile images into Esri Compact Cache V2 / TPKX.**

The converter is intentionally not a GIS renderer. It is an interoperability bridge.

## Current Factory line

**Offline Map Factory 1.0** is the current clean operator product.

Status: **BUILT / SELF-TESTED — LIVE ACCEPTANCE PENDING**.

Normal output choices:

```text
TPKX
MBTiles
Both
```

One Advanced Tool remains:

```text
existing raster MBTiles → TPKX
```

REST / Static WMTS output is not part of the current Factory.

The earlier **TPKX Map Factory v1.0.0** remains a separate RELEASE-ACCEPTED / FROZEN historical milestone.

## Separation of concerns

- **QGIS** — source handling, projection, rendering, labels, symbology, composition.
- **MBTiles** — raster tile-pyramid container; manufacturing handoff and first-class finished/interchange product when preserved.
- **Converter** — TMS row translation, Compact Cache V2 binary packaging, TPKX metadata.
- **TPKX** — compact native deployment package.
- **ArcGIS Earth / Field Maps** — downstream runtimes with different operational roles.
- **GNSS / PRAVE / F22 / QR / KML** — live or interoperable field inputs around the prepared basemap/runtime system.

## Advanced-user implication

A GIS professional can ignore the Factory's four canned source choices, build arbitrary raster cartography in QGIS, export compatible raster MBTiles, and use only the Advanced MBTiles → TPKX stage.

That remains the professional escape hatch rather than burdening the beginner-facing GUI with GIS internals.

## MBTiles preservation rule

If MBTiles will be useful downstream, preserve the direct QGIS-built MBTiles at manufacture time.

Do not use reverse TPKX → MBTiles recovery as a production shortcut. A recovered production MBTiles later showed blurred/missing regions on ArcGIS Earth Mobile even though controlled fixture work had looked promising.

Target acceptance outranks internal structural cleverness.

## Precision

The critical TMS-to-ArcGIS Y conversion and bundle addressing are integer operations:

```text
y_arcgis = (2^z - 1) - y_tms
```

The converter does not deliberately round tile coordinates or resample the raster imagery.

## Current validation state

Historical live acceptance includes:

- 271,497-tile advanced conversion → ArcGIS Earth PASS;
- 271,242-tile normal Esri World / Google Labels Factory build → PASS;
- historical TPKX Map Factory v1.0.0 release smoke test → PASS;
- production-scale TPKX at **25,561,426 KB** in Windows File Explorer opened directly from SMB/router storage over Wi-Fi → PASS.

Offline Map Factory 1.0 must still earn its own product-line acceptance through real MBTiles-only, TPKX-only, Both, and Advanced conversion runs.

## Current mobile deployment direction

```text
TPKX
→ microSD
→ Android
→ ArcGIS Field Maps / ArcGIS Earth
```

Esri documents TPKX sideloading to Android/device microSD for Field Maps. Offline GeoStack's own Field Maps target test is still pending, so keep vendor support and project acceptance separate.

## Map Fountain boundary

Map Fountain successfully proved both Windows native TPKX-over-SMB and Android Static REST WMTS router paths. It is now parked from the primary personal-phone workflow and retained as engineering evidence / possible future Starlink-basecamp shared storage.

## Operational doctrine

> **There can be no operational dependence on public Internet connectivity. Period.**

> **Keep the operator-facing Factory simple; expose professional complexity through controlled escape hatches instead of clutter.**
