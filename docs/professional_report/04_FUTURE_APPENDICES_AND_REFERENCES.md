# Offline GeoStack — Professional GIS Report, Part 4

## Future Extensions, Do-Not-Regress Rules, Canonical Settings, Status Matrix, and References

## 24. Future Extension Paths

| Candidate | Status | Recommended direction |
| --- | --- | --- |
| Additional QGIS cartographic recipes | Open for v1.1+ | Add only after controlled visual acceptance; preserve simple four-source v1.0 baseline. |
| Advanced converter support for more raster variations | Potential | Add only with specification/test fixtures; do not destabilize proven PNG/JPEG path. |
| Native GNSS field acceptance | Next operational test | Use actual receiver/COM settings; confirm centering/panning and serial exclusivity. |
| F22 -> AE manager | Designed | Normalize to common live-position structure; avoid separate renderer. |
| QR -> AE Automation API | Conceptual/modernization | Bounded allowlisted commands and destination markers. |
| AE workspace/startup automation | Partially available | Freeze a field profile only after cold-start/offline acceptance. |
| Field Maps TPKX crossover | Not yet live-proven | Test the exact Factory-made TPKX before any public compatibility claim. |
| Public release/tutorial | Ready after packaging/docs | Lead with simple map-making result; reveal advanced converter/GIS internals later. |

## 25. Do-Not-Regress Rules for Future Maintainers and AI Systems

> **PRIMARY RULE**  
> Do not confuse a newer idea with a proven replacement. Preserve live-proven components until the replacement has crossed the same acceptance gate.

1. Do not return to Google Earth Enterprise archaeology as the primary architecture. AE + native TPKX is the baseline.
2. Do not require a local HTTP/KML/PNG server merely to display the offline basemap in AE when native TPKX is available.
3. Do not make MBTiles the normal operator deliverable. It is a manufacturing intermediate; advanced users may choose it upstream.
4. Do not rewrite `MBTiles_to_TPKX_v0_1_0.py` casually. Integrate around it unless a verified defect requires a controlled change.
5. Do not reintroduce hash gates into the Factory without a new explicit requirement.
6. Do not modify the locked QGIS reference projects in place during production; use disposable copies.
7. Do not turn the beginner GUI into a general GIS control panel. Keep the normal workflow simple.
8. Do not remove the advanced MBTiles -> TPKX path; it is the direct bridge for professional QGIS users.
9. Do not claim an input/source is legally cacheable merely because the Factory can technically package it.
10. Do not expose the Automation API beyond localhost without a specific operational requirement and security review.
11. Do not alter proven PRAVE field indices, ID construction, or RSSI thresholds without evidence from real traffic.
12. Do not force F22 into a separate map renderer; normalize protocols into a common AE live-position layer.
13. Do not discard KML; keep it as an interoperability and external-feed mechanism.
14. Do not treat Internet availability as part of the operational core. Show-time essentials must function offline.
15. During live troubleshooting, use screen area -> visible landmark -> exact control -> one action, then wait for screenshot/telemetry.
16. When identifying large output files in acceptance records, preserve the exact Windows File Explorer size displayed to the operator rather than silently converting units.

## Appendix A. Canonical v1.0 Paths, Files, and Settings

| Item | Canonical value |
| --- | --- |
| Master project identity | Offline GeoStack |
| Factory release | `TPKX_MAP_FACTORY_v1_0_0.zip` |
| Launcher | `Start TPKX Map Factory.bat` |
| QGIS | 3.44.9 |
| Python | 3.14.5 |
| Primary QGZ | `C:\Google Earth Project\QGIS\REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz` |
| Blend QGZ | `C:\Google Earth Project\QGIS\ESRI and Google Labels.qgz` |
| PRAVE icons | `C:\MyData\PRAVE_ME\Icons` |
| AE Automation API default | `http://localhost:8000` |
| Render DPI | 96 |
| Tile format | PNG |
| Antialiasing | ON |
| Metatile | 4 |
| Public zoom range | Z0-Z20 |
| Default maximum | Z18 |
| Normal output | `.tpkx` only |
| Advanced input | Compatible raster `.mbtiles` |

## Appendix B. Converter Formula and Binary Reference

```text
TMS -> ArcGIS top-origin row:
  y = (1 << z) - 1 - tms_y

Bundle origin:
  b_row = (y // 128) * 128
  b_col = (x // 128) * 128

Bundle name:
  R{b_row:04x}C{b_col:04x}.bundle

Index slot:
  index_pos = (y % 128) * 128 + (x % 128)

Compact Cache V2 index value:
  IDX = tile_offset + (tile_size << 40)

Fixed bundle prefix:
  64-byte header + 16,384 x 8-byte index = 131,136 bytes
```

These formulas correspond to Esri’s published Compact Cache V2 description [R3] and the live-proven converter source.

## Appendix C. Exact v1.0 Smoke-Test Package Inspection

The exact TPKX uploaded from the live v1.0 smoke test was independently inspected as a ZIP package. It contained 22 members: `root.json`, `iteminfo.json`, `thumbnail.png`, and 19 Compact Cache V2 bundles covering L00 through L18. Parsing the 19 bundle indexes found 65 populated tile records. `root.json` identified `esriMapCacheStorageModeCompactV2`, 256 x 256 PNG tiles, 96 DPI, minLOD 0, maxLOD 18, packetSize 128, and EPSG:3857 spatial metadata. ArcGIS Earth rendered the package at the intended location.

| Observed field | Value |
| --- | --- |
| Output name | `test2 small.tpkx` |
| Windows File Explorer size | 12,852 KB |
| Elapsed | 0:00:12 |
| Package members | 22 |
| Bundle files | 19 |
| Populated tile records | 65 |
| Tile format | PNG |
| LOD range | 0-18 |
| Storage format | `esriMapCacheStorageModeCompactV2` |
| Packet size | 128 |
| Spatial reference | wkid 102100 / latestWkid 3857 |

## Appendix D. Engineering Status Matrix at v1.0 Release

| Subsystem | Status | Continuity note |
| --- | --- | --- |
| ArcGIS Earth native TPKX viewing | LIVE-PROVEN | Large and small packages accepted. |
| TPKX Map Factory v1.0.0 | RELEASE-ACCEPTED | Exact release ZIP passed live smoke test. |
| QGIS -> temporary MBTiles stage | LIVE-PROVEN | QGIS 3.44.9; PNG, 96 DPI, metatile 4. |
| `MBTiles_to_TPKX_v0_1_0` | LIVE-PROVEN / FROZEN | Preserves raster bytes; Compact Cache V2 writer. |
| Advanced MBTiles -> TPKX | LIVE-PROVEN | 271,497-tile stress conversion accepted by AE. |
| Esri World / Google Labels source | LIVE-PROVEN | Large 271,242-tile normal build accepted. |
| AE workspace resume of loaded TPKX | LIVE-OBSERVED | Packages repopulated after restart in operator test. |
| PRAVE -> AE Automation drawings | LIVE-PROVEN | Six tester units with labels/RSSI icons. |
| Native AE GNSS with actual field receiver | NOT YET FIELD-PROVEN | Officially supported; needs actual receiver acceptance. |
| F22 -> AE live-position manager | DESIGNED | Build after current baseline; common manager. |
| QR -> AE commands/markers | CONCEPTUAL NEXT | Preserve optical handoff; modernize output. |
| Field Maps exact Factory TPKX | NOT YET LIVE-PROVEN | Test before public compatibility claim. |

## Appendix E. Official Technical References

R1. QGIS Documentation — Generate XYZ tiles (MBTiles). `https://docs.qgis.org/latest/en/docs/user_manual/processing_algs/qgis/rastertools.html` — QGIS documents raster XYZ tile generation from the current project into MBTiles.

R2. Esri — Tile Package Specification. `https://github.com/Esri/tile-package-spec` — Defines TPKX package structure: JSON metadata, thumbnail, tile folder, Compact Cache V2 bundles; Apache 2.0 repository.

R3. Esri — Compact Cache V2 Technical Description. `https://github.com/Esri/raster-tiles-compactcache/blob/master/CompactCacheV2.md` — Documents 128 x 128 bundles, naming, 64-byte header, 131,072-byte index, row-major indexing, combined offset/size record.

R4. ArcGIS Earth — Get started. `https://doc.arcgis.com/en/arcgis-earth/get-started/get-started.htm` — Official ArcGIS Earth product/workflow overview.

R5. ArcGIS Earth Automation API — Using the API. `https://doc.arcgis.com/en/arcgis-earth/automation-api/use-api.htm` — Documents RESTful Automation API and default localhost endpoint.

R6. ArcGIS Earth — Connect and visualize real-time data. `https://doc.arcgis.com/en/arcgis-earth/use/realtime-data.htm` — Documents NMEA GNSS device integration, current location, observations, and tracks.

R7. ArcGIS Earth — Administrator configuration. `https://doc.arcgis.com/en/arcgis-earth/administer/admin-config.htm` — Documents startup layers, tile packages, basemaps, workspace/configuration capabilities.

R8. ArcGIS Enterprise 10.7 — New tile package format. `https://enterprise.arcgis.com/en/get-started/10.7/windows/what-s-new-in-arcgis-enterprise.htm` — Documents TPKX introduction, CompactV2 storage, ArcGIS Pro 2.3, and open specification for third-party read/write solutions.

R9. ArcGIS Pro — Share a tile package. `https://pro.arcgis.com/en/pro-app/latest/help/sharing/overview/tile-package.html` — Documents TPK/TPKX as image-tile packages usable as basemaps in ArcGIS applications including ArcGIS Earth.

## Appendix F. Canonical Project Evidence and Lineage

- Exact v1.0 release ZIP and its `System Files` directory are the primary code truth for the public Factory.
- `MBTiles_to_TPKX_v0_1_0.py` is the converter truth; do not infer converter behavior from older KML/Bloommap converters.
- The 13 Aug 2026 ArcGIS Earth Offline Deployment System continuity paper is historical context, not final v1.0 state; later changes include 96 DPI, final four-source menu, no Neighbor tool, no hash gate, advanced converter, PRAVE API live proof, and v1.0 release acceptance.
- Finished Products is the preferred canonical archive for older proven project tools; historical artifacts may have been superseded.
- Live screenshots are evidence of acceptance state, not merely illustrations. Preserve exact Windows-visible file sizes and elapsed times when recording production tests.
- The v1.0 release is feature-frozen. Any functional expansion should branch to v1.1+ and retain a copy of this accepted release.

## Closing Engineering Statement

Offline GeoStack’s central technical achievement is not a new GIS renderer. It is a clean interoperability bridge: use QGIS for what QGIS already does extremely well—render a multiscale raster map—then preserve that work in the native package structure ArcGIS Earth already knows how to consume. The result is a low-friction offline map manufacturing system that can serve both non-GIS operators and advanced GIS users without forcing either audience into the other’s workflow.

The significance for future AI systems is equally concrete: the successful path depended on reading open specifications, respecting file-format exactness, separating rendering from packaging, preserving proven components, and repeatedly submitting every stage to a real target application. The map on the screen—not the elegance of the theory—remains the final acceptance authority.

> **RELEASE BASELINE**  
> TPKX Map Factory v1.0.0 is RELEASE-ACCEPTED as of 15 August 2026. ArcGIS Earth + native TPKX is the current offline basemap baseline. All future changes must preserve or re-prove this accepted behavior.
