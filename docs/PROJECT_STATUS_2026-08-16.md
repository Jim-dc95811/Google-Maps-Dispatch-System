# Offline GeoStack — Project Status — 2026-08-16

This is the dated continuity checkpoint for the major engineering changes completed or observed on 2026-08-16.

## Executive state

Offline GeoStack now has **two live-proven local raster deployment families** around the same QGIS/MBTiles manufacturing core:

```text
A. local package
QGIS → MBTiles → TPKX → ArcGIS Earth

B. local service
QGIS → MBTiles → HTTPS WMTS → private USB tether → ArcGIS Earth Mobile
```

The project still has **no operational dependence on the public Internet**.

## Frozen accepted baseline

### TPKX Map Factory v1.0.0

**Status: RELEASE-ACCEPTED / FROZEN — 2026-08-15**

Do not replace the frozen accepted archive with a later TEST build.

Frozen converter:

`MBTiles_to_TPKX_v0_1_0.py`

The exact accepted ZIP remains a manual GitHub-release task under issue #1.

## TPKX Map Factory v1.2.0 TEST

**Status: BUILT / SELF-TESTED; Windows live acceptance underway**

Reason for branch:

Map Fountain made the QGIS-built MBTiles useful as an operational product rather than disposable manufacturing material.

Normal choices:

```text
TPKX
MBTiles
Both
```

`Both` is the current TEST default.

Current intended meaning:

- TPKX → ArcGIS Earth local-file deployment;
- MBTiles → Map Fountain local service deployment;
- Both → preserve both options from the same QGIS-built raster pyramid.

The experimental TPKX → MBTiles recovery tool was removed from v1.2 after a recovered production map showed blurred/missing regions on mobile.

## ArcGIS Earth Mobile local-file testing

**Status: LIVE-PROVEN on multiple packages**

Successful local Android TPKX examples:

- Rasta Thames Bridge;
- smaller Esri package;
- smaller Google Hybrid package.

One larger Google Hybrid package returned:

`spatial reference not supported`

Do not generalize that one failure into a blanket mobile TPKX limitation.

## USB Map Fountain

### Current live tool

`Rasta USB Map Fountain v0.2.1 TEST`

**Status: LIVE-PROVEN**

Live chain:

```text
MBTiles on Windows PC / SSD
→ HTTPS WMTS
→ Android USB tether / Remote NDIS
→ ArcGIS Earth Mobile
```

Proven:

- PC-to-phone USB local network;
- HTTP service proof;
- HTTPS service proof;
- QR service loading;
- outside Internet removed while map remained functional;
- selectable MBTiles GUI;
- unique map/service identity fixed stale cached-map reuse;
- three different substantial MBTiles displayed;
- large Lago panorama displayed smoothly on Android.

### Operator navigation envelope

Live observation:

> **Do not whip the mobile view around. Deliberate pan/zoom is smooth and reliable; rapid repeated movement can outrun the current path.**

Treat this as current operator guidance until a later live test replaces it.

### Current engineering limitation

The HTTPS proof used certificate material tied to the observed USB-tether PC IP during the test sequence. General IP/certificate lifecycle handling is not yet a finished consumer workflow.

## TPKX → MBTiles recovery experiment

**Status: REJECTED AS PRODUCTION PATH**

Controlled Thames Bridge fixture:

- 22 bundles read;
- 6,976 tiles recovered;
- Z0–Z18;
- recovered coordinate/tile-byte set matched the controlled TPKX tile set.

Production ESG1S recovery:

- 50 bundles;
- 271,211 tiles;
- Z0–Z18;
- recovered MBTiles Windows File Explorer size: **27,709,676 KB**;
- mobile visual result contained blurred/missing regions.

Decision: rebuild source MBTiles from QGIS and preserve MBTiles going forward.

## Native GNSS

**Status: LIVE-OBSERVED — 2026-08-15**

Actual field receiver drove ArcGIS Earth Windows native own-position.

Known-good observed input:

- 9600 baud;
- GLL present;
- RMC present.

## PRAVE

**Status: LIVE-PROVEN**

PRAVE → ArcGIS Earth Automation API displayed controlled units with native drawings / fire-truck RSSI icons.

Healthy observed state included:

```text
UNITS=6
API_OK=47
API_BAD=0
BAD_RMC=0
BAD_PRAVE=0
RMC=FRESH
```

## Rasta Pyramid Factory sibling project

Dedicated repository:

`Jim-dc95811/Rasta-Pyramid-Factory`

**v0.1.3 TEST: LIVE-PROVEN**

Major 2026-08-16 proofs include:

### Montreal

- 29,684 × 7,620 PNG;
- 13,381 tiles;
- 52 bundles;
- 0:05:04;
- ArcGIS Earth PASS.

### Frankfurt

- 8,003 × 5,622 JPEG;
- automatic Atlantic synthetic parking near 30°N/80°W;
- ArcGIS Earth PASS.

### Tower Bridge

- 15,287 × 7,643 JPEG;
- 6,976 tiles;
- 22 bundles;
- 0:02:18;
- TPKX **294,910 KB**;
- ArcGIS Earth PASS.

### Kings Reach Panorama 2

- 63,000 × 18,589 JPEG;
- ~1.17 billion pixels;
- 67,619 tiles;
- 30 bundles;
- 0:23:07;
- TPKX **1,949,149 KB**;
- ArcGIS Earth PASS;
- deep navigation resolved individual people inside London Eye pods.

### Tibidabo / Barcelona

- 62,141 × 14,606 JPEG;
- ~908 million pixels;
- 52,482 tiles;
- 30 bundles;
- 0:20:40;
- ArcGIS Earth PASS;
- useful fine detail distributed across the city.

### Rasta output-size rule

Source file megabytes are a weak predictor.

Prioritize:

1. width × height;
2. total source pixels;
3. scene detail/compressibility;
4. zoom range;
5. tile encoding.

A smaller compressed JPEG may contain far more pixels than a much larger TIFF.

## GitHub maintenance completed in this review

- Offline GeoStack README updated to current dual deployment architecture.
- current architecture SVG updated.
- mobile / Map Fountain technical record added.
- roadmap updated.
- changelog updated.
- technical architecture updated.
- AI continuity note updated.
- stale repo-rename issue #2 closed.
- v1.0 exact-binary issue #1 left open and clarified.
- Rasta README / roadmap / changelog / acceptance / AI restart records updated through gigapixel proofs.
- Rasta one-time GitHub Actions bootstrap history documented.

## GitHub Actions notification note

A delayed email may report:

`Materialize exact source: All jobs have failed`

That refers to the **first** temporary Rasta bootstrap workflow run. The corrected second run succeeded, committed the exact source files, and removed the temporary workflow. It is historical noise, not a current repository failure.

## Next gates

1. finish the direct-QGIS MBTiles rebuild now being used to replace the defective recovered ESG1S MBTiles;
2. validate that fresh MBTiles through Map Fountain in the exact mobile area that showed defects;
3. finish Windows live acceptance of TPKX Map Factory v1.2 output modes;
4. generalize Map Fountain HTTPS certificate/IP handling;
5. perform cold restart / reconnect tests;
6. return to field GNSS + PRAVE moving-vehicle demonstration when desired;
7. manually attach the exact frozen v1.0.0 ZIP to GitHub.

## Governing evidence rule

> **A clever internal result is not acceptance. The real target decides.**
