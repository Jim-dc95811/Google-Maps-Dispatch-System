# Offline GeoStack

## QGIS → MBTiles / TPKX → ArcGIS Earth Desktop + Mobile + Live Field Positioning

**A Windows-first offline geospatial stack for manufacturing native raster map products, carrying them into the field, serving them through simple local infrastructure, and feeding live GNSS / PRAVE / F22 / QR data without depending on the public Internet at showtime.**

![ArcGIS Earth Systems — router-only Map Fountain architecture](https://raw.githubusercontent.com/Jim-dc95811/Map-Fountain/main/docs/map_fountain_router_architecture_2026-08-17.svg)

**Offline GeoStack** is the master operational project identity.

> **QGIS makes the pixels. The deployment path decides how those pixels reach the operator.**

> **Build it online. Carry it offline. Serve it locally when that is the better tool.**

---

## Current status at a glance

| Subsystem | Status |
| --- | --- |
| TPKX Map Factory v1.0.0 | ✅ **RELEASE-ACCEPTED / FROZEN** |
| QGIS → raster MBTiles manufacturing | ✅ **LIVE-PROVEN** |
| MBTiles → TPKX / Compact Cache V2 converter | ✅ **LIVE-PROVEN** |
| ArcGIS Earth Windows native TPKX runtime | ✅ **LIVE-PROVEN** |
| ArcGIS Earth Mobile local TPKX | ✅ **LIVE-PROVEN on multiple packages** |
| Router-only Map Fountain — USB SSD + Flint 2 + Samba | ✅ **LIVE-PROVEN** |
| Large TPKX Ethernet storage benchmark | ✅ **LIVE-PROVEN** |
| Large TPKX Wi-Fi storage benchmark | ✅ **LIVE-PROVEN** |
| ArcGIS Earth direct network-hosted TPKX over Wi-Fi | ✅ **LIVE-PROVEN** |
| Historical Windows MBTiles → HTTPS WMTS → Android path | ✅ **LIVE-PROVEN HISTORY** |
| PRAVE → ArcGIS Earth Automation API | ✅ **LIVE-PROVEN** |
| AE session restoration of loaded TPKX | ✅ **LIVE-OBSERVED** |
| Native AE GNSS with actual field receiver | ✅ **LIVE-OBSERVED** |
| TPKX → MBTiles recovery | ❌ **REJECTED as production path** |
| Operational public-Internet dependency | **NONE BY DESIGN** |

---

## Major milestone — router-only Map Fountain, 2026-08-17

The field map appliance was simplified to:

```text
native TPKX on USB SSD
        ↓
GL.iNet Flint 2
        ↓
Samba / SMB
        ↓
Ethernet or Wi-Fi
        ↓
Windows laptop
        ↓
ArcGIS Earth
```

The production-scale `ESG1N.tpkx` package was benchmarked through the router over Ethernet and Wi-Fi, then opened directly from the Samba share and rendered interactively in ArcGIS Earth over Wi-Fi.

Large specimen:

- `ESG1N.tpkx`
- benchmark size: **26,174,899,216 bytes**
- Windows File Explorer identification: **25,561,426 KB**

Ethernet benchmark:

- random seek: **25.33 MiB/s**
- random p95: **9.98 ms**
- four-client aggregate: **51.21 MiB/s**
- sequential: **42.58 MiB/s**

Wi-Fi benchmark:

- random seek: **5.19 MiB/s**
- random p95: **50.56 ms**
- four-client aggregate: **5.31 MiB/s**
- sequential: **6.14 MiB/s**

The key result is not the synthetic speed number. **ArcGIS Earth itself successfully opened and rendered the native TPKX while it remained on the router-attached SSD.**

The current field-appliance rule is now simple:

> **Keep the router dumb. Keep the maps native. Let ArcGIS Earth do the GIS work.**

See the standalone **[Map Fountain](https://github.com/Jim-dc95811/Map-Fountain)** repository for the acceptance record and evidence hashes.

---

## Current architecture

Offline GeoStack separates **map manufacturing**, **map storage/delivery**, and **map use**.

```text
MAP MANUFACTURING
map sources / imagery
        ↓
QGIS 3.44.9 + Python tools
        ↓
verified raster MBTiles
        ↓
        ├── preserve MBTiles
        └── Compact Cache V2 converter → native TPKX

FIELD DELIVERY
finished native products
        ↓
USB SSD
        ↓
consumer router + Samba
        ↓
private Ethernet / Wi-Fi
        ↓
ArcGIS Earth clients

LIVE FIELD DATA
GNSS / PRAVE / F22 / QR
        ↓
ArcGIS Earth native inputs / Automation API
```

No public Internet connection is required for the core local map path.

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

## TPKX Map Factory later TEST branch

The later output-choice branch exposes:

```text
TPKX
MBTiles
Both
```

Important rule:

- direct QGIS-built MBTiles are the accepted way to preserve MBTiles;
- experimental reverse TPKX → MBTiles recovery was rejected after production mobile visual defects;
- the frozen `MBTiles_to_TPKX_v0_1_0.py` converter remains the proven forward path.

---

## ArcGIS Earth runtime

ArcGIS Earth is the current terrestrial chart plotter and primary operational viewer.

Live-proven / observed project capabilities include:

- native local TPKX display;
- native TPKX opened directly from a router Samba share;
- ArcGIS Earth Mobile local TPKX on compatible packages;
- KML / KMZ / NetworkLinks;
- 3D navigation;
- native GNSS/NMEA own-position display;
- local Automation API;
- native drawings/markers;
- restoration of previously loaded desktop TPKX files.

### Native GNSS live observation — 2026-08-15

Known-good observed receiver input:

- **9600 baud**
- GLL and RMC sentences present

ArcGIS Earth displayed the operator's real-time own-position blue dot from the actual field GNSS receiver.

---

## PRAVE / remote field positioning

The `$PRAVE` decoder has a **LIVE-PROVEN ArcGIS Earth Automation API path**.

Controlled test traffic displayed units `7-101` through `7-106` as native ArcGIS Earth drawings using the established fire-truck RSSI icon family.

Observed healthy state included:

```text
UNITS=6
API_OK=47
API_BAD=0
BAD_RMC=0
BAD_PRAVE=0
RMC=FRESH
```

Forward field inputs include:

- `$PRAVE`
- F22
- native GNSS / NMEA
- QR dispatch / bounded command input
- KML/KMZ / NetworkLinks where interoperability makes KML the right tool

---

## Rasta Pyramid Factory

[Rasta Pyramid Factory](https://github.com/Jim-dc95811/Rasta-Pyramid-Factory) generalizes the raster-manufacturing side beyond ordinary geographic map extents.

It is LIVE-PROVEN across giant flat-image and georeferenced-raster inputs, including gigapixel-class imagery, and can publish:

```text
MBTiles
TPKX
Both
```

Rasta manufactures the pixels. Map Fountain carries the finished products. ArcGIS Earth consumes them.

---

## Historical Windows Map Fountain path

On 2026-08-16 a Windows-hosted implementation proved:

```text
raster MBTiles
→ local HTTPS WMTS
→ Android USB tether
→ ArcGIS Earth Mobile
```

It proved local/offline mobile tile consumption, HTTPS, QR loading, per-map service identity, multiple substantial MBTiles, and continued operation with outside Internet removed.

That remains engineering history and a useful compatibility technique. **The current field-appliance direction is router-only.**

---

## No operational Internet dependency

> **There can be no operational dependence on Internet connectivity. Period.**

The doctrine concerns outside connectivity, not useful private local networking.

Allowed and encouraged where useful:

- local USB storage;
- private Ethernet;
- private Wi-Fi;
- Samba file sharing;
- local device-to-device communication.

Online services may enhance preparation or convenience, but the core field map system must remain usable when the public Internet disappears.

---

## Evidence discipline

Project status labels remain strict:

- **DESIGNED**
- **BUILT / SELF-TESTED**
- **LIVE-OBSERVED**
- **LIVE-PROVEN**
- **RELEASE-ACCEPTED / FROZEN**

The intended target decides acceptance. A clever converter, clean self-test, or fast benchmark is not enough if ArcGIS Earth does not render the real product correctly.

---

## Start here

- **[Map Fountain router-only live proof](https://github.com/Jim-dc95811/Map-Fountain)**
- **[Software & Downloads](docs/SOFTWARE_AND_DOWNLOADS.md)**
- **[Quick Start](docs/QUICK_START.md)**
- **[TPKX Map Factory v1.0.0 release record](releases/README.md)**
- **[Required QGIS project files](required_qgis_projects/)**
- **[Technical Architecture](docs/TECHNICAL_ARCHITECTURE.md)**
- **[PRAVE → ArcGIS Earth live integration](docs/PRAVE_ARCGIS_EARTH_INTEGRATION.md)**
- **[Offline doctrine / Persistent Geographic Context](docs/OFFLINE_OPERATION_AND_PERSISTENT_GEOGRAPHIC_CONTEXT.md)**

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

**QGIS → native map products → router-only local delivery → ArcGIS Earth → live field position.**

> **It is not the number of bytes that matters. It is what the bytes are doing.**
