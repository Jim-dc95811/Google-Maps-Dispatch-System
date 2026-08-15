# AI CONTINUITY / RESTART NOTE

This repository is intended to be understandable by future human maintainers and future AI systems without silently reviving superseded architecture.

## Current baseline

As of 2026-08-15, the current public map architecture is:

```text
QGIS 3.44.9
  -> temporary raster MBTiles
  -> custom MBTiles to TPKX converter
  -> Esri Compact Cache V2 / .tpkx
  -> ArcGIS Earth
```

TPKX Map Factory v1.0.0 is LIVE-PROVEN / RELEASE ACCEPTED.

ArcGIS Earth is abbreviated **AE** throughout current project work.

## Hard requirement

> There can be no operational dependence on Internet connectivity. Period.

Internet access is acceptable for preparation, map manufacture, refresh, optional online routing, or other nonessential enhancements. Essential command and map-viewing behavior must continue offline.

## Acceptance authority

For finished TPKX products, **ArcGIS Earth is the final operational acceptance authority**. A package must open without complaint, land in the correct location, expose the expected zoom behavior, and render correctly.

## Do not regress

- Do not return Google Earth Pro to primary-viewer status by inertia.
- Do not present KML Super Overlay / Blooming Onion as the current basemap architecture.
- Do not make temporary MBTiles a normal public deliverable.
- Do not casually rewrite the proven MBTiles-to-TPKX converter.
- Do not add persistent work folders, logs, or sidecars to the user's chosen TPKX destination.
- Do not reintroduce the removed Neighbor Extent/Grid-ID complexity into the normal-user GUI.
- Keep advanced GIS freedom through the existing-MBTiles -> TPKX button.
- Retain KML for interoperability, NetworkLinks, external feeds, and saved content.

## Current known-good baseline

- Windows 10/11 64-bit
- Python 3.14.5
- QGIS 3.44.9
- ArcGIS Earth
- Factory raster recipe: PNG, 96 DPI, antialiasing ON, metatile 4, Z0-Z20

No additional Python libraries are required by the core TPKX converter path.

## Proven paths

1. Normal Factory: source -> area -> zoom -> QGIS -> temporary MBTiles -> TPKX -> AE.
2. Advanced Factory: existing raster MBTiles -> TPKX -> AE.
3. PRAVE -> ArcGIS Earth Automation API is LIVE-PROVEN with native drawings and RSSI fire-truck icons.

## Persistent Geographic Awareness

Current operational language includes **Persistent Geographic Awareness**: keeping position, surroundings, routes, and terrain continuously visible and available without relying on a network request at showtime.

## Historical archive rule

Legacy Google Earth, KML forest/Blooming Onion, Network Earth, and Google Earth Enterprise work is technically valuable lineage. Preserve it as history. Do not treat old material as current merely because it exists.

See:

- `README.md`
- `docs/TECHNICAL_ARCHITECTURE.md`
- `docs/LEGACY_GOOGLE_EARTH_README_2026-07-23.md`
- `releases/TPKX_MAP_FACTORY_v1_0_0_RELEASE_NOTES.md`

for the current restart point.