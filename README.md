# Offline GeoStack

## QGIS → MBTiles / TPKX → ArcGIS Earth Desktop + Mobile + Live Field Positioning

**A Windows-first offline geospatial stack for manufacturing raster map pyramids, carrying them as native TPKX, serving them locally as MBTiles/WMTS, and feeding live GNSS / PRAVE / F22 / QR field data without depending on the Internet at showtime.**

![System architecture](https://raw.githubusercontent.com/Jim-dc95811/Map-Fountain/main/docs/ChatGPT%20Image%20Aug%2016%2C%202026%2C%2007_11_25%20PM.png)

This repository began life as the **Google Maps Dispatch System**. That lineage is preserved, but the 2026 architecture has outgrown the old name.

**Offline GeoStack** is the master project identity.

> **QGIS makes the pixels. The deployment path decides how those pixels reach the operator.**

> **Build it online. Carry it offline. Serve it locally when that is the better tool.**

---

## Status at a glance

| Subsystem | Status |
| --- | --- |
| TPKX Map Factory v1.0.0 | ✅ **RELEASE-ACCEPTED / FROZEN** |
| QGIS → raster MBTiles manufacturing | ✅ **LIVE-PROVEN** |
| MBTiles → TPKX / Compact Cache V2 converter | ✅ **LIVE-PROVEN** |
| Advanced existing-MBTiles → TPKX conversion | ✅ **LIVE-PROVEN** |
| ArcGIS Earth Windows native TPKX runtime | ✅ **LIVE-PROVEN** |
| ArcGIS Earth Mobile local TPKX | ✅ **LIVE-PROVEN on multiple packages** |
| USB Map Fountain v0.2.1 TEST — MBTiles → HTTPS WMTS → Android | ✅ **LIVE-PROVEN** |
| USB Map Fountain with outside Internet removed | ✅ **LIVE-PROVEN** |
| TPKX Map Factory v1.2.0 TEST — TPKX / MBTiles / Both | 🟡 **BUILT / SELF-TESTED; live acceptance underway** |
| PRAVE → ArcGIS Earth Automation API | ✅ **LIVE-PROVEN** |
| AE session restoration of loaded TPKX | ✅ **LIVE-OBSERVED** |
| Native AE GNSS with actual field receiver | ✅ **LIVE-OBSERVED** |
| TPKX → MBTiles recovery | ❌ **REJECTED as production path after mobile visual defects** |
| Operational Internet dependency | **NONE BY DESIGN** |

---

## Start here

- **[Software & Downloads — exact versions + official links](docs/SOFTWARE_AND_DOWNLOADS.md)**
- **[Quick Start](docs/QUICK_START.md)**
- **[ArcGIS Earth Mobile + USB Map Fountain](docs/ARCGIS_EARTH_MOBILE_MAP_FOUNTAIN.md)**
- **[TPKX Map Factory v1.0.0 release record](releases/README.md)**
- **[Required QGIS project files](required_qgis_projects/)**
- **[Professional GIS Engineering Record](docs/professional_report/README.md)**
- **[Technical Architecture](docs/TECHNICAL_ARCHITECTURE.md)**
- **[PRAVE → ArcGIS Earth live integration](docs/PRAVE_ARCGIS_EARTH_INTEGRATION.md)**
- **[Offline doctrine / Persistent Geographic Context](docs/OFFLINE_OPERATION_AND_PERSISTENT_GEOGRAPHIC_CONTEXT.md)**

The exact release-accepted Windows archive is named `TPKX_MAP_FACTORY_v1_0_0.zip`. It remains preserved in the project’s canonical working archive. A connector-truncated GitHub copy was deliberately removed rather than leaving a bad public download; the exact binary should still be attached directly to GitHub before public release distribution.

---

## Current architecture

The project now has **two deliberate raster deployment paths from the same MBTiles manufacturing stage**.

```text
Map source / QGIS layer stack
          ↓
QGIS 3.44.9 raster rendering
          ↓
verified raster MBTiles
          ↓
          ├──────────────────────────────────────────────┐
          │                                              │
          │                                              │
          ↓                                              ↓
Custom MBTiles → TPKX converter                  USB Map Fountain
(Esri Compact Cache V2)                          local HTTPS WMTS
          ↓                                              ↓
native .tpkx                                  Android USB tether
          ↓                                              ↓
ArcGIS Earth Windows / Mobile                 ArcGIS Earth Mobile
```

The two paths solve different operational problems:

- **TPKX** is a self-contained native package for local file use in ArcGIS Earth.
- **MBTiles + Map Fountain** keeps a larger map library on the Windows PC / attached SSD and sends only the requested raster tiles to ArcGIS Earth Mobile over a private local link.

Neither path requires outside Internet connectivity at incident/showtime.

---

## TPKX Map Factory v1.0.0 — frozen accepted baseline

**Status: LIVE-PROVEN / RELEASE-ACCEPTED — 2026-08-15**

Normal-user workflow:

```text
1. Choose map source
2. Choose map area
3. Choose zoom range
4. BUILD TPKX MAP
5. Open the finished .tpkx in ArcGIS Earth
```

The v1.0.0 GUI exposes four frozen map choices:

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
- manufacturing format: **MBTiles**
- accepted v1.0 final operator deliverable: **one `.tpkx`**

Advanced v1.0 path:

**ADVANCED: MBTILES → TPKX**

The accepted v1.0.0 ZIP and converter remain frozen even while later TEST branches expand the workflow.

---

## TPKX Map Factory v1.2.0 TEST

**Status: BUILT / SELF-TESTED; Windows live acceptance underway — 2026-08-16**

The live mobile work changed the value of the MBTiles stage. MBTiles is no longer merely disposable manufacturing material when Map Fountain deployment is desired.

v1.2 therefore exposes the normal build choice:

```text
TPKX
MBTiles
Both
```

Current TEST behavior:

- **TPKX** — QGIS manufactures MBTiles, the frozen proven converter creates TPKX, and the TPKX is published.
- **MBTiles** — QGIS manufactures and verifies MBTiles, publishes it directly, and does not invoke the TPKX converter.
- **Both** — one QGIS-manufactured MBTiles pyramid is preserved and also fed to the same frozen converter to create TPKX.
- **Both is the current TEST default.**
- Advanced **MBTiles → TPKX** remains available.
- Experimental **TPKX → MBTiles recovery was removed** after a recovered production map showed blurred/missing regions on ArcGIS Earth Mobile.

The frozen `MBTiles_to_TPKX_v0_1_0.py` converter remains unchanged.

---

## USB Map Fountain — mobile local serving

**Status: LIVE-PROVEN — 2026-08-16**

The live-proven chain is:

```text
MBTiles on Windows PC / SSD
        ↓
Rasta USB Map Fountain v0.2.1 TEST
        ↓
HTTPS WMTS
        ↓
Android USB tether / Remote NDIS
        ↓
ArcGIS Earth Mobile
```

Observed live results:

- local PC-to-phone network confirmed through Android USB tethering;
- ArcGIS Earth Mobile requested real WMTS raster tiles and received HTTP `200` responses;
- HTTPS transport became functional;
- QR-based service loading became functional;
- map display continued with outside Internet removed;
- three different substantial MBTiles were displayed successfully;
- a large Lago panorama displayed and navigated smoothly on Android;
- each selected MBTiles now receives a unique service/map identity so stale tiles from a prior map are not reused.

Live mobile operating note:

> **Deliberate pan/zoom is smooth and reliable. Rapid repeated zooming or whipping the view around can outrun the current delivery/render path. Move deliberately and let the map settle.**

See [ArcGIS Earth Mobile + USB Map Fountain](docs/ARCGIS_EARTH_MOBILE_MAP_FOUNTAIN.md) for the complete evidence record and current engineering boundaries.

---

## ArcGIS Earth Mobile local TPKX

Local-file TPKX use is also live-proven on Android.

Observed successful packages include:

- Rasta-produced Thames Bridge TPKX;
- a smaller Esri map TPKX;
- a smaller Google Hybrid TPKX.

One larger Google Hybrid package returned `spatial reference not supported`. Because other packages loaded correctly, treat mobile TPKX compatibility as package-specific until that metadata difference is isolated. Do not turn the one failure into a blanket claim that Mobile rejects Factory TPKX.

---

## The converter in one screenful

```text
MBTiles SQLite tiles
  zoom_level
  tile_column
  tile_row
  tile_data
        ↓
TMS row → ArcGIS top-origin row
        ↓
128 × 128 Compact Cache V2 bundle addressing
        ↓
.bundle binary records + indexes
        ↓
root.json + iteminfo.json + thumbnail
        ↓
ZIP64 .tpkx
```

Critical TMS row conversion:

```text
y_arcgis = (2^z - 1) - y_tms
```

Tile placement and bundle indexing are deterministic. The raster tile bytes produced by QGIS are preserved rather than resampled into a new cartographic pyramid.

---

## Live acceptance evidence — desktop map manufacturing

### First integrated Factory proof

- Source: Google Hybrid
- Area: 113.31 sq mi
- Zooms: Z8–Z18
- Tiles: 23,119
- Windows File Explorer size: **3,560,735 KB**
- Elapsed: **0:13:55**
- ArcGIS Earth: **PASS**

### Large advanced MBTiles → TPKX proof

- Tiles: **271,497**
- Bundles: **47**
- Zooms: Z8–Z18
- Windows File Explorer size: **25,561,426 KB**
- Elapsed: **0:17:59**
- ArcGIS Earth: **PASS**

### Large Esri World / Google Labels Factory proof

- Area: approximately 1,378.89 sq mi
- Tiles: **271,242**
- Zooms: Z8–Z18
- Windows File Explorer size: **24,291,406 KB**
- Elapsed: **2:51:52**
- ArcGIS Earth: **PASS**

### v1.0.0 release smoke test

- Output: `test2 small.tpkx`
- Windows-visible output size: **12,852 KB**
- Elapsed: **0:00:12**
- ArcGIS Earth: **PASS**

For finished TPKX output, **the intended ArcGIS Earth runtime remains the final acceptance authority**.

---

## ArcGIS Earth runtime + native GNSS

ArcGIS Earth remains the primary 3D operational viewer.

### Native GNSS live observation — 2026-08-15

![ArcGIS Earth native GNSS live observation](docs/images/native_gnss_live_2026-08-15.jpg)

*ArcGIS Earth displaying the operator's real-time blue-dot own position from the actual field GNSS receiver. Known-good observed input was 9600 baud with GLL and RMC NMEA sentences.*

Relevant capabilities observed or proven in this project include:

- native local TPKX display;
- ArcGIS Earth Mobile local TPKX display on compatible packages;
- local WMTS consumption on ArcGIS Earth Mobile;
- KML/KMZ and NetworkLinks;
- 3D globe navigation;
- native GNSS/NMEA capability;
- local Automation API;
- native drawing / marker display;
- session restoration of previously loaded desktop TPKX files.

Online services are enhancements, not dependencies.

---

## No operational Internet dependency

> **There can be no operational dependence on Internet connectivity. Period.**

The doctrine is about **outside connectivity**, not about forbidding useful private local links.

Both of these fit the doctrine:

```text
local TPKX on the device
```

and

```text
local MBTiles depot
→ private USB / local network
→ local WMTS
→ ArcGIS Earth Mobile
```

The second path was specifically proven while outside Internet connectivity was removed.

The project uses **Persistent Geographic Context** for the operating condition in which position, surroundings, routes, and terrain remain continuously visible without having to summon them from the public Internet.

---

## Live positioning and field inputs

Offline GeoStack is not only a map factory.

The `$PRAVE` decoder has a **LIVE-PROVEN ArcGIS Earth Automation API path**. Controlled traffic displayed units `7-101` through `7-106` as native ArcGIS Earth drawings using the established fire-truck RSSI icon family.

Observed healthy test state included:

```text
UNITS=6
API_OK=47
API_BAD=0
BAD_RMC=0
BAD_PRAVE=0
RMC=FRESH
```

Forward inputs include:

- `$PRAVE`
- F22
- native GNSS / NMEA
- QR dispatch / bounded command input
- KML/KMZ / NetworkLinks where interoperability makes KML the correct tool

---

## Required QGIS projects

The current reference projects are included in [`required_qgis_projects/`](required_qgis_projects/):

- `REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz`
- `ESRI and Google Labels.qgz`

Install location:

```text
C:\Google Earth Project\QGIS\
```

---

## Repository map

- `README.md` — public front door
- `ROADMAP.md` — current next gates
- `CHANGELOG.md` — architecture chronology
- `docs/ARCGIS_EARTH_MOBILE_MAP_FOUNTAIN.md` — Android / USB Map Fountain live proof
- `docs/SOFTWARE_AND_DOWNLOADS.md` — exact dependency versions and official download links
- `docs/README.md` — documentation index and architecture diagram
- `docs/TECHNICAL_ARCHITECTURE.md` — converter / pipeline engineering
- `docs/professional_report/` — long-form professional GIS and future-AI record
- `docs/PRAVE_ARCGIS_EARTH_INTEGRATION.md` — live positioning path
- `docs/OFFLINE_OPERATION_AND_PERSISTENT_GEOGRAPHIC_CONTEXT.md` — offline doctrine
- `docs/AI_ENGINEERING_METHOD.md` — human/AI development method
- `required_qgis_projects/` — current QGIS reference projects
- `releases/` — release notes, checklist, lineage, and binary-release status
- `docs/legacy/` — preserved Google Earth lineage

---

## Licensing and source-data boundary

Original Offline GeoStack software and documentation are published under the **MIT License** unless a file states otherwise.

That does **not** grant rights to third-party imagery, labels, basemaps, vendor software, or external services. Map-source licensing, caching, export, attribution, and redistribution rules remain source-specific. See [`NOTICE.md`](NOTICE.md) and [`docs/SOURCE_AND_LICENSING_NOTE.md`](docs/SOURCE_AND_LICENSING_NOTE.md).

---

## Authorship and AI collaboration

The project is developed and published by **Jim Gaddy** with **ChatGPT / Tool Master** serving as technical design, coding, GIS research, documentation, packaging, and diagnostic partner.

The project repeatedly demonstrates a closed-loop method: build the smallest controlled bridge, run it on the real target, treat screenshots/logs/files as telemetry, and only then promote the result from designed → built → live-proven.

---

# Offline GeoStack

**QGIS → MBTiles / TPKX → ArcGIS Earth Desktop + Mobile + Live Field Positioning**

> **It is not the number of bytes that matters. It is what the bytes are doing.**
