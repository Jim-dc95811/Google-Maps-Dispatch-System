# OFFLINE GEOSTACK — AI CONTINUITY / RESTART NOTE

## Current truth — 2026-08-20

The current clean Factory product line remains:

**OFFLINE MAP FACTORY 1.0**

Status: **BUILT / SELF-TESTED — LIVE ACCEPTANCE PENDING**.

The prior **TPKX Map Factory v1.0.0** remains a **RELEASE-ACCEPTED / FROZEN** historical milestone. Do not erase or relabel that record.

The major new work since the 2026-08-18 note is downstream Android deployment, not a Factory redesign.

Read first:

- `README.md`
- `ROADMAP.md`
- `docs/PROJECT_STATUS_2026-08-20.md`
- deployment repo `docs/FIELD_MAPS_MMPK_CARD_REFERENCE_2026-08-20.md`

---

## Offline Map Factory 1.0 contract

Normal operator capability:

- 4 sources: Google Earth, Google Hybrid, Esri World, Esri World / Google Labels;
- area by HOME EXTENT, Clipboard History diagonal points, or two manual GPS points;
- Z0-Z20;
- output: TPKX / MBTiles / Both;
- one Advanced Tool: existing MBTiles -> TPKX.

The current Factory deliberately does **not** include REST / Static WMTS output.

Do not reintroduce REST merely because historical TEST branches contain it.

---

## Finished-package standard

User-facing top level:

```text
OFFLINE MAP FACTORY 1.0 - Installation Guide.pdf
OFFLINE MAP FACTORY 1.0 - User Guide.pdf
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
RUN OFFLINE MAP FACTORY.bat
System Files\
```

All support code, tests, internal notes, icons, and implementation machinery belong behind `System Files`.

Required QGIS project placement:

```text
C:\Google Earth Project\QGIS\
```

with exact filenames:

```text
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
```

---

## Mission lock

The current Android mission is:

> **A Field Maps user must be able to open the app with zero public Internet and use a district-wide Esri Hybrid map through Z17. The same local map should stop the heavy basemap from burning cellular data when service exists.**

The key user-behavior problem is **map rationing**. The field user should be free to pan, zoom, and explore because the heavy geography is already local.

---

## Current district-card architecture

```text
Offline Map Factory
-> district TPKX
-> ArcGIS Pro minimal MMPK wrapper
-> physical microSD
   +-- Android\data\com.esri.fieldmaps\files\mappackages\DISTRICT.mmpk
   +-- Android\data\com.esri.fieldmaps\files\basemaps\DISTRICT.tpkx
-> Android
-> Field Maps + ArcGIS Earth Mobile
```

The duplicate TPKX is intentional. Reliability outranks storage efficiency.

Current gold-test card:

- 128 GB physical microSD;
- exFAT;
- Windows shows approximately 119 GB usable;
- approximately 52 GB district TPKX;
- approximately 52 GB matching MMPK;
- first target: Amazon Fire tablet for map-path acceptance;
- later target: GPS-capable personal Android phone for own-position acceptance.

The direct QGIS-built MBTiles remains a manufacturing/master artifact and is not required on this card.

---

## ArcGIS Pro MMPK result — PASS

ArcGIS Pro 3.7 was installed and used to wrap existing project TPKX files into modern MMPKs.

Minimal workflow:

```text
New Basemap
-> Add existing TPKX
-> Share
-> Mobile Map
-> Save package to file
-> Analyze
-> Package
```

Small specimen observations:

- analyzer: **0 errors / 0 warnings / 0 messages**;
- MMPK version 3.0;
- seven outer files;
- original TPKX preserved intact under `commondata/new_tpkx/`;
- `.mmap` directly references the packaged local TPKX;
- no HTTP/HTTPS references found in the small specimen `.mmap` / `.mapx`;
- Pro-created MMPK rendered in Windows ArcGIS Earth while Earth showed **Not signed in**.

A district-scale approximately 52 GB MMPK also packaged successfully from the existing approximately 52 GB district TPKX.

Interpretation: this proves the **manufacturing bridge**. It does **not** yet prove Field Maps runtime behavior.

---

## Field Maps current gate

### MMPK on physical microSD

Status: **VENDOR-DOCUMENTED / PROJECT LIVE TEST PENDING**.

Acceptance sequence:

1. finish copying the MMPK + TPKX to the physical card;
2. safely eject the card and insert it into the Fire;
3. open Field Maps;
4. go to **On Device**;
5. confirm the district MMPK appears;
6. open it and pan/zoom through Z17;
7. remove public Internet and repeat;
8. close/reopen Field Maps while still disconnected;
9. repeat later on a GPS-capable phone and verify own position;
10. test Field Maps restricted to Wi-Fi only while normal phone cellular service stays available.

Do not promote until the real device passes.

### Standalone TPKX on physical microSD

Status: **VENDOR-DOCUMENTED / PROJECT LIVE TEST PENDING**.

Keep it on the card as deliberate redundancy and as direct ArcGIS Earth Mobile content.

---

## Physical-card transport rule

Earlier Fire testing proved Android scoped storage blocks ordinary ADB/MTP-style injection into another app's protected `Android/data` tree.

Observed dead ends included:

- ADB push/move into `com.esri.fieldmaps` protected external storage;
- shell writes;
- MTP/File Explorer access through the protected tree.

Do not resume those tests unless a new capability materially changes the environment.

The current route follows Esri's documented physical-card sideload method: populate the card on the computer while it is outside Android, then insert the completed card into the device.

---

## Connectivity / authorization distinction

Keep these separate:

- **file validity / local package presence**;
- **Field Maps user authorization / sign-in behavior**.

Esri's sideload guidance does not describe a separate Internet activation or pre-exposure step that makes a local MMPK/TPKX file valid.

The standard Pro-created MMPK still needs the real cold-disconnected Field Maps test. Do not alter licensing metadata or attempt to bypass a control.

---

## Evidence snapshot

- Offline Map Factory 1.0: **BUILT / SELF-TESTED; LIVE ACCEPTANCE PENDING**.
- Historical TPKX Map Factory v1.0.0: **RELEASE-ACCEPTED / FROZEN**.
- MBTiles -> TPKX converter: **LIVE-PROVEN lineage**.
- ArcGIS Pro existing TPKX -> minimal MMPK: **PASS — small and district-scale packages created**.
- Pro-created MMPK in Windows ArcGIS Earth: **PASS — rendered while Earth showed Not signed in**.
- ArcGIS Earth Windows local TPKX: **LIVE-PROVEN**.
- ArcGIS Earth Mobile local TPKX: **LIVE-PROVEN on multiple packages**.
- Field Maps MMPK on physical microSD: **VENDOR-DOCUMENTED / PROJECT LIVE TEST PENDING**.
- Field Maps standalone TPKX on physical microSD: **VENDOR-DOCUMENTED / PROJECT LIVE TEST PENDING**.
- Native ArcGIS Earth GNSS: **LIVE-OBSERVED**, 9600 baud with GLL + RMC present.
- PRAVE -> ArcGIS Earth Automation API: **LIVE-PROVEN**.
- Map Fountain Windows TPKX-over-SMB: **LIVE-PROVEN / PARKED REFERENCE**.
- Map Fountain Android Static REST WMTS: **LIVE-PROVEN / PARKED REFERENCE**.
- Fire protected-folder ADB/MTP injection: **REJECTED / proven permission barrier**.
- TPKX -> MBTiles recovery: **REJECTED as production path**.

---

## Next Factory acceptance gate

The Factory itself still needs its independent product-line acceptance:

1. launcher starts correctly;
2. required QGZ files are found;
3. MBTiles-only build;
4. TPKX-only build;
5. Both build;
6. Advanced MBTiles -> TPKX;
7. finished TPKX opens and renders correctly in ArcGIS Earth;
8. cleanup and final-output behavior are correct.

Do not let the Android deployment success silently promote the Factory release line.

---

## REST / Static WMTS status

REST work remains **PARKED ENGINEERING HISTORY**.

Map Fountain is still a **LIVE-PROVEN / PARKED** reference and may return only if a real shared-storage need appears, such as Starlink/basecamp NAS, genuine multi-client use, or removable storage proving insufficient.

---

## Do not regress

- Do not replace the clean Factory with the REST experimental branch by inertia.
- Do not put developer clutter back at the user-facing package root.
- Do not casually rewrite the proven MBTiles -> TPKX converter.
- Do not revive TPKX -> MBTiles recovery as a production shortcut.
- Do not require router/server infrastructure for normal personal-phone deployment.
- Do not make public Internet mandatory.
- Do not return to protected-folder ADB/MTP injection as the normal Android solution.
- Do not treat a bare TPKX as a complete standalone Field Maps map card.
- Do not discard the standalone TPKX; it remains valuable redundancy and direct ArcGIS Earth Mobile content.
- Do not optimize storage elegance ahead of field reliability.
- Do not confuse vendor documentation or self-test success with project LIVE-PROVEN status.

---

## Known-good environment

- Windows 10/11 64-bit
- Python 3.14.5
- QGIS 3.44.9
- ArcGIS Pro 3.7 used for current MMPK bridge testing
- PNG tiles
- 96 DPI
- antialiasing ON
- metatile 4
- Z0-Z20

---

## Four-project map

1. `Offline-GeoStack` — master field mapping / manufacturing.
2. `Rasta-Pyramid-Factory` — giant-raster pyramid manufacturing.
3. `Map-Fountain` — live-proven router/storage delivery reference; parked / possible future Starlink NAS.
4. `Android-Field-Maps-and-ArcGIS-Earth-` — current personal-phone / physical-card deployment.

---

## Cold-start reading order

1. `README.md`
2. `ROADMAP.md`
3. `docs/PROJECT_STATUS_2026-08-20.md`
4. deployment repo `docs/FIELD_MAPS_MMPK_CARD_REFERENCE_2026-08-20.md`
5. `docs/SOFTWARE_AND_DOWNLOADS.md`
6. `docs/QUICK_START.md`
7. `releases/README.md`
8. Map Fountain only when router/network proof history matters
9. newest commits/issues

> **Keep the Factory simple. Put the heavy map on the card. Let the real target decide acceptance.**
