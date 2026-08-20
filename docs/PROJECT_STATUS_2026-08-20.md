# Offline GeoStack — Project Status — 2026-08-20

## Executive state

The project has reached a new Android deployment checkpoint without changing the core manufacturing architecture.

The current map-manufacturing product remains:

**OFFLINE MAP FACTORY 1.0**

Status remains **BUILT / SELF-TESTED — LIVE ACCEPTANCE PENDING** under its own release line.

The historical **TPKX Map Factory v1.0.0** remains **RELEASE-ACCEPTED / FROZEN**.

The important change on 2026-08-20 is downstream deployment:

```text
Offline Map Factory
-> district TPKX
-> ArcGIS Pro minimal MMPK wrapper
-> physical microSD
   +-- Field Maps mappackages\DISTRICT.mmpk
   +-- Field Maps basemaps\DISTRICT.tpkx
-> Android
-> Field Maps + ArcGIS Earth Mobile
```

## Mission lock

The mission is now explicit:

> **A Field Maps user must be able to open the app with zero public Internet and use a district-wide Esri Hybrid map through Z17. The same local map should eliminate the need to burn cellular data on the heavy basemap when service exists.**

The user-facing value is freedom from **map rationing**.

## ArcGIS Pro MMPK manufacturing result

ArcGIS Pro 3.7 trial was installed and used to test the supported mobile-map-package workflow.

Minimal procedure:

```text
New Basemap
-> Add existing TPKX
-> Share
-> Mobile Map
-> Save package to file
-> Analyze
-> Package
```

Small specimen result:

- analyzer: **0 errors / 0 warnings / 0 messages**;
- Pro-created MMPK version: **3.0**;
- only seven outer files;
- original project TPKX preserved intact under `commondata/new_tpkx/`;
- `.mmap` directly references the packaged local TPKX;
- no HTTP/HTTPS references found in the small specimen `.mmap` / `.mapx`;
- package rendered successfully in Windows ArcGIS Earth while Earth showed **Not signed in**.

ArcGIS Pro then successfully created the district-wide approximately **52 GB MMPK** from the existing approximately **52 GB TPKX**.

Interpretation: the modern Pro MMPK is a thin package/container around the already-manufactured TPKX for this use case; Pro does not need to rebuild the raster pyramid.

## Current gold-card layout

Physical card selected:

- 128 GB microSD;
- Windows shows approximately 119 GB usable;
- exFAT;
- intended field payload approximately 104 GB plus filesystem overhead.

Card layout:

```text
\Android\data\com.esri.fieldmaps\files\mappackages\DISTRICT.mmpk
\Android\data\com.esri.fieldmaps\files\basemaps\DISTRICT.tpkx
```

The duplication is deliberate. Reliability outranks storage efficiency.

The direct QGIS-built MBTiles remains a manufacturing/master artifact and is not required on this field card.

## Why physical microSD is now the primary Field Maps transport

The Fire-tablet investigation proved Android scoped-storage barriers against ordinary ADB/MTP writes into another app's protected `Android/data` tree.

Observed result:

- ordinary writable card areas accepted ADB writes;
- `Android/data/com.esri.fieldmaps/...` rejected ADB/move/push attempts;
- MTP/File Explorer did not solve the protected-directory barrier.

This path is rejected as a normal user workflow.

Esri documents a physical-card sideload method: place the files on the card while the card is outside Android, then insert the prepared card into the device. That is the current gold-test route.

## Field Maps status

### MMPK on physical microSD

Status: **VENDOR-DOCUMENTED / PROJECT LIVE TEST PENDING**.

Next real-target gate:

1. finish copying the district MMPK and TPKX to the physical card;
2. insert the prepared card into the Amazon Fire tablet;
3. open Field Maps;
4. go to **On Device**;
5. confirm the district MMPK appears;
6. open and pan/zoom through Z17;
7. remove public Internet and repeat;
8. close/reopen Field Maps while still disconnected;
9. later repeat on a GPS-capable Android phone for own-position behavior;
10. test Field Maps restricted to Wi-Fi only while normal phone cellular service remains available.

Do not promote until the real target passes.

### Standalone TPKX basemap on physical microSD

Status: **VENDOR-DOCUMENTED / PROJECT LIVE TEST PENDING**.

The standalone TPKX remains on the card intentionally as redundancy and as a local-basemap path.

## ArcGIS Earth Mobile role

ArcGIS Earth Mobile local TPKX remains **LIVE-PROVEN on multiple project packages**.

The emerging user-facing two-app model is:

```text
Field Maps          -> agency workflow / packaged on-device map
ArcGIS Earth Mobile -> fast direct local TPKX viewer
```

Earth Mobile should be positioned as a primary local map viewer, not merely as a backup.

## Connectivity / authorization boundary

Esri's sideload documentation does not describe a separate Internet activation or pre-exposure step that makes a local MMPK/TPKX file valid.

Keep two questions separate:

- **file validity / local package presence**;
- **Field Maps user authorization / sign-in behavior**.

The standard Pro-created MMPK has not yet passed the desired cold-disconnected Field Maps acceptance. Do not alter licensing metadata or attempt to bypass a control; let the legitimate package and real Field Maps app decide the boundary.

## Current status matrix

| Capability | Status |
| --- | --- |
| Offline Map Factory 1.0 | 🟡 **BUILT / SELF-TESTED — LIVE ACCEPTANCE PENDING** |
| Historical TPKX Map Factory v1.0.0 | ✅ **RELEASE-ACCEPTED / FROZEN** |
| QGIS -> raster MBTiles | ✅ **LIVE-PROVEN** |
| MBTiles -> TPKX / Compact Cache V2 | ✅ **LIVE-PROVEN** |
| ArcGIS Pro existing TPKX -> minimal MMPK | ✅ **PASS — small and district-scale packages created** |
| Pro-created MMPK in Windows ArcGIS Earth | ✅ **PASS — rendered while Earth showed Not signed in** |
| ArcGIS Earth Mobile local TPKX | ✅ **LIVE-PROVEN on multiple packages** |
| Field Maps MMPK on physical microSD | 🟡 **VENDOR-DOCUMENTED / PROJECT LIVE TEST PENDING** |
| Field Maps standalone TPKX on physical microSD | 🟡 **VENDOR-DOCUMENTED / PROJECT LIVE TEST PENDING** |
| Fire scoped-storage ADB/MTP injection | ❌ **REJECTED / proven permission barrier** |
| Map Fountain | ✅ **LIVE-PROVEN / PARKED REFERENCE** |
| Rasta v0.1.3 | ✅ **LIVE-PROVEN baseline** |
| TPKX -> MBTiles recovery | ❌ **REJECTED as production path** |

## Do not regress

- Do not return to protected-folder ADB/MTP injection as the normal Fire/Android solution.
- Do not treat a bare TPKX as a complete standalone Field Maps map card without a map/container relationship.
- Do not abandon the standalone TPKX; it remains useful redundancy and direct ArcGIS Earth Mobile content.
- Do not optimize storage elegance ahead of field reliability.
- Do not revive Map Fountain infrastructure unless a real shared-storage need reopens it.
- Do not promote Field Maps behavior from vendor documentation alone.
- Do not make public Internet an operational requirement.

## Governing rule

> **Manufacture the geography once. Put the heavy map on the card. Let the real field application decide acceptance.**
