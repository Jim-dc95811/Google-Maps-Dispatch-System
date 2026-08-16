# ArcGIS Earth Mobile + USB Map Fountain

## Standalone project home

Map Fountain now has its own repository:

**https://github.com/Jim-dc95811/Map-Fountain**

This Offline GeoStack document remains the integration/evidence record for how Map Fountain fits the master operational system.

## Status

**LIVE-PROVEN — 2026-08-16**

Offline GeoStack now has two independently proven ArcGIS Earth Mobile data paths:

1. **Local TPKX file** — copy a compatible `.tpkx` to Android storage and open it through ArcGIS Earth Mobile `Add Data → File`.
2. **Live local WMTS** — serve raster MBTiles from a Windows PC/SSD over the Android USB-tether network and add the service to ArcGIS Earth Mobile over HTTPS.

The second path is the current **USB Map Fountain** proof.

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

No outside Internet connection is required for map delivery or display.

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

The mobile viewer has a practical navigation envelope.

**Deliberate pan/zoom:** smooth and reliable in live testing.

**Rapid repeated zooming or whipping the view around:** can outrun the delivery/render path and make the viewer unhappy.

Current operator guidance is therefore simple:

> **Move deliberately. Let the map settle. Then continue.**

This is a live-observed operating characteristic, not a claim about a hard technical limit.

## QR / service identity lesson

The first multi-map GUI reused one WMTS layer identity and tile URL space, which allowed ArcGIS Earth Mobile to reuse stale cached test tiles. v0.2.1 corrected this by assigning each selected MBTiles a unique map/service identity and unique tile URL namespace.

The working operator sequence became:

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

The GUI can point at MBTiles on the PC or attached SSD; the map is not hard-coded into the server.

## Local TPKX acceptance

ArcGIS Earth Mobile also successfully opened multiple local TPKX files directly from Android storage, including a Rasta-produced Thames Bridge package and smaller Esri / Google Hybrid packages.

One larger Google Hybrid TPKX was rejected by the mobile app with `spatial reference not supported`. Because other TPKX files from the same broader project opened successfully, do not generalize that failure into a blanket mobile TPKX limitation. Treat package-level compatibility as something that still deserves controlled acceptance testing.

## TPKX → MBTiles recovery experiment

A reverse Compact Cache V2 recovery tool was prototyped and could recover exact raster tile bytes from a controlled TPKX fixture. However, a recovered production MBTiles displayed visual defects on ArcGIS Earth Mobile: blurred/missing regions appeared even though other areas looked correct.

Decision:

- **Do not use TPKX recovery as the production path.**
- The recovery tool was removed from TPKX Map Factory v1.2.
- New map production should preserve MBTiles directly when Map Fountain use is expected.

## TPKX Map Factory v1.2 direction

**Status: BUILT / SELF-TESTED; Windows live acceptance underway as of 2026-08-16.**

v1.2 changes the normal build choice to:

```text
TPKX
MBTiles
Both
```

`Both` is the default in the current TEST build so the same QGIS-manufactured raster pyramid can support both deployment paths:

```text
TPKX    → local ArcGIS Earth / ArcGIS Earth Mobile file use
MBTiles → USB Map Fountain → ArcGIS Earth Mobile live local service
```

The accepted v1.0.0 baseline remains preserved separately.

## Current engineering boundary

The Map Fountain proof is **single-device / private local serving**, not a claim of a production multi-user map server.

The current HTTPS prototype also used a certificate tied to the observed USB-tether PC address during live testing. General certificate/IP lifecycle handling remains future productization work.

## Next useful gates

- complete live acceptance of TPKX Map Factory v1.2 output modes;
- repeat Map Fountain with the newly produced direct MBTiles for a map whose recovered MBTiles showed defects;
- decide whether the next appliance transport should remain USB, move to local Wi-Fi, or support both;
- generalize HTTPS certificate handling without making setup burdensome;
- measure practical throughput/latency on larger production map libraries;
- test cold restart and reconnection behavior deliberately.
