# Offline GeoStack

## Offline map manufacturing + field-system integration

**Offline GeoStack is the master manufacturing and integration project for the four-repository family.**

> **QGIS renders the map. ArcGIS Pro packages the native Field Maps TPKX. The deployment project puts the finished capability in the user's hands.**

**Keywords:** offline GIS, QGIS, GeoTIFF, ArcGIS Pro, ArcGIS Earth, ArcGIS Field Maps, TPKX, MMPK, microSD, GNSS, PRAVE, wildland fire

---

## Current production direction — 2026-08-21

The Field Maps manufacturing path has changed.

The custom MBTiles -> TPKX converter lineage remains useful engineering research, but it is **no longer the production gate for Field Maps**.

The current production chain is:

```text
QGIS
-> finished labeled GeoTIFF in EPSG:3857
-> ArcGIS Pro: Create Map Tile Package
-> native ArcGIS Pro TPKX
-> physical removable storage
-> ArcGIS Field Maps
```

This turn followed a strict target result:

```text
historical project TPKX -> Field Maps REJECTED
canonical v0.3.1 TPKX  -> Field Maps REJECTED
Esri official Usa.tpkx  -> Field Maps ACCEPTED
```

The v0.3.1 rejection occurred even after its package/bundle structure matched the previously inspected `Usa.tpkx` invariants and preserved all test tiles byte-for-byte. That means a hand-built package can still miss behavior that the real ArcGIS toolchain supplies.

ArcGIS Pro now owns native TPKX construction for the Field Maps production branch.

- [Current Project Status — 2026-08-21](docs/PROJECT_STATUS_2026-08-21.md)
- [QGIS GeoTIFF Source Workflow](docs/QGIS_GEOTIFF_SOURCE_WORKFLOW_2026-08-21.md)
- [ArcGIS Pro GeoTIFF -> TPKX Workflow](docs/ARCGIS_PRO_GEOTIFF_TO_TPKX_2026-08-21.md)
- [TPKX / Field Maps Conformance engineering record](docs/TPKX_FIELD_MAPS_CONFORMANCE_2026-08-20.md)

---

## Small native ArcGIS Pro TPKX proof

A labeled QGIS GeoTIFF was created and then packaged with ArcGIS Pro **Create Map Tile Package**.

### QGIS source GeoTIFF

```text
37,767,543 bytes
4096 x 3072 RGB
EPSG:3857
Z18 source resolution = 0.597164283559817 meters/pixel
```

The successful hybrid render order was:

```text
Google Labels   <- top
ESRI Satellite  <- bottom
```

Reversing that order caused the imagery to cover the labels in the exported TIFF.

### ArcGIS Pro native TPKX

```text
tiff test 66.tpkx
38,306,245 bytes
Z0-Z18
PNG24
19 Compact Cache V2 bundles
creator: CreateMapTilePackage ArcGIS Pro
```

Forensic inspection of this real ArcGIS Pro output showed:

- Web Mercator WKID 102100 / latestWKID 3857;
- Compact Cache V2, packet size 128;
- actual Esri bundle-header pattern;
- `layers` contains a real `Raster Layer` record for the source GeoTIFF;
- no explicit ZIP directory records are required by this ArcGIS Pro-created package;
- the root spatial-reference object is simpler than the extended object previously copied into the custom converter.

This native ArcGIS Pro TPKX still needs the real Field Maps runtime vote before being called Field Maps LIVE-PROVEN.

---

## GeoTIFF Factory — new branch

A separate product line has been created deliberately rather than adding more modes to Offline Map Factory:

```text
GEOTIFF FACTORY 0.1.2 TEST
```

Scope is intentionally narrow:

- four map-source choices;
- standard two-point diagonal extent workflow;
- saved HOME EXTENT / Clipboard History / manual two-point entry;
- target detail Z16-Z20;
- fixed EPSG:3857;
- QGIS `Convert map to raster` engine;
- correct hybrid layer order baked in;
- one finished output: `.tif`;
- no MBTiles;
- no TPKX converter;
- no recovery tools.

Package surface remains professional and simple:

```text
RUN GEOTIFF FACTORY.bat
System Files\
```

The test package uses a self-contained QGIS template inside `System Files`; it does not depend at runtime on the historical Factory QGZ paths.

**Status: BUILT / BENCH-CHECKED — WINDOWS/QGIS LIVE TEST PENDING.**

See [GeoTIFF Factory test branch](src/geotiff_factory/README.md).

---

## GeoTIFF detail table

The GeoTIFF is one fixed-resolution master raster. ArcGIS Pro creates the lower zoom levels when it builds the TPKX.

| Target detail | QGIS map units per pixel |
| ---: | ---: |
| Z16 | `2.38865713397468` |
| Z17 | `1.19432856685505` |
| Z18 | `0.597164283559817` |
| Z19 | `0.298582141647617` |
| Z20 | `0.149291070823808325` |

ArcGIS Pro **Maximum Level Of Detail** should match the QGIS GeoTIFF source detail.

---

## District 7 branch

The current district production attempt is:

```text
District 7
Esri Satellite + Google Labels
GeoTIFF source
Z17
map units per pixel = 1.19432856685505
```

A full District 7 Z17 GeoTIFF build was started on the live QGIS machine on 2026-08-21. Completion and finished file size are still pending and must not be inferred until the run finishes.

After the GeoTIFF completes:

```text
District 7 Z17 GeoTIFF
-> ArcGIS Pro Create Map Tile Package
-> native District 7 TPKX
-> physical card
-> Field Maps acceptance
```

---

## Current status

| Subsystem | Status |
| --- | --- |
| QGIS manual GeoTIFF workflow | ✅ **LIVE-PROVEN SMALL TEST** |
| ArcGIS Pro GeoTIFF -> native TPKX | ✅ **LIVE-PROVEN BUILD / FIELD MAPS VOTE PENDING** |
| GeoTIFF Factory 0.1.2 TEST | 🟡 **BUILT / BENCH-CHECKED — LIVE TEST PENDING** |
| District 7 Z17 GeoTIFF | 🟡 **LIVE BUILD STARTED — COMPLETION PENDING** |
| Field Maps Designer + physical `basemaps` path | ✅ **LIVE-PROVEN** |
| Esri official `Usa.tpkx` in Field Maps | ✅ **LIVE-PROVEN** |
| Historical project converter TPKX in Field Maps | ❌ **FAILED** |
| Canonical converter v0.3.1 in Field Maps | ❌ **FAILED** |
| Canonical converter v0.3.2 | 🟡 **BENCH RESEARCH ONLY — NOT PRODUCTION GATE** |
| ArcGIS Earth Windows native project TPKX | ✅ **LIVE-PROVEN** |
| ArcGIS Earth Mobile local project TPKX | ✅ **LIVE-PROVEN on multiple packages** |
| Historical TPKX Map Factory v1.0.0 | ✅ **RELEASE-ACCEPTED / FROZEN FOR EARTH TARGET** |
| Offline Map Factory 1.0 QGIS -> MBTiles side | ✅ **LIVE-PROVEN** |
| ArcGIS Pro existing TPKX -> MMPK bridge | ✅ **PASS, but does not repair source TPKX** |
| Native ArcGIS Earth GNSS | ✅ **LIVE-OBSERVED** |
| PRAVE -> ArcGIS Earth Automation API | ✅ **LIVE-PROVEN** |
| Map Fountain | ✅ **LIVE-PROVEN / PARKED** |
| Operational public-Internet dependency at showtime | **NONE BY DESIGN** |

---

## Historical converter research branch

The converter work is preserved rather than erased.

v0.3.1 proved that the project can reproduce much of Compact Cache V2 correctly, including tile addressing and bundle payloads, but Field Maps still rejected the package.

v0.3.2 added a further PNG `pHYs` normalization experiment after a difference was found between QGIS tiles and Esri's `Usa.tpkx`. It remains bench research and has not displaced the native ArcGIS Pro production path.

A real ArcGIS Pro-generated TPKX now provides a much better specimen for future converter research. In particular it exposes package behaviors that the earlier `Usa.tpkx` comparison did not establish as universal.

See issue #3 and `src/esri_canonical_tpkx_test/README.md`.

---

## Historical product lines

### TPKX Map Factory v1.0.0

**RELEASE-ACCEPTED / FROZEN — 2026-08-15 for its actual ArcGIS Earth target.**

Do not rewrite or relabel the accepted artifact. Field Maps failures narrow its compatibility claim; they do not erase the original acceptance.

### Offline Map Factory 1.0

Its QGIS -> raster MBTiles manufacturing remains useful and live-proven. Its hand-built TPKX stage is not the current Field Maps production route.

### Rasta Pyramid Factory

Rasta v0.1.3 remains LIVE-PROVEN for giant-raster manufacturing and ArcGIS Earth use. A future Field Maps branch should prefer native ArcGIS Pro TPKX production unless a custom converter later earns its own strict Field Maps acceptance.

---

## Four-project family

1. **Offline GeoStack** — map manufacturing + integration + GeoTIFF/ArcGIS Pro production path.
2. **[Rasta Pyramid Factory](https://github.com/Jim-dc95811/Rasta-Pyramid-Factory)** — giant-raster / deep-zoom manufacturing.
3. **[Map Fountain](https://github.com/Jim-dc95811/Map-Fountain)** — LIVE-PROVEN shared-storage/network reference; parked from normal personal-phone deployment.
4. **[Android Field Maps + ArcGIS Earth](https://github.com/Jim-dc95811/Android-Field-Maps-and-ArcGIS-Earth-)** — deployment and real Field Maps acceptance endpoint.

---

## Hard doctrine

> **There can be no operational dependence on public Internet connectivity. Period.**

> **Use the vendor's native production path when it is available and proven.**

> **The real target decides acceptance.**

---

# Offline GeoStack

> **QGIS makes the finished raster. ArcGIS Pro makes the native TPKX. Put the finished map on the card and let Field Maps decide.**
