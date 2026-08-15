# Offline GeoStack

## QGIS → TPKX → ArcGIS Earth + Live Field Positioning

### TPKX Map Factory v1.0.0 / ArcGIS Earth Runtime

Architecture, Implementation, Validation, Operational Doctrine, and Future-AI Continuity Reference


System manufacturing concept: operator extent and source selection -> QGIS render engine -> temporary MBTiles -> custom converter -> native TPKX -> ArcGIS Earth.

Release status: v1.0.0 RELEASE ACCEPTED / LIVE-PROVEN

Technical snapshot: 15 August 2026

Project architecture & live validation: Jim Gaddy

AI engineering, code, analysis & documentation: ChatGPT (GPT-5.6 Sol / “Tool Master”)


## Document Control and Evidence Standard

| Role | Authority / contribution |

| --- | --- |

| Project architect, owner, operational designer, and live-test authority | Jim Gaddy |

| AI engineering contractor: format research, code design, converter implementation, integration, technical analysis, documentation | ChatGPT (GPT-5.6 Sol), project nickname “Tool Master” |

| Primary GIS/render engine | QGIS 3.44.9 |

| Primary runtime/viewer | ArcGIS Earth (AE) |


This paper is both a professional GIS engineering record and a cold-start continuity document for future human maintainers and AI systems. It records what was built, why it was built, exactly how the production chain works, what was proven on live Windows hardware, which components remain intentionally frozen, and which adjacent functions are proven, planned, or merely conceptual.

| FUTURE-AI COLD-START TRUTH<br>ArcGIS Earth (AE) + native TPKX is the current baseline. TPKX Map Factory v1.0.0 is release-accepted. The custom MBTiles_to_TPKX_v0_1_0.py converter is a stable component and should not be rewritten casually. QGIS 3.44.9 and Python 3.14.5 are the established Windows versions. The baseline field doctrine is zero operational dependence on Internet connectivity. KML remains supported for interoperability, but native TPKX is the offline basemap path. |

| --- |


| Evidence label | Meaning |

| --- | --- |

| LIVE-PROVEN | Observed on the user’s real Windows hardware and accepted by the target application or field workflow. |

| RELEASE-ACCEPTED | Exact release package passed the defined smoke test and is frozen for distribution. |

| BUILT / SELF-TESTED | Code or package exists and passed local/bench checks but has not yet crossed every intended real-world gate. |

| DESIGNED | Architecture is defined but implementation or field acceptance remains incomplete. |

| CONCEPTUAL | Candidate future capability; do not present as implemented. |


Project-derived observations and test results are identified as such. Statements about QGIS, TPKX, Compact Cache V2, ArcGIS Earth, Automation API, and GNSS behavior are cross-checked against official QGIS or Esri documentation where appropriate. Source imagery licensing and provider terms are separate from the engineering validity of the Factory and must be evaluated for each source and deployment.

## Contents

1. Executive Summary

2. Historical Problem and the 2026 Pivot

3. System Architecture and Design Principles

4. TPKX Map Factory v1.0.0 Release Package

5. QGIS Raster Manufacturing Stage

6. Geographic Extent and Coordinate Handling

7. Cartographic Source Handling and Layer Composition

8. MBTiles as a Temporary Manufacturing Intermediate

9. Custom MBTiles -> TPKX Converter: Technical Implementation

10. Compact Cache V2 Binary Mechanics

11. Precision, Determinism, and “No Fudging” Audit

12. Production Pipeline, Verification, and Cleanup

13. Advanced Existing-MBTiles Conversion Path

14. Human-Factors GUI Design

15. Release Evolution and Engineering Decisions

16. Live Acceptance and Performance Evidence

17. ArcGIS Earth as the Runtime

18. Offline Operational Doctrine and Persistent Geographic Context

19. PRAVE / Live Position Integration through the Automation API

20. GNSS, F22, QR, KML, and Other Integration Paths

21. Deployment Model and Security Boundaries

22. AI-Assisted Engineering Methodology

23. Known Limitations and Non-Goals

24. Future Extension Paths

25. Do-Not-Regress Rules for Future Maintainers and AI Systems

Appendices A-F


## 1. Executive Summary

TPKX Map Factory v1.0.0 is a Windows-based geospatial manufacturing workflow that converts a simple operator request—map source, geographic area, and zoom range—into a single native ArcGIS tile package (.tpkx) that opens directly in ArcGIS Earth. The public workflow deliberately hides the complexity of QGIS project rendering, tile pyramid construction, MBTiles, Compact Cache V2 bundle generation, metadata construction, and package verification. The operator receives one finished TPKX file.

The core interoperability result is that QGIS already has a mature raster rendering pipeline and can generate a raster MBTiles pyramid from the current project, while Esri’s TPKX format is openly documented and stores image tiles in Compact Cache V2 bundles. QGIS documentation exposes a “Generate XYZ tiles (MBTiles)” processing algorithm [R1]. Esri documents TPKX as an open tile package specification containing Compact Cache V2 image tiles, JSON metadata, and a thumbnail, and explicitly describes third-party read/write solutions as an intended use of the open specification [R2, R8]. The Factory connects these two ecosystems.

The custom converter does not re-render the cartography. It reads existing raster PNG/JPEG bytes from the MBTiles SQLite database, converts the tile addressing convention, writes the bytes into Esri Compact Cache V2 bundle files, creates TPKX metadata, and packages the result. In the proven PNG workflow, the map pixels created by QGIS survive the conversion unchanged. The conversion problem is therefore primarily one of exact indexing, binary packing, coordinate conventions, metadata, and packaging—not image synthesis.

The project reached v1.0.0 release acceptance on 15 August 2026. Large production-style builds and the advanced direct-conversion path were already accepted by ArcGIS Earth in v0.1.6. The exact v1.0.0 release ZIP then passed a live smoke test: launch, manual GPS extent entry, normal Factory build, finished TPKX creation, and direct rendering in ArcGIS Earth.

| ONE-SENTENCE ARCHITECTURE<br>QGIS makes the finished pixels; MBTiles carries the temporary tile pyramid; the custom converter repackages those exact tiles into Compact Cache V2; ArcGIS Earth consumes the resulting TPKX natively. |

| --- |


## 2. Historical Problem and the 2026 Pivot

### 2.1 Legacy path: making Google Earth Pro behave as an offline field viewer

The project began with Google Earth Pro because its 3D globe, KML support, and operator familiarity were attractive for terrestrial situational awareness. Substantial engineering was performed around Google Earth-specific constraints: KML SuperOverlay forests, MBTiles-to-KML conversion, offline startup/cache recovery, local HTTP serving, dynamic KML/PNG delivery, and Google Earth Enterprise Client exploration. These efforts were technically useful because they forced a detailed understanding of raster tile pyramids, zoom-level cartography, KML region/LOD behavior, caching, and offline viewer requirements.

The decisive 2026 change was not that the prior work failed; it was that ArcGIS Earth offered a cleaner native destination. ArcGIS Earth accepted existing KML content and, more importantly, directly accepted local TPKX tile packages. Esri describes ArcGIS Earth as a lightweight 3D application for geospatial data and documents local/offline-capable data and tile-package workflows [R4, R5]. The project therefore stopped treating Google Earth compatibility as the system boundary and adopted AE as the primary runtime.

### 2.2 Why TPKX became the target

TPKX is the modern Esri tile-package format. Esri introduced the format with ArcGIS Enterprise 10.7 / ArcGIS Pro 2.3 and stated that the format uses CompactV2 storage and has an open specification specifically enabling custom third-party tile-package solutions [R8]. That is the key historical fact: the target was not a reverse-engineered proprietary container. It was an openly documented Esri package that QGIS simply did not emit directly in the project’s existing workflow.

### 2.3 Design consequence

The new question became: can the proven QGIS raster output be preserved and repackaged into the native tile container that AE already understands? The answer was yes. This turned the project from a viewer-emulation problem into a format-bridge and workflow-automation problem.

## 3. System Architecture and Design Principles


Figure 1. TPKX Map Factory manufacturing workflow. The temporary MBTiles is a factory intermediate; the operator-facing deliverable is the final TPKX.

### 3.1 Normal operator path

1.  Choose one of the approved map/cartography sources.

2.  Choose a geographic area using a saved EPSG:3857 HOME EXTENT, Windows Clipboard History with two diagonal points, or two manually entered latitude/longitude coordinates.

3.  Choose minimum and maximum zoom levels (allowed Z0-Z20).

4.  Press BUILD TPKX MAP and choose the final filename.

5.  QGIS renders a temporary raster MBTiles using the selected project/cartography.

6.  The proven converter creates a Compact Cache V2 TPKX from that MBTiles.

7.  The pipeline verifies the TPKX structure and zoom range.

8.  Temporary files are deleted; the selected destination retains the finished TPKX only.

9.  Open the TPKX directly in ArcGIS Earth.

### 3.2 Advanced GIS path

An advanced user can bypass the standard source/extent/QGIS stage entirely. If a compatible raster MBTiles already exists—perhaps created from a custom QGIS project containing parcels, contours, forestry layers, local imagery, historical scans, utility data, or bespoke symbology—the user presses ADVANCED: MBTILES -> TPKX. The Factory invokes the same proven converter and produces a verified TPKX. This deliberately preserves a simple novice workflow while exposing the real interoperability bridge to GIS professionals.

### 3.3 Frozen design principles

- Native offline package over runtime server dependence for the basemap.

- No operational dependency on Internet connectivity at incident/showtime.

- QGIS owns cartographic composition; the converter does not interpret layer semantics.

- MBTiles is a temporary manufacturing intermediate, not the normal operator deliverable.

- The proven converter is stable and is integrated around rather than casually rewritten.

- The output destination is clean: one finished TPKX on success.

- KML is retained for interoperability and live/external content, but is not forced to carry the offline raster basemap.

- Human operators get a simple, landmark-oriented GUI; advanced users get a direct converter escape hatch.

- Source-specific licensing/permissions are a separate governance layer from the package mechanics.

## 4. TPKX Map Factory v1.0.0 Release Package

The v1.0.0 release package is intentionally small because it does not embed QGIS, Python, ArcGIS Earth, imagery, or a duplicated GIS runtime. It is orchestration, validation, conversion logic, and user-interface code that controls installed components. The exact release ZIP is 60,045 bytes compressed; the contained project files total 178,570 bytes by logical file size. The small footprint is not a measure of algorithmic simplicity: the capability resides in the precise ordering and interaction of the code and binary structures.

| Release component | Purpose | Bytes |

| --- | --- | --- |

| README - START HERE.txt | Operator-facing launch and requirements summary | 772 |

| START TPKX MAP FACTORY.pyw | Minimal GUI handoff launcher | 243 |

| Start TPKX Map Factory.bat | Windows launch entry point | 405 |

| System Files/TPKX_MAP_FACTORY.py | Tkinter GUI, workflow control, icons, heartbeat/progress | 31,214 |

| System Files/TPKX_PIPELINE.py | Normal and advanced TPKX orchestration; verification; TEMP cleanup | 15,025 |

| System Files/MBTiles_to_TPKX_v0_1_0.py | Stable raster MBTiles -> TPKX / Compact Cache V2 converter | 21,318 |

| System Files/DIRECT_MBTILES_ENGINE.py | QGIS native:tilesxyzmbtiles manufacturing engine | 12,792 |

| System Files/FACTORY_CORE.py | QGIS/project/source/extent/process hardening inherited from prior factory | 83,147 |

| System Files/GET_CLIPBOARD_HISTORY.ps1 | Windows Clipboard History two-point helper | 3,052 |

| System Files/Factory_Config.ini | Pinned QGIS paths/render settings/source definitions | 1,216 |

| System Files/README_TPKX_MAP_FACTORY.txt | Engineering/operator reference and smoke-test checklist | 5,050 |


Figure 2. Exact v1.0.0 GUI on the live Windows smoke-test machine. Color icons and persistent bottom controls were added without changing the proven v0.1.6 build/conversion architecture.

## 5. QGIS Raster Manufacturing Stage

### 5.1 Pinned runtime

| Component | Known-good value |

| --- | --- |

| QGIS | 3.44.9 |

| Python | 3.14.5 |

| QGIS project root | C:\Google Earth Project\QGIS\ |

| Primary locked project | REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz |

| Blend project | ESRI and Google Labels.qgz |

| QGIS processing algorithm | native:tilesxyzmbtiles |

| Raster output | PNG MBTiles |

| DPI | 96 |

| Antialiasing | ON |

| Metatile size | 4 |

| Public zoom ceiling | Z20 |


QGIS documentation describes Generate XYZ tiles (MBTiles) as generating raster XYZ tiles from the current QGIS project into a single MBTiles file [R1]. The Factory uses that capability through qgis_process rather than reimplementing cartographic rendering. The project therefore inherits QGIS’s mature handling of layer stacking, rasterization, labeling, source access, symbology, blend order, and project coordinate behavior.

### 5.2 Disposable-project design

The required QGZ project files are reference masters. The Factory validates the required project, creates a disposable copy, modifies/selects source-specific project content as needed, and invokes qgis_process against the disposable project. The reference file is not intentionally rewritten. The project’s chosen protection model is read-only reference files plus archive/download recovery—not hash gating. Earlier SHA-256 enforcement experiments were deliberately removed because they added operational brittleness without improving the desired field workflow.

### 5.3 QGIS preflight

- Factory refuses to build if QGIS Desktop is already running, avoiding project/processing conflicts.

- The configured QGIS installation is located and its reported version is checked against 3.44.9.

- Selected source hosts are tested for reachability during the online manufacturing stage.

- A disposable source-selected QGZ is created.

- qgis_process is launched hidden; JSON parameters include extent, zoom range, DPI, transparent background, antialiasing, PNG tile format, quality, metatile size, and output path.

- During QGIS rendering, the GUI reports elapsed time and growing temporary MBTiles size.

