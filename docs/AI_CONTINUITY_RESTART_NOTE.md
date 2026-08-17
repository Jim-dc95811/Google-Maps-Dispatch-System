# OFFLINE GEOSTACK — AI CONTINUITY / RESTART NOTE

This repository is intended to be understandable by future human maintainers and future AI systems without silently reviving superseded architecture.

## Master identity

**Offline GeoStack — QGIS → MBTiles / TPKX → ArcGIS Earth Desktop + Mobile + Live Field Positioning**

The repository is named `Offline-GeoStack`. Older Google Maps Dispatch System names are lineage only.

## Current truth — 2026-08-17

The accepted desktop map baseline remains frozen:

```text
QGIS 3.44.9
→ raster MBTiles
→ custom MBTiles → TPKX converter
→ Esri Compact Cache V2 / .tpkx
→ ArcGIS Earth Windows
```

The current field delivery appliance is now **router only**:

```text
native TPKX on USB SSD
→ GL.iNet Flint 2
→ Samba / SMB
→ Ethernet or Wi-Fi
→ Windows
→ ArcGIS Earth
```

This router-only path is **LIVE-PROVEN**. ArcGIS Earth opened `ESG1N.tpkx` directly from the router-attached SSD over Wi-Fi and rendered/navigated it successfully.

Do not reintroduce a field GIS-server appliance from older design history unless a new real-target failure proves additional software is necessary.

ArcGIS Earth is abbreviated **AE** throughout project work.

## Evidence-status snapshot

- TPKX Map Factory v1.0.0: **RELEASE-ACCEPTED / LIVE-PROVEN**.
- MBTiles → TPKX frozen converter: **LIVE-PROVEN**.
- ArcGIS Earth Windows local TPKX: **LIVE-PROVEN**.
- Router-only Map Fountain: **LIVE-PROVEN**.
- Large TPKX Ethernet storage benchmark: **LIVE-PROVEN**.
- Large TPKX Wi-Fi storage benchmark: **LIVE-PROVEN**.
- ArcGIS Earth direct network-hosted TPKX over Wi-Fi: **LIVE-PROVEN**.
- ArcGIS Earth Mobile local TPKX: **LIVE-PROVEN on multiple packages**.
- Historical Windows-hosted HTTPS WMTS to Android: **LIVE-PROVEN HISTORY**.
- Native Windows AE GNSS with actual receiver: **LIVE-OBSERVED**, known-good 9600 baud with GLL + RMC present.
- PRAVE → AE Automation API: **LIVE-PROVEN**.
- Later TPKX Map Factory output-choice branch: **TEST branch; do not confuse with frozen v1.0.0**.
- TPKX → MBTiles recovery: **REJECTED as production path** after mobile visual defects in a recovered production map.

## Hard requirement

> There can be no operational dependence on Internet connectivity. Period.

This means outside/public Internet dependency. It does not prohibit private local networking.

The current router-only path satisfies the doctrine:

```text
local SSD
→ private router LAN
→ Samba
→ ArcGIS Earth
```

No public map service is required for the proven TPKX read path.

## Router-only Map Fountain milestone

Large specimen:

- `ESG1N.tpkx`
- 26,174,899,216 bytes by benchmark script
- 25,561,426 KB Windows File Explorer identification

Ethernet baseline:

- random 25.33 MiB/s
- random p95 9.98 ms
- four-client aggregate 51.21 MiB/s
- sequential 42.58 MiB/s

Wi-Fi baseline:

- random 5.19 MiB/s
- random p95 50.56 ms
- four-client aggregate 5.31 MiB/s
- sequential 6.14 MiB/s

The real acceptance event came afterward: AE opened the same network-hosted TPKX over Wi-Fi and rendered the Jacksonville map.

## Current desktop/mobile map architecture

The MBTiles stage remains a useful manufacturing branch point:

```text
QGIS
→ verified raster MBTiles
    ├─→ preserve MBTiles
    └─→ frozen converter → TPKX
```

Field delivery then uses the simplest target-compatible form:

```text
TPKX on router-attached SSD
→ Samba
→ ArcGIS Earth Windows
```

For mobile, compatible local TPKX is already proven. Additional router-only mobile delivery remains a separate acceptance gate.

## Historical Windows Map Fountain lesson

On 2026-08-16, a Windows-hosted HTTPS WMTS implementation proved local mobile raster delivery over Android USB tether.

That branch taught important lessons about:

- local mobile networking;
- HTTPS acceptance;
- QR service loading;
- per-map service identity and cache isolation;
- deliberate versus rapid navigation;
- operation with outside Internet removed.

Keep those lessons. Do not confuse that historical software path with the current router-only field appliance.

## TPKX recovery lesson

A reverse Compact Cache V2 recovery experiment could reproduce exact tile bytes in a controlled fixture. That did **not** establish production suitability.

A recovered production MBTiles later showed blurred/missing regions on ArcGIS Earth Mobile.

Decision:

- recovery is not the production path;
- rebuild important MBTiles directly from QGIS;
- preserve MBTiles at manufacture time when needed;
- target-viewer acceptance outranks internal byte-level cleverness.

## Acceptance authority

For TPKX, the intended ArcGIS Earth runtime is the operational authority.

For the router-only path, acceptance requires:

- the share is stable;
- the intended native file opens from the router-attached SSD;
- AE renders the correct map;
- useful navigation works;
- the path remains local/offline.

## Do not regress

- Do not return Google Earth Pro to primary-viewer status by inertia.
- Do not present KML Super Overlay / Blooming Onion as the current basemap architecture.
- Do not casually rewrite the frozen MBTiles→TPKX converter.
- Do not revive TPKX→MBTiles recovery as a production shortcut without solving and live-proving the defect.
- Do not add a field GIS server to the proven router-only TPKX path without evidence that one is required.
- Do not make public Internet mandatory.
- Do not make normal consumers use manual static IP configuration.
- Keep advanced GIS freedom through existing-MBTiles → TPKX.
- Retain KML for interoperability, NetworkLinks, external feeds, and saved content.
- Do not turn incidental multi-client capability into a supported multi-user product claim until measured.
- Do not show `FINISHED`, a full progress bar, or `COMPLETE` before final verification/publishing is actually done.
- Do not confuse Windows cache/read-ahead throughput with raw network speed.

## Current known-good environment

- Windows 10/11 64-bit
- Python 3.14.5
- QGIS 3.44.9
- ArcGIS Earth Windows
- ArcGIS Earth Mobile Android
- GL.iNet Flint 2 GL-MT6000 for router-only Map Fountain proof
- Factory raster recipe: PNG, 96 DPI, antialiasing ON, metatile 4, Z0–Z20

No additional Python libraries are required by the frozen TPKX converter path.

## Proven paths

1. Frozen normal Factory: source → area → zoom → QGIS → MBTiles → TPKX → AE Windows.
2. Advanced Factory: existing raster MBTiles → TPKX → AE Windows.
3. Router-only Map Fountain: USB SSD → Flint 2 → Samba → Wi-Fi → AE Windows → native TPKX.
4. Local Android file: compatible TPKX → ArcGIS Earth Mobile.
5. Historical mobile WMTS: MBTiles → HTTPS WMTS → USB tether → ArcGIS Earth Mobile.
6. PRAVE → ArcGIS Earth Automation API with native drawings / RSSI fire-truck icons.
7. Native AE GNSS own-position on Windows.

## Persistent Geographic Context

Current operational language uses **Persistent Geographic Context**: keeping position, surroundings, routes, and terrain continuously visible and available without relying on a public-network request at showtime.

## Historical archive rule

Legacy Google Earth, KML forest/Blooming Onion, Network Earth, and other superseded server experiments are technically valuable lineage. Preserve them as history. Do not treat old material as current merely because it exists.

## Binary-release truth

The exact accepted `TPKX_MAP_FACTORY_v1_0_0.zip` remains preserved in the canonical project archive. A connector-truncated GitHub copy was removed. Do not mistake a TEST branch, reconstructed archive, or partial upload for the release-accepted binary.

## Cold-start reading order

1. `README.md`
2. Map Fountain `README.md` and `docs/ACCEPTANCE_RECORD.md`
3. `ROADMAP.md`
4. `CHANGELOG.md`
5. `docs/TECHNICAL_ARCHITECTURE.md`
6. `docs/PRAVE_ARCGIS_EARTH_INTEGRATION.md`
7. `releases/README.md`
8. newest commits / issues

Report the current evidence status before changing behavior.

## Governing principle

> **Keep the router dumb. Keep the maps native. Let ArcGIS Earth do the GIS work.**
