# ArcGIS Earth Mobile + USB Map Fountain

> **HISTORICAL PROOF RECORD — 2026-08-16.** This document preserves the Windows-hosted USB-tether WMTS path that was live-proven before the router-only Map Fountain breakthroughs and before the current personal-phone / microSD deployment direction. Do not treat the word “current” inside the preserved chronology below as current 2026-08-18 architecture.

## Standalone project home

Map Fountain has its own repository:

**https://github.com/Jim-dc95811/Map-Fountain**

Current personal-phone deployment work now lives in:

**https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-**

This Offline GeoStack document remains an integration/evidence record for the historical USB Map Fountain proof.

## Status at the recorded milestone

**LIVE-PROVEN — 2026-08-16**

Offline GeoStack proved two ArcGIS Earth Mobile data paths at that stage:

1. **Local TPKX file** — compatible `.tpkx` opened through ArcGIS Earth Mobile.
2. **Live local WMTS** — raster MBTiles served from a Windows PC/SSD over the Android USB-tether network and added to ArcGIS Earth Mobile over HTTPS.

The second path was the USB Map Fountain proof.

## Live-proven chain

```text
raster MBTiles on Windows PC / attached SSD
        ↓
Rasta USB Map Fountain v0.2.1 TEST
        ↓
local HTTPS WMTS
        ↓
Android USB tether / Remote NDIS network
        ↓
ArcGIS Earth Mobile
        ↓
on-demand raster tiles
```

No outside Internet connection was required for map delivery or display.

## What was actually observed

- Android USB tether created a local IP network between the Windows PC and phone.
- Windows-side tether adapter was observed as `Remote NDIS based Internet Sharing Device #2`.
- ArcGIS Earth Mobile consumed a local WMTS service through `Add Data → URL`.
- HTTPS service and QR-based service entry were made functional.
- The phone continued displaying the served map with outside Internet removed.
- Three different substantial raster MBTiles were successfully displayed through the Map Fountain path.
- A large Lago panorama MBTiles was served from the PC and navigated smoothly on ArcGIS Earth Mobile.
- HTTP server logs showed real Android tile requests with `200` responses across multiple zoom levels.

## Operator behavior observed on mobile

**Deliberate pan/zoom:** smooth and reliable in live testing.

**Rapid repeated zooming or whipping the view around:** could outrun the tested delivery/render path.

This was an observed characteristic of that specific active-server/USB-tether path.

## QR / service identity lesson

The first multi-map GUI reused one WMTS layer identity and tile URL space, which allowed ArcGIS Earth Mobile to reuse stale cached test tiles. v0.2.1 corrected this by assigning each selected MBTiles a unique map/service identity and unique tile URL namespace.

Recorded working sequence:

```text
USB tether ON
→ START MAP FOUNTAIN
→ CHOOSE MBTILES
→ START HTTPS MAP FOUNTAIN
→ OPEN QR
→ ArcGIS Earth Mobile: Add Data → QR Code
→ scan
→ map loads
```

## Local TPKX acceptance

ArcGIS Earth Mobile also successfully opened multiple local TPKX files directly from Android storage, including a Rasta-produced Thames Bridge package and smaller Esri / Google Hybrid packages.

One larger Google Hybrid TPKX was rejected by the mobile app with `spatial reference not supported`. Because other TPKX files opened successfully, that failure was not generalized into a blanket mobile TPKX limitation.

## TPKX → MBTiles recovery experiment

A reverse Compact Cache V2 recovery tool could recover exact raster tile bytes from a controlled TPKX fixture. A recovered production MBTiles later displayed blurred/missing regions on ArcGIS Earth Mobile.

Decision:

- **Do not use TPKX recovery as the production path.**
- New map production should preserve direct QGIS MBTiles when MBTiles is needed.

## What happened afterward

Chronology after this proof:

1. Map Fountain moved from the Windows-hosted server to a router-only Flint 2 + SSD design.
2. Windows ArcGIS Earth opened a production-scale native TPKX directly over SMB/Wi-Fi.
3. ArcGIS Earth Mobile consumed a pre-generated Static REST WMTS directly from Flint 2 HTTPS/WebDAV.
4. Both router paths were LIVE-PROVEN.
5. The broader project then simplified the normal personal-phone direction again: local TPKX on microSD, with Field Maps/ArcGIS Earth as downstream apps.

So this document is important engineering lineage, but **USB Map Fountain is not current deployment architecture.**
