# Offline GeoStack Roadmap

The release-accepted **TPKX Map Factory v1.0.0** remains frozen. New capability is developed in later TEST branches and promoted only after live target acceptance.

## Frozen v1.0 baseline

- ✅ TPKX Map Factory v1.0.0 release accepted
- ✅ QGIS 3.44.9 raster manufacturing
- ✅ custom MBTiles → Compact Cache V2 / TPKX bridge
- ✅ advanced existing-MBTiles conversion
- ✅ ArcGIS Earth Windows native TPKX runtime
- ✅ PRAVE → ArcGIS Earth Automation API proof
- ✅ no operational Internet dependency for core map display

## 2026-08-16 mobile breakthrough

### ArcGIS Earth Mobile local TPKX

**Status: ✅ LIVE-PROVEN on multiple packages**

Observed successful local-file packages include a Rasta Thames Bridge TPKX plus smaller Esri and Google Hybrid TPKX files copied into Android storage and opened through ArcGIS Earth Mobile.

One larger Google Hybrid package returned `spatial reference not supported`. Because other TPKX packages loaded successfully, keep this as a package-level compatibility question rather than a blanket mobile limitation.

### USB Map Fountain

**Status: ✅ LIVE-PROVEN — v0.2.1 TEST**

Live-proven chain:

```text
MBTiles on Windows PC / SSD
        ↓
local HTTPS WMTS
        ↓
Android USB tether / Remote NDIS
        ↓
ArcGIS Earth Mobile
```

Proven behavior:

- phone reaches Windows PC over USB tether;
- ArcGIS Earth Mobile consumes WMTS tiles from the PC;
- service works with outside Internet removed;
- HTTPS works;
- QR service loading works;
- GUI can select different MBTiles from the PC / SSD;
- unique service IDs prevent stale-map cache reuse;
- three different substantial MBTiles have displayed successfully;
- large Lago panorama displayed smoothly on mobile.

Live operator envelope:

> **Deliberate pan/zoom is reliable. Rapid repeated zooming or whipping the view around can outrun the current delivery/render path.**

Near-term Map Fountain work:

1. generalize HTTPS certificate/IP lifecycle beyond the current test address;
2. controlled cold-restart / reconnect test;
3. repeat with additional large production map libraries;
4. measure throughput and latency on practical field hardware;
5. decide whether the appliance transport should be USB, Wi-Fi, or both;
6. preserve the single-user/private-depot positioning unless multi-user behavior is deliberately accepted.

### Wi-Fi / vehicle appliance follow-on

**Status: architecture candidate informed by live USB proof**

The earlier concept remains useful, but it is no longer hypothetical at the application layer. WMTS → ArcGIS Earth Mobile is proven. The remaining Wi-Fi/Pi question is transport/appliance packaging.

Candidate:

```text
Pi / Windows map depot + SSD
        ↓
private local Wi-Fi or USB link
        ↓
HTTPS WMTS
        ↓
ArcGIS Earth Mobile
```

Do not add appliance complexity until the software and operator workflow are stable.

## Map-production expansion

### TPKX Map Factory v1.2.0 TEST — output choice

**Status: 🟡 BUILT / SELF-TESTED; Windows live acceptance underway — 2026-08-16**

The Map Fountain proof changed MBTiles from disposable manufacturing material into a useful deployment product.

Normal operator choices in v1.2 TEST:

```text
TPKX
MBTiles
Both
```

Behavior:

- **TPKX** — manufacture MBTiles, run the frozen proven converter, publish TPKX.
- **MBTiles** — manufacture and verify MBTiles, publish it directly, skip TPKX conversion.
- **Both** — preserve the QGIS-built MBTiles and create TPKX from the exact same tile pyramid.
- **Both is the current TEST default.**

Advanced **MBTiles → TPKX** remains available.

The accepted v1.0.0 baseline stays separate and unchanged.

### TPKX → MBTiles recovery

**Status: ❌ REJECTED AS PRODUCTION PATH**

A reverse Compact Cache V2 recovery experiment could recover exact raster tile bytes from a controlled fixture. A recovered production map later showed blurred/missing regions on ArcGIS Earth Mobile.

Decision:

- remove the recovery tool from v1.2;
- rebuild important MBTiles directly from QGIS instead;
- preserve MBTiles going forward when Map Fountain deployment may be needed.

### More QGIS recipes

**Status: open for v1.2+**

The four-source v1.0 menu stays frozen. Add sources only after small-area visual acceptance and without burdening the beginner workflow.

### Advanced raster compatibility

**Status: potential**

Current converter baseline remains raster PNG/JPEG MBTiles. Additional raster variations require controlled fixtures and target-viewer acceptance. Vector/PBF support is not a current goal.

## Reliability / fortification candidates

### One controlled QGIS manufacturing retry

**Status: candidate**

Allow at most one visible retry only for a clearly failed QGIS manufacturing stage before conversion begins. No infinite loops; no hidden restarts.

### Large-build free-space preflight

**Status: candidate**

Perform a conservative free-space sanity check for work/output volumes before hours-long builds.

### Explicit stage/status preservation

**Status: required principle**

Long operations must tell the operator what is actually happening. Do not show `FINISHED`, a full green bar, or `COMPLETE` while final verification/publishing is still running.

Suggested stage vocabulary:

```text
QGIS manufacturing
MBTiles verification
TPKX conversion
TPKX verification
Publishing MBTiles
Publishing TPKX
Complete
```

## Field integration

### Native GNSS

**Status: ✅ LIVE-OBSERVED — 2026-08-15**

Actual field receiver drove ArcGIS Earth native realtime blue-dot location on Windows. Known-good observed input: **9600 baud**, GLL + RMC present.

### F22 → common live-position manager

**Status: designed**

Normalize F22 at the protocol edge and feed the same ArcGIS Earth live-position abstraction used by other remote-unit inputs.

### QR → ArcGIS Earth

**Status: active interoperability path**

QR is now live-proven for Map Fountain service loading on ArcGIS Earth Mobile. Dispatch/command QR remains a separate bounded-command modernization candidate.

## Public documentation / community

- attach the exact accepted `TPKX_MAP_FACTORY_v1_0_0.zip` as the public v1.0 binary;
- finish live acceptance of v1.2 output modes before promoting it;
- publish a clean desktop + mobile demonstration showing both TPKX and Map Fountain paths;
- document the USB Map Fountain operator workflow and practical navigation envelope;
- present the MBTiles → TPKX bridge and local mobile serving path to GIS/QGIS/ArcGIS Earth audiences;
- retain Google Earth / KML work as lineage, not current baseline.

## Non-goals

- rebuilding QGIS inside the Factory;
- rebuilding ArcGIS Earth;
- making public Internet connectivity mandatory;
- marketing incidental multi-client behavior as a supported multi-user product;
- hiding evidence status behind marketing language;
- rewriting proven components without a verified defect;
- using TPKX recovery as a shortcut after it failed the live mobile visual gate;
- adding unbounded restart loops or invisible automatic recovery.

## Governing rule

> **New capability must earn its way into the baseline by answering to the real target.**
