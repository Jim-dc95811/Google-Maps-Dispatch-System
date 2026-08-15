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


Figure 6. Large normal v0.1.6 Factory run completion: 271,242 tiles, Z8-Z18, 24,291,406 KB, elapsed 2:51:52.


Figure 7. Large normal Factory output loaded with neighboring TPKX packages in ArcGIS Earth.


Figure 8. Exact v1.0.0 smoke-test output “test2 small” rendered in ArcGIS Earth. This closed the release gate.

## 17. ArcGIS Earth as the Runtime

ArcGIS Earth is not merely a visualization endpoint for this project; it is the operational runtime around which the offline system is now organized. Esri documents ArcGIS Earth as a lightweight 3D application for geospatial data, supports tile packages as local/startup content, provides a RESTful Automation API, and supports real-time NMEA GNSS [R4-R7].

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

## 18. Offline Operational Doctrine and Persistent Geographic Context

| HARD REQUIREMENT<br>There can be no operational dependence on Internet connectivity. At showtime, loss of Internet must not prevent core map viewing, position context, or other essential command functions. Internet services are optional enhancements. |

| --- |


The deployment philosophy is to perform Internet-dependent preparation before the operational event. The map package is manufactured ahead of time and carried to the field. A cellular hotspot, LTE modem, VPN, carrier account, signal coverage, login, or cloud endpoint must not become a prerequisite for seeing the command map.

### 18.1 Persistent Geographic Context

The project adopted the phrase “Persistent Geographic Context” for the operating condition in which position, surroundings, routes, and terrain remain continuously visible without requiring the operator to summon the information. With AE already open, offline TPKX imagery loaded, and a GNSS source centering the view, the map becomes a continuously present spatial instrument rather than a sequence of user queries.

This distinction is especially important for large-area situational awareness : an operator can see not only “I am at X” but “I am on this road, in this forest, relative to this drainage, clearing, access route, structure cluster, and surrounding terrain.” The same model has non-emergency applications such as delivery, utility, forestry, rural real estate, property inspection, and other work in which the user benefits from seeing what lies ahead before entering an area with uncertain cellular coverage.

## 19. PRAVE / Live Position Integration through the Automation API

The ArcGIS Earth transition also modernized the project’s live remote-unit display. The proven PRAVE decoder parses a mixed Raveon serial stream containing local RMC and asynchronous $PRAVE messages. Rather than forcing PRAVE through KML, the new path sends native drawing operations to the ArcGIS Earth Automation API. Esri documents the default Automation API endpoint hierarchy under localhost:8000 and exposes drawing, graphic, layer, camera, flight, workspace, and snapshot operations [R5].


Figure 9. Live PRAVE Automation API acceptance in ArcGIS Earth: units 7-101 through 7-106 rendered as native labeled drawings with fire-truck RSSI icons.


Figure 10. PRAVE live bridge console during the accepted API test. Status counters included UNITS, API_OK, API_BAD, BAD_RMC, BAD_PRAVE, and RMC freshness.

### 19.1 Canonical identity and RSSI rules

|E