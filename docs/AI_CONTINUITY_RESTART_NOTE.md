# OFFLINE GEOSTACK — AI CONTINUITY / RESTART NOTE

## Current truth — 2026-08-18

The current clean Factory product line is:

**OFFLINE MAP FACTORY 1.0**

Status: **BUILT / SELF-TESTED — LIVE ACCEPTANCE PENDING**.

The prior **TPKX Map Factory v1.0.0** remains a RELEASE-ACCEPTED / FROZEN historical milestone. Do not erase or relabel that record.

---

## Offline Map Factory 1.0 contract

Normal operator capability:

- 4 sources: Google Earth, Google Hybrid, Esri World, Esri World / Google Labels;
- area by HOME EXTENT, Clipboard History diagonal points, or two manual GPS points;
- Z0–Z20;
- output: TPKX / MBTiles / Both;
- one Advanced Tool: existing MBTiles → TPKX.

The current Factory deliberately does **not** include REST / Static WMTS output.

Do not reintroduce REST merely because historical TEST branches contain it.

---

## Finished-package standard

User-facing top level:

```text
OFFLINE MAP FACTORY 1.0 - Installation Guide.pdf
OFFLINE MAP FACTORY 1.0 - User Guide.pdf
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
RUN OFFLINE MAP FACTORY.bat
System Files\
```

All support code, tests, internal notes, icons, and implementation machinery belong behind `System Files`.

The operator should not see loose Python files, test BATs, or developer clutter.

Required QGIS project placement:

```text
C:\Google Earth Project\QGIS\
```

with exact filenames:

```text
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
```

---

## Evidence snapshot

- Offline Map Factory 1.0: **BUILT / SELF-TESTED; LIVE ACCEPTANCE PENDING**.
- Historical TPKX Map Factory v1.0.0: **RELEASE-ACCEPTED / FROZEN**.
- MBTiles → TPKX converter: **LIVE-PROVEN lineage**.
- ArcGIS Earth Windows local TPKX: **LIVE-PROVEN**.
- ArcGIS Earth Mobile local TPKX: **LIVE-PROVEN on multiple packages**.
- Native ArcGIS Earth GNSS: **LIVE-OBSERVED**, 9600 baud with GLL + RMC present.
- PRAVE → ArcGIS Earth Automation API: **LIVE-PROVEN**.
- Field Maps Android TPKX sideload to device/microSD: **DOCUMENTED BY ESRI; PROJECT LIVE TEST PENDING**.
- Map Fountain Windows TPKX-over-SMB: **LIVE-PROVEN / PARKED REFERENCE**.
- Map Fountain Android Static REST WMTS: **LIVE-PROVEN / PARKED REFERENCE**.
- TPKX → MBTiles recovery: **REJECTED as production path**.

---

## Next Factory acceptance gate

Run the packaged Offline Map Factory 1.0 on the real Windows/QGIS machine and prove:

1. launcher starts correctly;
2. required QGZ files are found;
3. MBTiles-only build;
4. TPKX-only build;
5. Both build;
6. Advanced MBTiles → TPKX;
7. finished TPKX opens and renders correctly in ArcGIS Earth;
8. cleanup and final-output behavior are correct.

Do not promote Offline Map Factory 1.0 to LIVE-PROVEN / RELEASE-ACCEPTED before this run.

Fortification follows acceptance and should be evidence-driven, not an architecture rewrite.

---

## REST / Static WMTS status

REST work is **PARKED ENGINEERING HISTORY**.

The v1.3/v1.4 experiments proved useful lessons about giant directory trees, packaging overhead, Static REST WMTS, and compact `.restmap` seeds.

Current decision: preserve the record, remove REST from the clean Factory, and reopen it only if a real target again requires it.

---

## Personal-phone deployment direction

```text
Offline Map Factory TPKX
→ microSD card
→ Android
→ ArcGIS Field Maps / ArcGIS Earth
```

The complicated work belongs on the map-maker side. The field user should receive a prepared card and a very short procedure.

Current card-sizing direction:

- district Z17;
- county Z18;
- State Forests / selected high-value Z20;
- Google Hybrid and Esri imagery/labels where useful and storage permits.

Android deployment repository:

`Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-`

---

## Hard requirement

> **There can be no operational dependence on public Internet connectivity. Period.**

Online access may be used during map manufacture or refresh. Essential prepared-map use must survive loss of outside connectivity.

---

## Do not regress

- Do not replace the clean Factory with the REST experimental branch by inertia.
- Do not put developer clutter back at the user-facing package root.
- Do not casually rewrite the proven MBTiles → TPKX converter.
- Do not revive TPKX → MBTiles recovery as a production shortcut.
- Do not require router/server infrastructure for normal personal-phone deployment.
- Do not make public Internet mandatory.
- Do not make normal users understand QGIS/Python/CRS internals.
- Do not confuse vendor documentation or self-test success with project LIVE-PROVEN status.
- Do not display COMPLETE before final verification/publication is complete.

---

## Known-good environment

- Windows 10/11 64-bit
- Python 3.14.5
- QGIS 3.44.9
- PNG tiles
- 96 DPI
- antialiasing ON
- metatile 4
- Z0–Z20

No extra Python packages are required by the core converter path.

---

## Four-project map

1. `Offline-GeoStack` — master field mapping / manufacturing.
2. `Rasta-Pyramid-Factory` — giant-raster pyramid manufacturing.
3. `Map-Fountain` — live-proven router/storage delivery reference; parked / possible future Starlink NAS.
4. `Android-Field-Maps-and-ArcGIS-Earth-` — personal-phone / microSD deployment.

---

## Cold-start reading order

1. `README.md`
2. `ROADMAP.md`
3. `docs/PROJECT_STATUS_2026-08-18.md`
4. `docs/SOFTWARE_AND_DOWNLOADS.md`
5. `docs/QUICK_START.md`
6. `releases/README.md`
7. Android deployment repository
8. Map Fountain only when router/network proof history matters
9. newest commits/issues

> **Keep the Factory simple. Keep the package clean. Let the real target decide acceptance.**
