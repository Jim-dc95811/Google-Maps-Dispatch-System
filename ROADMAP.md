# Offline GeoStack Roadmap

The release-accepted **TPKX Map Factory v1.0.0** remains frozen. New capability is developed in later TEST branches and promoted only after real-target acceptance.

## Frozen v1.0 baseline

- ✅ TPKX Map Factory v1.0.0 release accepted
- ✅ QGIS 3.44.9 raster manufacturing
- ✅ custom MBTiles → Compact Cache V2 / TPKX bridge
- ✅ advanced existing-MBTiles conversion
- ✅ ArcGIS Earth Windows native TPKX runtime
- ✅ PRAVE → ArcGIS Earth Automation API proof
- ✅ no operational Internet dependency for core map display

---

## Current primary direction — local removable deployment

The active field question is no longer whether a router can serve maps. That has been proven.

The current question is how much useful geography can be put directly on ordinary Android phones with the least possible operator complexity.

```text
Factory-built TPKX
→ microSD card
→ Android
→ ArcGIS Field Maps / ArcGIS Earth
```

Deployment work lives in:

**[Android Field Maps + ArcGIS Earth](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-)**

### Immediate map-size gates

Measure real finished products before freezing card tiers:

1. district-wide Z17;
2. county-level Z18;
3. selected State Forest / high-value Z20 areas;
4. Google Hybrid versus Esri imagery/labels equivalents where both are useful.

Record exact finished sizes and elapsed build times.

### Immediate Field Maps gate

Esri documents sideloaded TPKX basemaps on Android/device microSD. The project must still run its own controlled target test.

Acceptance requires:

- known-good TPKX placed in the Field Maps basemap folder on microSD;
- Field Maps sees and selects the local basemap;
- Android app-level network setting blocks Field Maps cellular data;
- Wi-Fi removed;
- local imagery continues to pan/zoom;
- own-position behavior checked;
- close/reopen persistence checked.

Do not promote this project path to LIVE-PROVEN before that test passes.

---

## Factory development

### v1.0.0

Remains **RELEASE-ACCEPTED / FROZEN**.

### Direct MBTiles output

Preserve direct QGIS-built MBTiles when MBTiles is needed. Reverse TPKX → MBTiles recovery remains rejected as a production shortcut.

### v1.3 / v1.4 Static REST exploration

Map Fountain's Android proof triggered a Static REST WMTS manufacturing branch.

The v1.3 production-scale giant-tree/ZIP experiment exposed major file-count and packaging overhead.

`TPKX_MAP_FACTORY_v1_4_0_TEST` moved to a compact portable `.restmap` seed that expands the disposable WMTS tree at the final SSD location.

Status:

- small lifecycle fixture: **SELF-TESTED**;
- full production acceptance: **NOT FROZEN**;
- current priority: **lower than direct local TPKX / microSD deployment**.

Keep the branch as engineering work. Do not let it redefine the accepted Factory baseline by inertia.

---

## Map Fountain — proven / parked

Map Fountain remains a valuable proof record, not the current default personal-phone architecture.

### Windows proof

```text
native TPKX on USB SSD
→ GL.iNet Flint 2
→ Samba / SMB
→ Wi-Fi
→ Windows
→ ArcGIS Earth
```

Status: ✅ **LIVE-PROVEN**.

### Android router proof

```text
Static REST WMTS
→ USB SSD
→ Flint 2 local HTTPS/WebDAV
→ Wi-Fi
→ ArcGIS Earth Mobile
```

Status: ✅ **LIVE-PROVEN**.

### Current disposition

**PARKED from the primary personal-phone deployment path.**

Possible future role:

```text
Starlink
→ Flint 2 WAN
→ USB SSD
→ local SMB / Wi-Fi / Ethernet
→ basecamp laptops and local consumers
```

That would be a practical poor-man's NAS / incident map reservoir, not a reason to complicate every phone.

---

## Rasta Pyramid Factory

Rasta remains the sibling project for arbitrary giant rasters and deep-zoom imagery.

Current live-proven baseline: v0.1.3.

A later v0.1.4 TEST added independent TPKX / MBTiles / REST outputs, but its REST branch remains a TEST branch tied to the Map Fountain exploration. Rasta's core value does not depend on REST or router delivery.

Potential deployment use: spare SD-card capacity can carry deep-zoom cityscapes, historical scans, specialty maps, or other large raster pyramids when useful.

---

## Field integration

### Native GNSS

**Status: ✅ LIVE-OBSERVED — 2026-08-15**

Known-good observed input: **9600 baud**, GLL + RMC present.

### PRAVE

PRAVE → ArcGIS Earth Automation API remains **LIVE-PROVEN**.

### F22 / QR / KML

Keep as field/live/interoperability input paths. Add only when the real operational use calls for them.

---

## Public documentation priorities

- keep the four repositories cross-linked and role-specific;
- keep v1.0.0 clearly separated from TEST branches;
- preserve Map Fountain as proof history without presenting it as mandatory field hardware;
- document the Android microSD workflow without turning the public guide into a GIS encyclopedia;
- preserve the one-page Field Maps procedure as the normal-user handoff;
- publish real card-size results after the district/county/Z20 builds finish;
- retain Google Earth / KML work as lineage, not current baseline.

---

## Non-goals

- forcing ordinary field users to run the Factory;
- requiring a router/server for the normal personal-phone map path;
- rebuilding QGIS inside the Factory;
- rebuilding ArcGIS Earth or Field Maps;
- making public Internet connectivity mandatory;
- reviving Raspberry Pi / Pi-server architecture by default;
- using rejected TPKX recovery as a shortcut;
- promoting vendor documentation to project LIVE-PROVEN status without target testing;
- adding GIS features merely because the software exposes them.

## Governing rules

> **New capability must earn its way into the baseline by answering to the real target.**

For personal mobile deployment:

> **Make the map once. Put it on the card. Let the phone read local bytes.**
