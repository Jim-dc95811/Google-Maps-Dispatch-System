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

## 2026-08-17 router-only Map Fountain breakthrough

**Status: ✅ LIVE-PROVEN**

Proven chain:

```text
native TPKX on USB SSD
→ GL.iNet Flint 2
→ Samba / SMB
→ Wi-Fi
→ Windows
→ ArcGIS Earth
```

The production-scale `ESG1N.tpkx` package was benchmarked through the router over both Ethernet and Wi-Fi, then opened directly from the Samba share and rendered interactively in ArcGIS Earth over Wi-Fi.

The field delivery architecture is now **router only**. The router provides storage/network/file sharing; ArcGIS Earth provides the GIS intelligence.

### Next Map Fountain gates

1. Repeat the successful ArcGIS Earth application test over Ethernet for direct comparison.
2. Characterize real ArcGIS Earth deliberate pan/zoom behavior over Wi-Fi.
3. Test cold close/reopen and Wi-Fi reconnect behavior.
4. Test multiple simultaneous Eaters.
5. Test the simplest router-only ArcGIS Earth Mobile path separately.
6. Build the basecamp Feeder only after consumption behavior is stable.

Do not add a field GIS-server layer unless real target evidence proves one is necessary.

## Historical mobile breakthrough — 2026-08-16

### ArcGIS Earth Mobile local TPKX

**Status: ✅ LIVE-PROVEN on multiple packages**

Observed successful local packages include a Rasta Thames Bridge TPKX plus smaller Esri and Google Hybrid packages.

One larger Google Hybrid package returned `spatial reference not supported`. Keep that as a package-level compatibility question rather than a blanket mobile limitation.

### Windows-hosted local WMTS proof

**Status: ✅ LIVE-PROVEN HISTORY**

Historical proven chain:

```text
MBTiles on Windows PC / SSD
→ local HTTPS WMTS
→ Android USB tether
→ ArcGIS Earth Mobile
```

That work proved local mobile tile delivery, operation with outside Internet removed, HTTPS, QR loading, multiple substantial MBTiles, and a large Lago panorama.

It remains a useful compatibility technique, but it is **not** the current field-appliance architecture.

## Map-production expansion

### Later TPKX Map Factory output-choice branch

Normal operator choices:

```text
TPKX
MBTiles
Both
```

Behavior:

- **TPKX** — manufacture MBTiles, run the frozen proven converter, publish TPKX.
- **MBTiles** — manufacture and verify MBTiles, publish directly.
- **Both** — preserve the QGIS-built MBTiles and create TPKX from the same pyramid.

The accepted v1.0.0 baseline stays separate and unchanged.

### TPKX → MBTiles recovery

**Status: ❌ REJECTED AS PRODUCTION PATH**

A reverse Compact Cache V2 recovery experiment worked on a controlled fixture but a recovered production map later showed blurred/missing regions on ArcGIS Earth Mobile.

Decision:

- do not use recovery as the production shortcut;
- rebuild important MBTiles directly from QGIS;
- preserve MBTiles at manufacture time when they may be needed later.

### More QGIS recipes

**Status: open for later TEST branches**

The four-source v1.0 menu stays frozen. Add sources only after small-area visual acceptance and without burdening the beginner workflow.

## Reliability / fortification candidates

### One controlled QGIS manufacturing retry

Allow at most one visible retry only for a clearly failed QGIS manufacturing stage before conversion begins. No infinite loops or hidden restarts.

### Large-build free-space preflight

Perform a conservative free-space sanity check for work/output volumes before hours-long builds.

### Explicit stage/status preservation

Long operations must say what is actually happening. Do not show `COMPLETE` while verification/publishing is still running.

Suggested stages:

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

QR remains a bounded dispatch/data-input method and was also live-proven for historical mobile service loading.

## Public documentation / community

- attach the exact accepted `TPKX_MAP_FACTORY_v1_0_0.zip` as the public v1.0 binary;
- keep the router-only architecture drawing at the top of all three active repositories;
- publish the 2026-08-17 Map Fountain benchmark and ArcGIS Earth Wi-Fi acceptance evidence;
- document the exact prior-art search boundary without making unsupported worldwide-first claims;
- finish live acceptance of later Factory output modes before promoting them;
- publish a clean field demonstration of Factory → SSD → router → ArcGIS Earth;
- retain Google Earth / KML work as lineage, not current baseline.

## Non-goals

- rebuilding QGIS inside the Factory;
- rebuilding ArcGIS Earth;
- making public Internet connectivity mandatory;
- turning the consumer router into a GIS computer;
- requiring a field GIS-server process for the proven desktop TPKX path;
- marketing unmeasured multi-client behavior as supported;
- hiding evidence status behind marketing language;
- rewriting proven components without a verified defect;
- using rejected TPKX recovery as a shortcut;
- adding unbounded restart loops or invisible automatic recovery.

## Governing rule

> **New capability must earn its way into the baseline by answering to the real target.**

For field map delivery:

> **Keep the router dumb. Keep the maps native. Let ArcGIS Earth do the GIS work.**
