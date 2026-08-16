# Offline GeoStack Roadmap

The v1.0 map-manufacturing baseline is frozen. The roadmap expands the stack **around** proven components rather than reopening them casually.

## v1.0 baseline — frozen

- ✅ TPKX Map Factory v1.0.0 release accepted
- ✅ QGIS 3.44.9 raster manufacturing
- ✅ custom MBTiles → Compact Cache V2 / TPKX bridge
- ✅ advanced existing-MBTiles conversion
- ✅ ArcGIS Earth native TPKX runtime
- ✅ PRAVE → ArcGIS Earth Automation API proof
- ✅ no operational Internet dependency for core map display

## Near-term field integration

### Native GNSS acceptance

**Status:** ✅ LIVE-PROVEN — 2026-08-15

The actual field GNSS receiver successfully drove ArcGIS Earth native realtime location on Windows. Known-good bench configuration is **9600 baud** with **GLL and RMC NMEA sentences** present in the stream. ArcGIS Earth displayed the native blue-dot own position without Python or a custom ME plotting path.

Keep this simple for normal operators: prefer ArcGIS Earth native GNSS when the actual field receiver and serial architecture permit it.

### F22 → common live-position manager

**Status:** designed

Decode F22 at the protocol edge and normalize it into the same ArcGIS Earth live-position abstraction used by other remote-unit inputs. Do not create a second renderer merely because the transport differs.

### QR → ArcGIS Earth

**Status:** modernization candidate

Preserve QR as an optical/physical dispatch and command input. Preferred modern output is a bounded Automation API action: destination marker, fly-to, layer toggle, operating-view reset, or other allowlisted command.

## Map-production expansion

### v1.1 output-format choice

**Status:** strong candidate

The v1.0 Factory already manufactures a finished raster MBTiles before invoking the proven MBTiles → TPKX converter. A future v1.1 GUI can expose that existing production stage as a supported final deliverable without changing the rendering engine.

Proposed operator choices:

```text
TPKX
MBTiles
Both
```

Behavior:

- **TPKX** — preserve the accepted v1.0 behavior: manufacture temporary MBTiles, convert it, verify the TPKX, and publish the TPKX.
- **MBTiles** — manufacture and verify the raster MBTiles, publish it as the final product, and stop before conversion.
- **Both** — publish the verified MBTiles and then use the same proven converter to publish the TPKX as well.

Keep **TPKX** as the default so the v1.0 operator workflow remains familiar. Do not fork the QGIS rendering path merely to create the MBTiles edition; both outputs must come from the same proven manufacturing engine.

This opens the Factory to users and applications that want raster MBTiles but have no interest in ArcGIS Earth.

### More QGIS recipes

**Status:** open for v1.1+

The four-source v1.0 menu stays frozen. Additional cartographic recipes should be added only after small-area visual acceptance and should not make the beginner GUI harder to operate.

### Advanced raster compatibility

**Status:** potential

Current converter baseline is raster PNG/JPEG MBTiles. Additional raster variations may be considered only with controlled fixtures and ArcGIS Earth acceptance. Vector/PBF support is not a v1.0 goal.

## v1.1 reliability / fortification candidates

The v1.0 Factory already has strong output-integrity, cancellation, cleanup, duplicate-instance, temporary-workspace, verification, and subprocess protections. Any additional hardening should remain **bounded and visible** rather than turning a successful batch Factory into a self-restarting supervisor system.

### One controlled QGIS manufacturing retry

**Status:** candidate

If the QGIS manufacturing subprocess fails **before conversion begins**, allow at most **one automatic retry** after cleaning the failed temporary manufacturing state.

Requirements:

- visibly report `RETRY 1/1` to the operator;
- create a fresh disposable QGIS/work directory for the retry;
- never retry forever;
- never hide the original failure in the log;
- never overwrite an existing accepted output;
- if the retry fails, stop cleanly and report the failure.

Do **not** automatically retry the TPKX converter after an ambiguous conversion/disk failure. Converter failure should remain a clean stop until there is evidence that a particular failure mode is safe to retry.

### Large-build free-space preflight

**Status:** candidate

Before starting a large build, perform a conservative free-space sanity check for the selected work/output volumes. The exact estimator can remain intentionally simple; its job is to catch obviously impossible jobs before hours of QGIS rendering begin, not to promise an exact final byte count.

### Explicit stage/status preservation

**Status:** candidate

Keep operator-visible stage reporting unambiguous across long jobs and any future retry path:

```text
QGIS manufacturing
MBTiles verification
TPKX conversion
TPKX verification
Publishing
Complete
```

A retry or recovery action must say exactly which stage is being repeated. Avoid silent restarts.

## Mobile / nearby-depot experiments

### ArcGIS Earth Mobile exact-TPKX acceptance

**Status:** bench test pending

Install ArcGIS Earth Mobile on Android and test an **exact Factory-produced TPKX** completely offline before making a public compatibility claim. Start with a small known-good package, then test a substantial production package only after the small gate passes.

### Wi-Fi Map Fountain

**Status:** experimental architecture candidate

Investigate a deliberately simple nearby map appliance:

```text
Raspberry Pi + SSD
        ↓
local Wi-Fi access point
        ↓
on-demand raster tile service
        ↓
ArcGIS Earth Mobile
```

Goal: the Pi/SSD remains the mother map depot while Android consumes map tiles **in real time over local Wi-Fi**, without downloading the complete mother TPKX to the device and without Internet connectivity.

The Pi should remain a dumb map-serving appliance, not become a GIS workstation. Prefer a standards-based tile interface supported by ArcGIS Earth Mobile, with the existing TPKX/Compact Cache V2 knowledge used only as needed to retrieve the requested raster tiles efficiently.

Bench questions to answer before productizing:

- Can ArcGIS Earth Mobile consume the local service reliably while completely offline from the Internet?
- Can the service expose multiple mother maps cleanly?
- What latency/throughput is acceptable while panning and zooming?
- What previously viewed tiles, if any, remain visible after the Android leaves Wi-Fi range?
- Does any retained cache survive an ArcGIS Earth Mobile restart?

Do not treat incidental client caching as an offline guarantee until live testing establishes its actual behavior.

## Deployment polish

### ArcGIS Earth workspace profile

**Status:** partially explored

Investigate a deliberate field workspace using startup layers, local packages, custom icons, autosave, and other administrator-supported controls. Freeze only after cold-start and offline acceptance.

### ArcGIS Field Maps crossover

**Status:** not yet live-proven

Test an exact Factory-produced TPKX on the intended Android/iOS Field Maps workflow before making a public compatibility claim.

## Public documentation / community

- Publish the exact accepted v1.0 ZIP through a direct GitHub binary upload.
- Publish a clean-machine start-to-finish map-manufacturing demonstration.
- Present the MBTiles → TPKX bridge to GIS/QGIS/ArcGIS Earth technical audiences.
- Keep legacy Google Earth material available as lineage, not as the current baseline.

## Non-goals

- Rebuilding QGIS inside the Factory
- Rebuilding ArcGIS Earth
- Turning the baseline into a multi-user map server
- Making cloud connectivity mandatory
- Hiding evidence status behind marketing language
- Rewriting proven components merely because a cleaner implementation seems possible
- Adding unbounded restart loops or invisible automatic recovery behavior

## Governing rule

> **New capability must earn its way into the baseline by answering to the same live target that accepted the old capability.**
