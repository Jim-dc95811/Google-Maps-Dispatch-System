# Offline GeoStack

## Offline map manufacturing + field-system integration

**Offline GeoStack is the master manufacturing and integration project for the four-repository family.**

> **QGIS makes the pixels. The Factory packages them. The deployment project puts the finished capability in the user's hands.**

**Keywords:** offline GIS, offline maps, QGIS, ArcGIS Earth, ArcGIS Field Maps, MMPK, TPKX, MBTiles, Compact Cache V2, microSD, cellular-data protection, map rationing, GNSS, PRAVE, wildland fire, human AI engineering

---

## Current priority — final Field Maps vote on specimen-conformant TPKX

A live ArcGIS Field Maps control test on 2026-08-20 isolated a verified defect in the historical MBTiles -> TPKX converter:

```text
historical project TPKX -> Field Maps REJECTED
Esri official Usa.tpkx  -> Field Maps ACCEPTED
```

Both used the same physical-card `basemaps` path and the same Field Maps Designer workflow. Therefore the card path, Designer map and general Web Mercator setup are proven; package construction was the engineering subject.

The repair lineage is now:

- **v0.2.0** corrected Esri's exact canonical LOD/spatial-reference values but still had literal package differences;
- **v0.3.0** reproduced the actual Esri bundle-header / ZIP / thumbnail conventions and passed the first full structural bench audit;
- **v0.3.1** keeps that construction and adds stronger built-in structural verification plus automatic byte-for-byte source-tile verification on bench-sized inputs.

The v0.3.1 output has no currently known structural deviation from the invariant conventions in Esri's official `Usa.tpkx`, and **174 / 174 source tiles were recovered byte-for-byte** from the finished package.

One real Field Maps acceptance vote remains.

- [TPKX / Field Maps Conformance — 2026-08-20](docs/TPKX_FIELD_MAPS_CONFORMANCE_2026-08-20.md)
- [Canonical TPKX test branch](src/esri_canonical_tpkx_test/README.md)
- [Android Field Maps + ArcGIS Earth](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-)

---

## Current status

| Subsystem | Status |
| --- | --- |
| **Offline Map Factory 1.0** | 🟡 **BUILT / SELF-TESTED — RELEASE ACCEPTANCE BLOCKED ON FINAL TPKX FIELD MAPS VOTE** |
| QGIS -> raster MBTiles manufacturing | ✅ **LIVE-PROVEN** |
| Historical MBTiles -> TPKX converter in ArcGIS Earth | ✅ **LIVE-PROVEN** |
| Historical converter output in ArcGIS Field Maps | ❌ **FAILED / SUPERSEDED FOR FIELD MAPS CONFORMANCE** |
| Esri official `Usa.tpkx` in Field Maps from physical microSD | ✅ **LIVE-PROVEN** |
| Esri specimen-conformant converter v0.3.1 | ✅ **BENCH STRUCTURAL PASS — FIELD MAPS FINAL VOTE PENDING** |
| v0.3.1 tile preservation | ✅ **174 / 174 BYTE-IDENTICAL** |
| ArcGIS Pro existing TPKX -> minimal MMPK | ✅ **PASS — small and district-scale packages created** |
| Pro-created MMPK in Windows ArcGIS Earth | ✅ **PASS — rendered while Earth showed Not signed in** |
| ArcGIS Earth Windows native TPKX | ✅ **LIVE-PROVEN** |
| ArcGIS Earth Mobile local TPKX | ✅ **LIVE-PROVEN on multiple project packages** |
| Field Maps Designer + physical `basemaps` path | ✅ **LIVE-PROVEN** |
| Corrected district TPKX + MMPK cold-card acceptance | 🟡 **PENDING v0.3.1 FIELD MAPS PASS** |
| Native ArcGIS Earth GNSS | ✅ **LIVE-OBSERVED** |
| PRAVE -> ArcGIS Earth Automation API | ✅ **LIVE-PROVEN** |
| Map Fountain network delivery proofs | ✅ **LIVE-PROVEN / PARKED REFERENCE** |
| Historical TPKX Map Factory v1.0.0 | ✅ **RELEASE-ACCEPTED / FROZEN FOR ARCGIS EARTH TARGET** |
| TPKX -> MBTiles recovery | ❌ **REJECTED as production path** |
| Operational public-Internet dependency | **NONE BY DESIGN** |

---

## Offline Map Factory 1.0

The current clean Factory product line remains deliberately simple:

- four map sources: Google Earth, Google Hybrid, Esri World, Esri World / Google Labels;
- area from HOME EXTENT, Clipboard History diagonal points, or two manual GPS points;
- Z0-Z20;
- output choice: TPKX / MBTiles / Both;
- Advanced Tool: existing MBTiles -> TPKX;
- no REST / Static WMTS output in the clean product.

Known-good environment:

```text
Windows 10/11 64-bit
QGIS 3.44.9
Python 3.14.5
PNG raster tiles
96 DPI
antialiasing ON
metatile 4
Z0-Z20
```

### Finished-package standard

```text
OFFLINE MAP FACTORY 1.0 - Installation Guide.pdf
OFFLINE MAP FACTORY 1.0 - User Guide.pdf
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
RUN OFFLINE MAP FACTORY.bat
System Files\
```

The operator sees a finished product, not a developer dump.

### Release boundary

The QGIS -> MBTiles side remains valid. The TPKX stage must not be release-promoted for the broader Field Maps mission until v0.3.1 gets the real Field Maps vote.

The historical release remains frozen and its ArcGIS Earth acceptance history remains valid.

---

## v0.3.1 conformance result

Current candidate converter:

```text
ESRI_CANONICAL_TPKX_TEST_v0_3_1.zip
12,018 bytes
SHA-256 dcdac0cbfcb3276e392e71f76aaa73e1e71581728ba2bb64c76efefdd753f1ec
```

Current ready-made test TPKX:

```text
small mbtile test v031.tpkx
29,239,000 bytes
SHA-256 91f1f93f2485c5a344b7ac94d30746df8c6b7c1ac5a9c80bb9aa97f6274a3797
```

Bench checks include the actual Esri bundle-header pattern, explicit ZIP directory hierarchy, Esri-style ZIP metadata, root/iteminfo schema, canonical LOD table, 96-DPI thumbnail metadata, tile addressing, and byte-for-byte source-tile preservation.

v0.3.1 also performs the invariant structural checks itself before declaring success. Bench-sized inputs receive automatic full source-to-package tile verification; `--deep-verify` can force that verification on large inputs.

**Bench result: PASS. No remaining structural defect is currently known.**

---

## District-card mission

> **A Field Maps user must be able to open the app with zero public Internet and use a district-wide Esri Hybrid map through Z17. The same local map should stop the heavy basemap from burning cellular data when service exists.**

The intended chain remains:

```text
Offline Map Factory
-> corrected district TPKX
-> ArcGIS Pro minimal MMPK wrapper
-> physical microSD
   +-- Field Maps mappackages\DISTRICT.mmpk
   +-- Field Maps basemaps\DISTRICT.tpkx
-> Android
-> ArcGIS Field Maps + ArcGIS Earth Mobile
```

ArcGIS Pro packaging remains proven, but Pro preserves the source TPKX intact. Therefore the district MMPK is rebuilt only after the corrected TPKX passes Field Maps.

---

## ArcGIS Earth integration

Live-proven / observed capabilities include local native TPKX, router-hosted TPKX over SMB, ArcGIS Earth Mobile local TPKX, KML/KMZ/NetworkLinks, native GNSS/NMEA, Automation API, drawings/markers and PRAVE remote-unit display.

Known-good GNSS observation:

```text
9600 baud
GLL + RMC present
```

---

## Historical Factory lineage

### TPKX Map Factory v1.0.0

**RELEASE-ACCEPTED / FROZEN — 2026-08-15**

Its actual acceptance target was Factory manufacture plus ArcGIS Earth rendering. That history remains valid. The 2026-08-20 Field Maps test added a stricter compatibility boundary and justified a new converter lineage rather than rewriting the accepted archive.

### REST / Static WMTS exploration

REST experiments remain useful history under Map Fountain but are not part of Offline Map Factory 1.0.

---

## Four-project family

1. **Offline GeoStack** — master map manufacturing + field-system integration.
2. **[Rasta Pyramid Factory](https://github.com/Jim-dc95811/Rasta-Pyramid-Factory)** — giant-raster / deep-zoom manufacturing; its future TPKX stage will inherit the proven replacement converter after the Field Maps vote.
3. **[Map Fountain](https://github.com/Jim-dc95811/Map-Fountain)** — LIVE-PROVEN shared-storage/network delivery reference; parked from normal personal-phone use.
4. **[Android Field Maps + ArcGIS Earth](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-)** — deployment to the user and Field Maps acceptance evidence.

---

## Hard doctrine

> **There can be no operational dependence on public Internet connectivity. Period.**

> **When an official working reference implementation exists, reproduce/conform to it first.**

> **Do the iterative engineering on the bench. Ask the field operator for one acceptance vote, not a stream of debugging experiments.**

> **The real target decides acceptance.**

---

## Start here

- **[TPKX / Field Maps Conformance — 2026-08-20](docs/TPKX_FIELD_MAPS_CONFORMANCE_2026-08-20.md)**
- **[Current Project Status — 2026-08-20](docs/PROJECT_STATUS_2026-08-20.md)**
- **[Canonical TPKX test branch](src/esri_canonical_tpkx_test/README.md)**
- [Android deployment + ArcGIS Earth user features](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-)
- [Map Fountain proof archive](https://github.com/Jim-dc95811/Map-Fountain)

---

# Offline GeoStack

> **Manufacture the geography once. Conform to the real standard. Put the heavy map on the card. Let the real field application decide acceptance.**
