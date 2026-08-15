# Professional GIS Report — Part 3

## 15. Release Evolution and Engineering Decisions

| Version / milestone | Key change / acceptance |
| --- | --- |
| Standalone converter v0.1.0 | Custom raster MBTiles -> Compact Cache V2 TPKX implemented and bench validated; later accepted live by AE. |
| Factory v0.1.0 TEST | First integrated QGIS -> temporary MBTiles -> TPKX chain; Hybrid 113.31 sq mi, 23,119 tiles, Z8-Z18, 3,560,735 KB, 0:13:55; AE PASS. |
| v0.1.1 TEST | 96 DPI; final four source choices; Esri/Google Labels donor-project support; UI simplification. |
| v0.1.2 TEST | Neighbor tool removed; “Choose map area”; manual GPS points; direct HOME EXTENT order cue; Grid ID removed; no filename suggestion. |
| v0.1.3 TEST | SHA/fingerprint gate removed. Small Esri/Google Labels Z8-Z20 acceptance: 7,206 tiles, 813,147 KB, 0:04:45. |
| v0.1.4 TEST | TEMP/destination hygiene fixed; disposable read-only QGZ cleanup corrected; large production-style runs. |
| v0.1.5 TEST | Advanced existing-MBTiles conversion added, but converter control fell below the visible screen on live Windows scaling. |
| v0.1.6 TEST | Advanced control moved to always-visible bottom command bar. Advanced 271,497-tile conversion PASS; normal 271,242-tile large build PASS. |
| v1.0.0 | Feature freeze from v0.1.6 mechanics; color icons + heartbeat/progress polish; exact release ZIP smoke-tested and accepted 15 Aug 2026. |

A key release discipline is that v1.0.0 is not a rewrite. It is a release pass around live-proven v0.1.6 mechanics. New capabilities after release acceptance should become v1.1 or later rather than destabilizing the v1.0 baseline.

## 16. Live Acceptance and Performance Evidence

| Test | Path | Result |
| --- | --- | --- |
| First integrated Factory acceptance | Google Hybrid; 113.31 sq mi; Z8-Z18; 23,119 tiles; 3,560,735 KB; 0:13:55 | AE rendered sharply; end-to-end architecture accepted. |
| Small high-zoom blend | Esri World / Google Labels; 2.17 sq mi; Z8-Z20; 7,206 tiles; 813,147 KB; 0:04:45 | AE visual acceptance at close operating scale. |
| Advanced converter stress | Existing raster MBTiles; 271,497 tiles; Z8-Z18; 47 bundles; 25,561,426 KB; 0:17:59 | TPKX opened/rendered in AE. Advanced path LIVE-PROVEN. |
| Large normal Factory run | Esri World / Google Labels; 1,378.89 sq mi; 271,242 tiles; Z8-Z18; 24,291,406 KB; 2:51:52 | Factory completed; AE opened/rendered. v0.1.6 mechanics LIVE-PROVEN. |
| Exact v1.0 smoke test | Google Hybrid; manual GPS extent; approx. 0.12 sq mi; Z0-Z18; 65 populated tiles; 12,852 KB; 0:00:12 | Exact release package launched, built, completed, and rendered in AE. RELEASE-ACCEPTED. |

The large normal v0.1.6 Factory run completed 271,242 tiles, Z8-Z18, 24,291,406 KB, elapsed 2:51:52. The resulting package loaded with neighboring TPKX packages in ArcGIS Earth. The exact v1.0.0 smoke-test output `test2 small` rendered in ArcGIS Earth and closed the release gate.

## 17. ArcGIS Earth as the Runtime

ArcGIS Earth is not merely a visualization endpoint for this project; it is the operational runtime around which the offline system is now organized. Esri documents ArcGIS Earth as a lightweight 3D application for geospatial data, supports tile packages as local/startup content, provides a RESTful Automation API, and supports real-time NMEA GNSS.

### 17.1 Live-observed behaviors relevant to deployment

- Native TPKX packages open directly and pan/zoom smoothly.
- Multiple TPKX packages can be loaded simultaneously in My Data.
- AE restores/repopulates loaded TPKX content after close/reopen in the tested workspace behavior.
- Point-to-point driving directions remain available when online; this is an enhancement, not an operational dependency.
- The Data tree provides operator-visible layer on/off control and organization.
- ArcGIS Earth accepted native Automation API drawings for the project’s live PRAVE units.
- The viewer can operate with local package data when Internet connectivity is absent.

### 17.2 Why native TPKX changes the architecture

In the prior Google Earth path, an offline raster basemap might require a KML hierarchy, local HTTP service, PNG tile lookup, and viewer-specific region/LOD behavior. Native TPKX collapses that runtime chain. The raster pyramid is already packaged in a format AE knows how to index. The operational computer no longer needs a local tile server merely to make the basemap visible.

## 18. Offline Operational Doctrine and Persistent Geographic Awareness

> **HARD REQUIREMENT**  
> There can be no operational dependence on Internet connectivity. At showtime, loss of Internet must not prevent core map viewing, position awareness, or other essential command functions. Internet services are optional enhancements.

The deployment philosophy is to perform Internet-dependent preparation before the operational event. The map package is manufactured ahead of time and carried to the field. A cellular hotspot, LTE modem, VPN, carrier account, signal coverage, login, or cloud endpoint must not become a prerequisite for seeing the command map.

### 18.1 Persistent Geographic Awareness

The project adopted the phrase **Persistent Geographic Awareness** for the operating condition in which position, surroundings, routes, and terrain remain continuously visible without requiring the operator to summon the information. With AE already open, offline TPKX imagery loaded, and a GNSS source centering the view, the map becomes a continuously present spatial instrument rather than a sequence of user queries.

This distinction is especially important for large-area situational awareness: an operator can see not only “I am at X” but “I am on this road, in this forest, relative to this drainage, clearing, access route, structure cluster, and surrounding terrain.” The same model has non-emergency applications such as delivery, utility, forestry, rural real estate, property inspection, and other work in which the user benefits from seeing what lies ahead before entering an area with uncertain cellular coverage.

## 19. PRAVE / Live Position Integration through the Automation API

The ArcGIS Earth transition also modernized the project’s live remote-unit display. The proven PRAVE decoder parses a mixed Raveon serial stream containing local RMC and asynchronous `$PRAVE` messages. Rather than forcing PRAVE through KML, the new path sends native drawing operations to the ArcGIS Earth Automation API. Esri documents the default Automation API endpoint hierarchy under `localhost:8000` and exposes drawing, graphic, layer, camera, flight, workspace, and snapshot operations.

Live PRAVE Automation API acceptance in ArcGIS Earth showed units `7-101` through `7-106` rendered as native labeled drawings with fire-truck RSSI icons. The PRAVE live bridge console reported status counters including `UNITS`, `API_OK`, `API_BAD`, `BAD_RMC`, `BAD_PRAVE`, and RMC freshness.

### 19.1 Canonical identity and RSSI rules

| Element | Rule |
| --- | --- |
| Display ID | field[8] + field[13] (individual padded to three digits); e.g. district 7 + individual 004 -> 7-004 |
| Unknown RSSI | blank/invalid -> icon level 0 |
| 1 bar | < -110 dBm |
| 2 bars | -110 to -101 dBm |
| 3 bars | -100 to -91 dBm |
| 4 bars | -90 to -81 dBm |
| 5 bars | >= -80 dBm |

The live API acceptance established that the six tester units 7-101 through 7-106 appeared with labels and the expected icon states, while the bridge console reported successful API activity and fresh RMC input. This function is therefore LIVE-PROVEN and is no longer merely a proposed AE migration path.

## 20. GNSS, F22, QR, KML, and Other Integration Paths

### 20.1 Native GNSS / NMEA

Esri documents direct connection of NMEA-capable GNSS devices to ArcGIS Earth, including current-location display, observations, track recording, raw NMEA recording, and historical NMEA review. The preferred architecture is to use AE native GNSS for “ME” / own position if the actual field receiver and COM-port behavior prove satisfactory. This path still requires field acceptance with the actual receiver architecture.

### 20.2 F22

F22 should become another input into the same native live-position abstraction rather than a separate renderer. Decode protocol-specific text at the edge, normalize unit ID/latitude/longitude/metadata, then send to one AE live-position manager. The earlier PRAVE-to-F22 mapping experiments remain useful history but are not the preferred modern rendering chain.

### 20.3 QR / dispatch

The QR workflow remains valuable as an optical/physical command and destination handoff. The modern target is QR decode -> bounded command or coordinate payload -> Automation API marker/camera/layer action. QR is intentionally separate from PRAVE/F22 transport. Destructive commands should require explicit confirmation and unknown commands should be rejected.

### 20.4 KML/KMZ/NetworkLinks

KML is retained. AE supports KML/KMZ and KML remains a good interoperability contract for placemarks, folders, NetworkLinks, external feeds, migration, and saved content. The architectural change is simply that KML is no longer required to impersonate a native raster-tile package or to carry every live-update function.

## 21. Deployment Model and Security Boundaries

### 21.1 Baseline field machine

- Windows 11.
- ArcGIS Earth installed and validated.
- QGIS 3.44.9 and Python 3.14.5 available on the map-manufacturing machine.
- Required read-only QGZ reference projects at the documented path.
- TPKX map depot on suitable local/external storage.
- Selected TPKX package(s) already loaded or easy to load.
- GNSS configured if used.
- PRAVE/F22/QR tools packaged as user-facing Windows launchers as those paths mature.
- Internet availability treated as optional.

### 21.2 Automation API boundary

The baseline Automation API should remain localhost-only. Esri documents the default local endpoint at `http://localhost:8000`. The project has no baseline requirement to expose control endpoints across a LAN. Any future remote exposure should be treated as a separate security design decision.

### 21.3 Workspace/startup configuration

Esri’s administrator configuration supports local workspaces, autosave, startup layers including tile packages, custom icons, organizational basemaps, and other controls. These features are candidates for making AE behave more like a preconfigured field appliance. Live operator observation already confirmed useful session persistence of loaded TPKX packages.

## 22. AI-Assisted Engineering Methodology

This project is a concrete example of AI reducing the coordination cost of a cross-domain GIS integration problem. The converter was not difficult because of one exotic algorithm; it was difficult because successful implementation required simultaneously understanding MBTiles/SQLite, TMS/XYZ conventions, Web Mercator tile math, Esri Compact Cache V2 binary layout, TPKX metadata, ZIP packaging, QGIS processing, Windows process control, and the acceptance behavior of ArcGIS Earth.

### 22.1 Division of labor

| Human / AI role | Primary responsibility |
| --- | --- |
| Human project architect / live-test authority | Operational requirements, field constraints, product simplicity, screenshots/telemetry, real Windows execution, visual acceptance, feature decisions, final go/no-go. |
| AI engineering contractor | Research official specifications, synthesize cross-domain architecture, write/modify Python and Windows launchers, analyze failures, construct converter/package mechanics, produce technical documentation, preserve continuity. |
| QGIS | Render cartography and produce the raster tile pyramid. |
| ArcGIS Earth | Act as the final runtime acceptance authority for TPKX and live display behavior. |

### 22.2 Why AI was effective here

A conventional team might distribute these specialties among GIS, Python, binary-format, Windows, and application-integration personnel. AI reduced handoff latency by holding the interacting specifications and code paths in one reasoning context. The final converter is compact, but discovering and validating the correct arrangement of bytes, metadata, row conventions, bundle offsets, and process boundaries is the high-value work.

### 22.3 Critical test discipline

The project did not accept “the code looks right” as proof. Every important stage was driven to a live target: QGIS had to produce a valid MBTiles; the converter had to generate a structurally valid TPKX; and ArcGIS Earth had to open, locate, and render it correctly. Screenshots were treated as telemetry. For live setup/troubleshooting, one action was issued at a time and the next instruction waited for the resulting screen state.

## 23. Known Limitations and Non-Goals

- Converter v0.1.0 supports raster PNG/JPEG MBTiles; it does not convert PBF/vector-tile MBTiles.
- The normal Factory is designed around Web Mercator raster tile pyramids and approved QGIS projects.
- The Factory does not grant rights to imagery; source licensing/caching/export permissions remain source-specific.
- The product is not designed as a multi-user map server. Native TPKX is the preferred single-user/private offline basemap model.
- ArcGIS Earth native GNSS with the actual field hardware remains an acceptance item even though the feature is officially supported.
- Field Maps consumption of the exact independently manufactured TPKX was identified as a promising crossover but remains NOT LIVE-PROVEN unless separately confirmed.
- Legacy internal identifiers such as “Network Earth” metadata remain in `DIRECT_MBTILES_ENGINE.py` from its proven lineage. They are harmless but should be treated as lineage artifacts, not current product branding.
- The v1.0 release intentionally avoids automatic filename generation and lets the operator choose the output name.
- No hash-integrity gate is part of the release. Reference QGZ recovery is handled by read-only protection and archived originals.
