# Offline GeoStack — Technical FAQ

## What is Offline GeoStack?

A Windows-first offline geospatial stack that uses QGIS for cartographic rendering, a custom MBTiles → TPKX interoperability bridge for packaging, ArcGIS Earth as the primary runtime, and GNSS / PRAVE / F22 / QR / KML as live or interoperable field inputs.

## Is TPKX Map Factory the whole project?

No. **TPKX Map Factory** is the map-manufacturing subsystem. **Offline GeoStack** is the master project.

## Why QGIS?

Because QGIS already does the hard cartographic work: source access, projection, layer composition, labels, symbols, blending, rasterization, zoom-dependent rendering, and MBTiles generation. Rebuilding that inside the Factory would be pointless and fragile.

## Why MBTiles if ArcGIS Earth does not open MBTiles directly?

MBTiles is the temporary manufacturing handoff. QGIS produces it cleanly; the custom converter consumes it cleanly. The normal user never needs to keep it.

## Does the converter redraw or resample the imagery?

No. In the proven raster PNG/JPEG path, the converter reads the existing `tile_data` bytes from MBTiles and writes those bytes into Compact Cache V2 bundle records. It changes addressing, indexes, metadata, and container structure—not the cartography.

## What is the critical row conversion?

MBTiles/TMS rows are bottom-origin while ArcGIS compact-cache rows are top-origin:

```text
y_arcgis = (2^z - 1) - y_tms
```

The addressing/bundle work is integer math.

## Is the converter doing coordinate “fudging”?

Not in the tile-placement path. The critical tile and bundle addressing uses integer operations. Web Mercator metadata uses ordinary double-precision floating-point math and Python `math.pi`. Human-readable console formatting does not feed rounded values back into package placement.

## Why Compact Cache V2?

That is the tile storage used by TPKX. Bundles cover 128 × 128 possible tile slots, with indexed binary records that ArcGIS applications can address efficiently.

## Does QGIS natively export TPKX?

Not in the workflow used here. QGIS produces the raster MBTiles; Offline GeoStack supplies the missing bridge into the Esri TPKX / Compact Cache V2 package structure.

## Why ArcGIS Earth?

Because it provides a modern 3D desktop runtime with native local TPKX support, KML/KMZ/NetworkLinks, GNSS/NMEA capability, a local Automation API, native drawings/markers, and useful session behavior. Most importantly for this project, a prepared TPKX can function without operational Internet dependency.

## Is ArcGIS Earth required to manufacture the TPKX?

No. QGIS + Python + the Factory/converter manufacture the package. ArcGIS Earth is the current target runtime and final acceptance authority.

## What does “ArcGIS Earth is the acceptance authority” mean?

A structurally plausible package is not enough. The project accepts a TPKX operationally when AE opens it, places it correctly, shows the expected zoom behavior, renders the expected cartography, and navigates normally.

## How large has this been tested?

Among the live acceptance runs:

- 271,497-tile advanced existing-MBTiles conversion → 47 bundles → AE PASS.
- 271,242-tile Esri World / Google Labels normal Factory build → AE PASS.
- Exact v1.0.0 smoke build → AE PASS.

See the professional report and release notes for the exact Windows-visible sizes and elapsed times.

## Can I use my own QGIS project?

Yes. That is the point of **ADVANCED: MBTILES → TPKX**. Build the raster cartography you want in QGIS, produce compatible raster MBTiles, then use the Factory only as the package bridge.

## Can the advanced path include parcels, roads, contours, flood zones, etc.?

If QGIS can render them into the raster MBTiles, the converter does not care what upstream layers produced the pixels. It receives finished raster tiles.

## Does Offline GeoStack require Internet access in the field?

Core map operation is designed specifically not to.

> **There can be no operational dependence on Internet connectivity. Period.**

Connectivity is useful during preparation and for optional online features. It is not allowed to become the single point of failure for essential map use.

## What is Persistent Geographic Context?

The operating condition where local map content, own position, surrounding roads/terrain, and other spatial context remain continuously present instead of being repeatedly requested from a network service.

## What is PRAVE doing in a map project?

PRAVE is one of the live remote-position inputs in the larger field system. The PRAVE → ArcGIS Earth Automation API path is live-proven with native drawings, unit labels, and RSSI fire-truck icons.

## What about F22 and QR?

They are continuing input paths. The forward design is to decode protocol-specific input at the edge, normalize it, and feed one ArcGIS Earth live-position/command layer rather than create separate renderers.

## Is KML obsolete here?

No. KML remains useful for interoperability, saved content, external feeds, placemarks, folders, and NetworkLinks. It is simply no longer required to impersonate the offline raster basemap or every live-position mechanism.

## What does the MIT license cover?

Original Offline GeoStack code and documentation, unless a file states otherwise. It does **not** grant rights to third-party imagery, labels, basemaps, vendor software, or external services. See `NOTICE.md` and `SOURCE_AND_LICENSING_NOTE.md`.

## Why is the repository still named Google-Maps-Dispatch-System?

Historical inertia. The master project has been renamed **Offline GeoStack**. The connected tool used for this rebuild cannot rename the repository slug/About metadata, so the final UI rename is tracked as an issue.

## Where is the exact v1.0 ZIP?

The exact release-accepted archive is preserved in the canonical project archive. A connector-truncated GitHub copy was removed deliberately. Direct GitHub attachment of the exact ZIP is the one remaining binary-publication step.

## What should a future AI read first?

1. `README.md`
2. `docs/AI_CONTINUITY_RESTART_NOTE.md`
3. `docs/professional_report/README.md`
4. `docs/TECHNICAL_ARCHITECTURE.md`
5. `CHANGELOG.md`
6. `ROADMAP.md`

Then inspect legacy material only when chronology matters.
