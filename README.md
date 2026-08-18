# Offline GeoStack

## QGIS → MBTiles / TPKX → offline field maps

**A Windows-first offline geospatial stack for manufacturing large raster map pyramids, packaging them as native TPKX, and putting the finished geography where the field user can reach it without depending on the public Internet.**

![Canonical ArcGIS Earth Systems router flowchart](https://raw.githubusercontent.com/Jim-dc95811/Map-Fountain/main/docs/arcgis_system_router_flowchart_2026-08-17.svg)

**Offline GeoStack** is the master operational project identity.

> **QGIS makes the pixels. The deployment path decides where those pixels live when the user needs them.**

---

## Current status at a glance

| Subsystem | Status |
| --- | --- |
| TPKX Map Factory v1.0.0 | ✅ **RELEASE-ACCEPTED / FROZEN** |
| QGIS → raster MBTiles manufacturing | ✅ **LIVE-PROVEN** |
| MBTiles → TPKX / Compact Cache V2 converter | ✅ **LIVE-PROVEN** |
| ArcGIS Earth Windows native TPKX runtime | ✅ **LIVE-PROVEN** |
| ArcGIS Earth Mobile local TPKX | ✅ **LIVE-PROVEN on multiple packages** |
| Native AE GNSS with actual field receiver | ✅ **LIVE-OBSERVED** |
| PRAVE → ArcGIS Earth Automation API | ✅ **LIVE-PROVEN** |
| Router-only Map Fountain — Windows TPKX over SMB | ✅ **LIVE-PROVEN / PARKED REFERENCE** |
| Router-only Map Fountain — Android Static REST WMTS | ✅ **LIVE-PROVEN / PARKED REFERENCE** |
| Android Field Maps TPKX on microSD | 🟡 **VENDOR-DOCUMENTED / PROJECT LIVE TEST PENDING** |
| TPKX Map Factory v1.4.0 REST-seed branch | 🟡 **TEST / SELF-TESTED — NOT RELEASE BASELINE** |
| TPKX → MBTiles recovery | ❌ **REJECTED as production path** |
| Operational public-Internet dependency | **NONE BY DESIGN** |

---

## Current field direction — carry the map

The most practical personal-phone deployment is now deliberately simple:

```text
QGIS / Factory
        ↓
finished native TPKX
        ↓
microSD card
        ↓
Android phone
        ↓
ArcGIS Field Maps or ArcGIS Earth
```

The map maker owns the complicated side. The field user should not have to learn QGIS, Python, projections, tile pyramids, or conversion internals.

Current map-card planning is based on real finished byte counts rather than guesses:

- **district — Z17**;
- **county — Z18**;
- **State Forests / selected high-value areas — Z20**;
- Google Hybrid and Esri imagery/labels where both are useful and storage allows.

The deployment work now has its own repository:

**[Android Field Maps + ArcGIS Earth](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-)**

That repository owns the personal-phone / microSD procedure, Field Maps acceptance work, cellular-data protection, and final user handoff.

---

## Why local pyramids matter

Raster map viewers work by continually requesting the tiles needed for the current screen and zoom level. One additional zoom level can require roughly four times as many deepest-level tile positions over the same area.

That is why streamed imagery can feel jerky in weak coverage even when the viewer itself is excellent.

Offline GeoStack changes the problem:

> **Have the pyramid ready before the user asks the screen to move.**

A local TPKX is not merely an emergency fallback. It can give the viewer the same useful raster detail without waiting for a cellular connection to deliver each new patch of imagery.

---

## TPKX Map Factory v1.0.0 — frozen accepted baseline

**Status: RELEASE-ACCEPTED — 2026-08-15**

Normal workflow:

```text
1. Choose map source
2. Choose map area
3. Choose zoom range
4. BUILD TPKX MAP
5. Open the finished .tpkx in ArcGIS Earth
```

Frozen map choices:

1. **Google Earth**
2. **Google Hybrid**
3. **Esri World**
4. **Esri World / Google Labels**

Frozen raster recipe:

- QGIS **3.44.9**
- Python **3.14.5** established known-good
- PNG raster tiles
- **96 DPI**
- antialiasing **ON**
- metatile **4**
- operator-selectable **Z0–Z20**

The exact accepted archive remains `TPKX_MAP_FACTORY_v1_0_0.zip`. Do not silently reconstruct it and call the result the accepted release.

---

## Later Factory TEST branches

Later work expanded the manufacturing choices beyond the frozen v1.0 public baseline.

### Direct MBTiles preservation

The accepted production lesson is simple:

- if MBTiles is needed, preserve the direct QGIS-built MBTiles;
- do **not** use reverse TPKX → MBTiles recovery as the production shortcut.

Recovered production MBTiles showed visual defects on the real mobile target even after controlled byte-level experiments looked promising.

### v1.3 / v1.4 REST exploration

Map Fountain's router-only Android proof led to an experimental Static REST WMTS manufacturing branch.

The production-scale v1.3 giant-tree/ZIP experiment exposed the cost of expanding, rereading, compressing, and moving hundreds of thousands of loose files.

`TPKX_MAP_FACTORY_v1_4_0_TEST` reset that experiment around a compact portable `.restmap` seed:

```text
verified MBTiles
→ compact <map>_REST.restmap seed
→ move one file
→ expand the disposable Static REST WMTS tree at the final SSD
```

The small lifecycle fixture is self-tested. This remains a **TEST branch**, and Map Fountain is no longer the primary personal-phone deployment direction. Do not confuse REST experimentation with the frozen v1.0 TPKX baseline.

---

## ArcGIS Earth runtime

ArcGIS Earth remains the current terrestrial chart plotter and a primary operational viewer.

Live-proven / observed project capabilities include:

- native local TPKX display;
- native TPKX opened directly from router Samba storage;
- ArcGIS Earth Mobile local TPKX on compatible packages;
- KML / KMZ / NetworkLinks;
- 3D navigation;
- native GNSS/NMEA own-position display;
- local Automation API;
- native drawings/markers;
- restoration of previously loaded desktop TPKX files.

### Native GNSS live observation — 2026-08-15

Known-good observed receiver input:

- **9600 baud**;
- GLL and RMC sentences present.

ArcGIS Earth displayed the operator's real-time own-position blue dot from the actual field GNSS receiver.

---

## ArcGIS Field Maps deployment target

Esri documents Android sideloading of `.tpk` / `.tpkx` basemaps directly to device storage or microSD.

Official Field Maps Android basemap folder:

```text
\Android\data\com.esri.fieldmaps\files\basemaps
```

Official reference:

- [ArcGIS Field Maps — Copy a basemap](https://doc.arcgis.com/en/field-maps/android/use-maps/configure-field-maps.htm)

The project has **not yet promoted its own Field Maps + microSD test to LIVE-PROVEN**. That real-phone acceptance belongs in the Android deployment repository.

---

## PRAVE / remote field positioning

The `$PRAVE` decoder has a **LIVE-PROVEN ArcGIS Earth Automation API path**.

Controlled traffic displayed units `7-101` through `7-106` as native ArcGIS Earth drawings using the established fire-truck RSSI icon family.

Forward field inputs include:

- `$PRAVE`;
- F22;
- native GNSS / NMEA;
- QR dispatch / bounded command input;
- KML/KMZ / NetworkLinks where interoperability makes KML the right tool.

---

## Rasta Pyramid Factory

[Rasta Pyramid Factory](https://github.com/Jim-dc95811/Rasta-Pyramid-Factory) generalizes the raster-manufacturing side beyond ordinary geographic map extents.

It is LIVE-PROVEN across giant flat-image and georeferenced-raster inputs, including gigapixel-class imagery.

Rasta's useful principle is the same as the map Factory: turn a large monolithic raster into a true multiscale pyramid so the viewer can move from overview to deep detail smoothly.

Rasta products can also ride on local storage when a field user wants deep-zoom reference imagery or when spare SD-card capacity would otherwise sit unused.

---

## Map Fountain — proven, then simplified away from the normal phone

[Map Fountain](https://github.com/Jim-dc95811/Map-Fountain) produced two important live proofs:

### Windows

```text
native TPKX on USB SSD
→ GL.iNet Flint 2
→ Samba / SMB
→ Wi-Fi
→ Windows
→ ArcGIS Earth
```

ArcGIS Earth opened a production-scale native TPKX directly from the router-attached SSD over Wi-Fi.

### Android

```text
Static REST WMTS folder
→ USB SSD
→ Flint 2 HTTPS/WebDAV
→ Wi-Fi
→ ArcGIS Earth Mobile
```

That also passed, including a cache-clear/restart retest.

Those proofs remain valuable engineering evidence. The project has now **parked Map Fountain from the primary personal-phone deployment path** because removable local storage is simpler for the intended user.

Map Fountain may return in a different role: **Starlink-connected basecamp storage / poor-man's NAS**, where shared local storage and Internet access are both useful but the local LAN still survives loss of outside connectivity.

---

## Four-project family

1. **Offline GeoStack** — master field-mapping and TPKX manufacturing system.
2. **[Rasta Pyramid Factory](https://github.com/Jim-dc95811/Rasta-Pyramid-Factory)** — general giant-raster / deep-zoom pyramid manufacturing.
3. **[Map Fountain](https://github.com/Jim-dc95811/Map-Fountain)** — proven router/storage delivery experiments; now parked reference / possible future basecamp NAS.
4. **[Android Field Maps + ArcGIS Earth](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-)** — deployment to normal Android users and microSD cards.

---

## No operational Internet dependency

> **There can be no operational dependence on Internet connectivity. Period.**

This means outside/public Internet dependency. It does not prohibit useful local networking when local networking is the right tool.

The current personal-phone direction goes even simpler: the map itself can live on the phone's removable storage.

Online services may enhance preparation, refresh source imagery, or provide optional live information. Loss of outside Internet must not erase the user's geographic context.

---

## Evidence discipline

Project status labels remain strict:

- **DESIGNED**
- **BUILT / SELF-TESTED**
- **LIVE-OBSERVED**
- **LIVE-PROVEN**
- **RELEASE-ACCEPTED / FROZEN**

The intended target decides acceptance. A clever converter, clean self-test, vendor feature page, or fast benchmark is not enough by itself.

---

## Start here

- **[Android deployment / SD-card project](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-)**
- **[Software & Downloads](docs/SOFTWARE_AND_DOWNLOADS.md)**
- **[Quick Start](docs/QUICK_START.md)**
- **[TPKX Map Factory v1.0.0 release record](releases/README.md)**
- **[Required QGIS project files](required_qgis_projects/)**
- **[Technical Architecture](docs/TECHNICAL_ARCHITECTURE.md)**
- **[PRAVE → ArcGIS Earth live integration](docs/PRAVE_ARCGIS_EARTH_INTEGRATION.md)**
- **[Offline doctrine / Persistent Geographic Context](docs/OFFLINE_OPERATION_AND_PERSISTENT_GEOGRAPHIC_CONTEXT.md)**
- **[Map Fountain proof archive](https://github.com/Jim-dc95811/Map-Fountain)**

---

## Licensing and source-data boundary

Original Offline GeoStack software and documentation are published under the **MIT License** unless a file states otherwise.

That does **not** grant rights to third-party imagery, labels, basemaps, vendor software, or external services. Source licensing, caching, export, attribution, and redistribution rules remain source-specific.

---

## Authorship and AI collaboration

The project is developed and published by **Jim Gaddy** with **ChatGPT / Tool Master** serving as technical design, coding, GIS research, documentation, packaging, and diagnostic partner.

The project uses a closed-loop engineering method: build the smallest controlled bridge, run it on the real target, treat screenshots/logs/packet captures/files as telemetry, and only then promote the result.

---

# Offline GeoStack

**Manufacture the geography once. Put it where the field user can reach it without asking the network for permission.**
