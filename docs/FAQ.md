# Offline GeoStack — Technical FAQ

## What is Offline GeoStack?

A Windows-first offline geospatial stack that uses QGIS for cartographic rendering, raster MBTiles as the tile-pyramid handoff/master when useful, a custom MBTiles → TPKX interoperability bridge for native packaging, and local field deployment that does not depend on the public Internet at showtime.

ArcGIS Earth remains a primary runtime. Android deployment work now also includes ArcGIS Field Maps.

## Is TPKX Map Factory the whole project?

No. **TPKX Map Factory** is the map-manufacturing subsystem. **Offline GeoStack** is the master project.

## Why QGIS?

Because QGIS already does the hard cartographic work: source access, projection, layer composition, labels, symbols, blending, rasterization, zoom-dependent rendering, and MBTiles generation. Rebuilding that inside the Factory would be pointless and fragile.

## Why MBTiles if ArcGIS Earth does not open MBTiles directly?

MBTiles contains the already-rendered raster pyramid. In the frozen v1.0 Factory it is primarily the manufacturing handoff to the converter. In later TEST branches it may also be deliberately preserved as a finished/interchange product.

The important rule is that direct QGIS-built MBTiles is the accepted MBTiles source. Reverse TPKX → MBTiles recovery was rejected as a production shortcut after real mobile visual defects.

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

## Does QGIS natively export the TPKX used here?

Not in this workflow. QGIS produces raster MBTiles; Offline GeoStack supplies the missing bridge into the Esri TPKX / Compact Cache V2 package structure.

## Why ArcGIS Earth?

Because it provides native local TPKX support, KML/KMZ/NetworkLinks, GNSS/NMEA capability, a local Automation API, drawings/markers, useful 3D navigation, and a local map path that can operate without public Internet.

## Is ArcGIS Earth required to manufacture the TPKX?

No. QGIS + Python + the Factory/converter manufacture the package. ArcGIS Earth is one of the primary target runtimes and has been the final acceptance authority for the proven TPKX work to date.

## What does “the real target is the acceptance authority” mean?

A structurally plausible package is not enough. The intended app must open it, place it correctly, show the expected zoom behavior, render the expected cartography, and navigate normally.

Vendor documentation establishes that a path should exist. It does not substitute for this project's own target test.

## How large has this been tested?

Among the live acceptance runs:

- 271,497-tile advanced existing-MBTiles conversion → 47 bundles → ArcGIS Earth PASS;
- 271,242-tile Esri World / Google Labels normal Factory build → ArcGIS Earth PASS;
- exact v1.0.0 smoke build → ArcGIS Earth PASS;
- production-scale `ESG1N.tpkx` at **25,561,426 KB** in Windows File Explorer → opened directly from router-attached storage over Wi-Fi → ArcGIS Earth PASS.

## Can I use my own QGIS project?

Yes. That is the point of **ADVANCED: MBTILES → TPKX**. Build the raster cartography you want in QGIS, produce compatible raster MBTiles, then use the Factory only as the package bridge.

## Can the advanced path include parcels, roads, contours, flood zones, etc.?

If QGIS can render them into the raster MBTiles, the converter does not care what upstream layers produced the pixels. It receives finished raster tiles.

## Does Offline GeoStack require Internet access in the field?

Core prepared-map operation is designed specifically not to.

> **There can be no operational dependence on Internet connectivity. Period.**

Connectivity is useful during preparation, imagery refresh, and optional online features. It is not allowed to become the single point of failure for essential map use.

## What is the current personal-phone direction?

```text
Factory-built TPKX
→ microSD card
→ Android
→ ArcGIS Field Maps / ArcGIS Earth
```

The current card-sizing experiment is testing district Z17, county Z18, and selected State Forest/high-value Z20 coverage with real finished byte counts.

## Does ArcGIS Field Maps support TPKX on Android/microSD?

Esri documents sideloaded `.tpk` / `.tpkx` basemaps on Android device storage or SD card.

Documented Android basemap folder:

```text
\Android\data\com.esri.fieldmaps\files\basemaps
```

Offline GeoStack's own Field Maps + microSD acceptance test is still pending. Do not label it project LIVE-PROVEN until the real target passes.

## Why set Field Maps to Wi-Fi only?

The target audience may be using personal phones and personal data plans. Esri states that the Cellular Data option inside Field Maps does not block every cellular-data use by the app. Android's app-level network setting can restrict Field Maps to Wi-Fi only while leaving ordinary phone cellular service available.

The deployment repository contains the lean field procedure.

## What happened to Map Fountain?

Map Fountain worked.

It live-proved:

1. native TPKX on router-attached SSD → SMB/Wi-Fi → ArcGIS Earth Windows;
2. Static REST WMTS on router-attached SSD → local HTTPS/Wi-Fi → ArcGIS Earth Mobile.

After proving those paths, the project simplified the normal personal-phone direction further by putting TPKX directly on removable local storage.

Map Fountain is therefore **proven / parked**, not a failed branch. It may return as a Starlink-connected basecamp storage / poor-man's NAS package.

## What is the `.restmap` branch?

A later TPKX Map Factory v1.4.0 TEST experiment created a compact portable REST seed instead of transporting a giant expanded WMTS file tree:

```text
verified MBTiles
→ <map>_REST.restmap
→ move one file
→ expand Static REST WMTS at final SSD
```

The small lifecycle fixture self-tested successfully. It remains experimental and does not replace the frozen v1.0.0 TPKX baseline.

## What is Persistent Geographic Context?

The operating condition where local map content, own position, surrounding roads/terrain, and other spatial context remain continuously present instead of being repeatedly requested from a public network service.

## What is PRAVE doing in a map project?

PRAVE is one of the live remote-position inputs in the larger field system. The PRAVE → ArcGIS Earth Automation API path is live-proven with native drawings, unit labels, and RSSI fire-truck icons.

## What about F22 and QR?

They are continuing input paths. The design is to decode protocol-specific input at the edge, normalize it, and feed one ArcGIS Earth live-position/command layer rather than create separate renderers.

## Is KML obsolete here?

No. KML remains useful for interoperability, saved content, external feeds, placemarks, folders, and NetworkLinks. It is simply no longer required to impersonate the offline raster basemap or every live-position mechanism.

## What are the four repositories now?

1. **Offline GeoStack** — master map-manufacturing / field-mapping system.
2. **Rasta Pyramid Factory** — arbitrary giant-raster / deep-zoom pyramid manufacturing.
3. **Map Fountain** — proven router/storage delivery evidence; parked reference / possible future basecamp NAS.
4. **Android Field Maps + ArcGIS Earth** — personal-phone / microSD deployment and user procedure.

## What does the MIT license cover?

Original Offline GeoStack code and documentation, unless a file states otherwise. It does **not** grant rights to third-party imagery, labels, basemaps, vendor software, or external services. See `NOTICE.md` and `SOURCE_AND_LICENSING_NOTE.md`.

## Where is the exact v1.0 ZIP?

The exact release-accepted archive is preserved in the canonical project archive. Do not substitute a TEST branch or reconstructed package and call it the accepted release.

## What should a future AI read first?

1. `README.md`
2. `ROADMAP.md`
3. `docs/AI_CONTINUITY_RESTART_NOTE.md`
4. `docs/TECHNICAL_ARCHITECTURE.md`
5. the Android deployment repository README
6. `CHANGELOG.md`
7. the v1.0 professional report when historical release detail is needed

Then inspect legacy material only when chronology matters.
