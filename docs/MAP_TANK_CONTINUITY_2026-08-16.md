# Map Tank continuity checkpoint — 2026-08-16

## Umbrella identity

Current preferred umbrella wording:

**ArcGIS Earth Systems — Offline Field Mapping**

Public posture: install ArcGIS Earth on PC and Android, then show what can be built around it for serious offline field use.

## Three current branches

1. **Offline GeoStack** — ArcGIS Earth PC operational side, TPKX, native GNSS, PRAVE, QR/dispatch integration, no operational Internet dependency.
2. **Rasta Pyramid Factory** — QGIS/Python raster manufacturing from ordinary or georeferenced imagery to MBTiles, TPKX, or Both; gigapixel-class deep-zoom proofs are live.
3. **Map Fountain** — MBTiles delivery toward ArcGIS Earth Mobile; Windows v0.2.1 TEST is live-proven over local HTTPS WMTS.

## Approved main architecture picture

Jim's mockup-derived drawing is now the first major image on all three project READMEs. Preserve that drawing as the architecture authority for this phase.

It shows:
- Factory: Google / Esri / image files -> QGIS + Python -> MBTiles + TPKX.
- PC: GPS + SSD TPKX + PRAVE radio -> ArcGIS Earth PC.
- Android: ArcGIS Earth Mobile -> Wi-Fi -> server/storage path -> SSD MBTiles.

**ArcGIS Earth PC itself is the current terrestrial chart plotter.** OpenCPN belongs to lineage/history, not the current runtime architecture.

## Map Tank

Nickname coined by Jim:

> “Hey what's that router with an SSD plugged into it doing behind your seat? That's our map tank.”

Concept: **consumer Wi-Fi router + USB SSD = private offline map reservoir** that may serve multiple laptops / Android devices. The point is to make the field-storage/delivery appliance vastly simpler for normal users than a Raspberry Pi.

Do not call this an “old Wi-Fi router” concept; current routers offer USB storage.

## Test router ordered

**GL.iNet Flint 2 — GL-MT6000**

Ordered 2026-08-16; expected 2026-08-17.

Reasons selected:
- USB 3.0 storage
- Wi-Fi 6
- stock Samba + WebDAV network storage
- WebDAV supports HTTP/HTTPS choices in stock firmware
- normal consumer GUI; no Linux/SSH/Pi ceremony
- suitable for multiple clients

## Map Tank architecture candidates

### A. Laptop / PC direct TPKX — first bench test

SSD -> Flint 2 USB storage -> Wi-Fi -> Windows laptop -> ArcGIS Earth -> TPKX.

Esri documentation supports adding local data from a computer or shared drive. This has **not yet been live-proven on the Flint 2**. It is the first test because Wireshark can capture the entire exchange.

### B. Static WMTS directly from router

Factory -> `WMTSCapabilities.xml` + static PNG/JPEG tile tree -> SSD -> router HTTP/WebDAV -> ArcGIS Earth Mobile.

Potentially no Pi, no Python at showtime, no Android helper, and no remote SQLite. QGIS already has XYZ-directory generation capability. **Conceptual / not live-proven.** HTTP-vs-HTTPS acceptance remains a real gate because the current Map Fountain mobile bench needed HTTPS.

### C. Router storage -> Android tile-server bridge -> ArcGIS Earth Mobile

Keep MBTiles on SSD; Android reads the map and exposes a local WMTS to ArcGIS Earth. Existing Android tile servers prove much of this architecture. Main unresolved seam: efficient random SQLite/MBTiles reads across SMB/WebDAV without copying the whole file locally.

### D. PMTiles / byte-range fallback

MBTiles -> PMTiles repack -> router serves byte ranges -> thin Android bridge -> ArcGIS Earth. PMTiles is attractive because it is designed for range access and avoids remote SQLite. `MinotaurG/pmtiles-kotlin` is a new MIT-licensed dependency-free Kotlin reader found during research.

### E. Whole-file TPKX delivery

Router share -> Android/PC copies selected TPKX locally -> ArcGIS Earth. Simple fallback; not live streaming.

## Prior art found

- **Tech Maven Portable Tile Server for Android**: Android can serve raster MBTiles as XYZ / OGC WMTS and can serve another app on the same Android device.
- **bojko108/mobile-tile-server** (GPL-3.0): open-source Android Java MBTiles tile server. Core is essentially `Z/X/Y -> TMS Y flip -> SELECT tile_data -> return bytes`, nearly the same core as Map Fountain.
- **PMTiles**: single-file range-addressable tile archive; conversion from MBTiles exists; Kotlin/JVM reader above provides a useful code base.

## First test ladder when Flint 2 arrives

1. Power Flint 2.
2. Plug a known-good SSD into USB 3.0.
3. Use the normal router GUI; no SSH.
4. Leave laptop on DHCP.
5. Enable the simplest read-only storage share.
6. Connect the Windows laptop to Map Tank Wi-Fi.
7. Open a known-good TPKX directly from the router/shared SSD in ArcGIS Earth PC.
8. Capture the complete session in Wireshark.
9. Inspect open/read behavior, sequential vs random access, throughput, retries, caching, and ArcGIS Earth behavior.
10. If useful, build a Windows Python “Android consumption simulator” that can request GetCapabilities + real Z/X/Y tiles with steady-pan, hawk-dive, and abuse profiles while logging latency/success/bytes.
11. Only after the PC/simulator evidence, move to the real Android path.

## Network-address rule

Use **DHCP** for laptop and Android clients. Do not manually assign static client IPs. If a client temporarily acts as a server, prefer a router DHCP reservation over manual Windows static configuration.

## Drone note

Jim owns a **DJI Mavic 2 Zoom**. Do not automatically spawn a separate drone-mapping branch. Treat it simply as another source of pixels:

DJI capture -> existing QGIS/Rasta factory -> MBTiles / TPKX -> ArcGIS Earth.

Photogrammetry / orthomosaic / automated georeferencing only if explicitly reopened.

## Preserve current software status

- **TPKX Map Factory v1.0.0** — RELEASE-ACCEPTED / FROZEN; do not reconstruct/repack the exact accepted release.
- **TPKX Map Factory v1.2.0 TEST** — normal TPKX / MBTiles / Both output selector; TPKX->MBTiles recovery was removed after visual defects; direct-QGIS MBTiles is the production direction.
- **Map Fountain v0.2.1 TEST** — LIVE-PROVEN Windows -> local HTTPS WMTS -> Android / ArcGIS Earth Mobile; per-map service identity solved stale-cache reuse. Deliberate navigation is smooth; rapid repeated navigation can outrun the current path.
- Raspberry Pi is now only one possible delivery appliance; **Map Tank may make it unnecessary**.

## Restart sentence

> Open `docs/MAP_TANK_CONTINUITY_2026-08-16.md`. The GL.iNet Flint 2 GL-MT6000 is arriving 2026-08-17. Start with the laptop direct-TPKX-over-router test and Wireshark capture.
