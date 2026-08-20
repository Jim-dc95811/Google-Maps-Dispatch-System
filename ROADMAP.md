# Offline GeoStack Roadmap

## Current Factory product line

**Offline Map Factory 1.0** remains the current clean product direction.

Status: **BUILT / SELF-TESTED — LIVE ACCEPTANCE PENDING**.

Current operator feature set:

- 4 sources: Google Earth, Google Hybrid, Esri World, Esri World / Google Labels;
- map area by HOME EXTENT, Clipboard History diagonal points, or two manual GPS points;
- Z0-Z20;
- output choice: TPKX / MBTiles / Both;
- one Advanced Tool: existing MBTiles -> TPKX;
- no REST / Static WMTS output in the current Factory.

The prior **TPKX Map Factory v1.0.0** remains a RELEASE-ACCEPTED / FROZEN historical milestone. Do not erase or relabel that acceptance record.

---

## Immediate Factory gate

Run Offline Map Factory 1.0 on the real Windows/QGIS target.

Acceptance sequence:

1. launch from `RUN OFFLINE MAP FACTORY.bat`;
2. verify both required QGZ references are found;
3. build a small **MBTiles-only** map;
4. build a small **TPKX-only** map;
5. build a small **Both** map;
6. run **Advanced MBTiles -> TPKX**;
7. open the produced TPKX in ArcGIS Earth;
8. confirm expected location, cartography, zoom behavior, navigation, cleanup, and final output state.

Only after that passes should Offline Map Factory 1.0 be promoted to LIVE-PROVEN / RELEASE-ACCEPTED.

---

## Current primary field direction — physical district map card

Mission:

> **A Field Maps user must be able to open the app with zero public Internet and use a district-wide Esri Hybrid map through Z17. The same local map should stop the heavy basemap from burning cellular data when service exists.**

Current field chain:

```text
Offline Map Factory TPKX
-> ArcGIS Pro minimal MMPK wrapper
-> physical microSD
   +-- Field Maps mappackages\DISTRICT.mmpk
   +-- Field Maps basemaps\DISTRICT.tpkx
-> Android
-> Field Maps + ArcGIS Earth Mobile
```

### Why both files

The duplication is deliberate.

- MMPK supplies a complete on-device Field Maps map.
- TPKX remains available as a sideloaded local basemap and direct ArcGIS Earth Mobile product.
- Storage efficiency ranks below field reliability.
- MBTiles remains on the manufacturing/master side unless a different downstream use explicitly needs it.

### ArcGIS Pro bridge — PASS

ArcGIS Pro 3.7 has now successfully created:

- a small minimal MMPK from an existing project TPKX;
- a district-scale approximately 52 GB MMPK from the existing approximately 52 GB district TPKX.

Small specimen observations:

- analyzer: 0 errors / 0 warnings / 0 messages;
- MMPK version 3.0;
- original TPKX preserved intact inside the MMPK;
- no HTTP/HTTPS references found in the small specimen `.mmap` / `.mapx`;
- Pro-created MMPK rendered in Windows ArcGIS Earth while Earth showed **Not signed in**.

This proves the manufacturing bridge only. Field Maps runtime acceptance remains pending.

### Current gold-test card

- 128 GB physical microSD;
- exFAT;
- Windows shows approximately 119 GB usable;
- approximately 52 GB district TPKX;
- approximately 52 GB district MMPK;
- first runtime target: Amazon Fire tablet;
- later GPS target: GPS-capable personal Android phone.

### Field Maps acceptance gate

1. populate the physical card on Windows while it is outside Android;
2. insert the prepared card into the Fire;
3. open Field Maps;
4. go to **On Device**;
5. confirm the district MMPK appears;
6. open and pan/zoom through Z17;
7. remove public Internet and repeat;
8. close/reopen Field Maps while still disconnected;
9. repeat later on a GPS-capable phone and verify own position;
10. test Field Maps restricted to Wi-Fi only while normal cellular service stays available.

Do not promote before the real device passes.

### Scoped-storage lesson

The Fire investigation proved ordinary ADB/MTP-style injection into another app's protected `Android/data` tree is not a viable normal-user path.

Do not reopen that dead end. Use Esri's documented physical-card sideload method.

---

## User-experience rule

The strongest selling point is freedom from **map rationing**.

The desired experience is:

```text
Field Maps          -> agency workflow
ArcGIS Earth Mobile -> fast local direct TPKX viewer
physical card       -> heavy geography already present
```

Keep cellular data for communication instead of streaming a giant basemap repeatedly.

---

## REST / Static WMTS exploration — PARKED HISTORY

The Map Fountain Android proof remains valid and preserved.

Current decision:

- preserve the history;
- do not include REST in Offline Map Factory 1.0;
- do not revive REST in the normal personal-phone path unless a real shared-storage need reopens it.

Possible future Map Fountain roles remain:

- Starlink/basecamp NAS;
- true multi-client shared-map need;
- removable storage proving insufficient.

---

## Rasta Pyramid Factory

Rasta remains the sibling project for arbitrary giant rasters and deep-zoom imagery.

Current live-proven baseline: v0.1.3.

The v0.1.4 REST branch remains TEST history tied to Map Fountain exploration; Rasta's core value does not depend on REST.

---

## Field integration

- Native GNSS: **LIVE-OBSERVED**, 9600 baud, GLL + RMC present.
- PRAVE -> ArcGIS Earth Automation API: **LIVE-PROVEN**.
- ArcGIS Earth Mobile local TPKX: **LIVE-PROVEN on multiple project packages**.
- Field Maps MMPK on physical microSD: **VENDOR-DOCUMENTED / PROJECT LIVE TEST PENDING**.

---

## Non-goals

- forcing ordinary field users to run the Factory;
- restoring REST to the clean Factory without a demonstrated need;
- requiring router/server infrastructure for normal personal-phone deployment;
- rebuilding QGIS;
- making public Internet mandatory;
- reviving Raspberry Pi / Pi-server architecture by default;
- using rejected TPKX recovery as a shortcut;
- returning to protected-folder ADB/MTP injection as the normal Android path;
- optimizing storage elegance ahead of field reliability;
- adding features because they exist rather than because users need them.

## Governing rules

> **The real target decides acceptance.**

> **Keep the Factory simple. Put the heavy map on the card.**
