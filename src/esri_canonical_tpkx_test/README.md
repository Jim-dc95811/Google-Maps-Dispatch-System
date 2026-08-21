# Esri Canonical TPKX Test Branch

## Current artifact

```text
ESRI_CANONICAL_TPKX_TEST_v0_2_0.zip
```

Package layout:

```text
ESRI_CANONICAL_TPKX_TEST_v0_2_0/
  RUN ESRI CANONICAL TPKX TEST.bat
  Engine/
    MBTiles_to_TPKX_ESRI_CANONICAL_v0_2_0_TEST.py
```

## Why this branch exists

ArcGIS Field Maps rejected a TPKX created by the historical project converter while accepting Esri's official `Usa.tpkx` through the same physical-card and Field Maps Designer workflow.

The official `Usa.tpkx` is therefore the golden master. The target is not merely "spec-compatible" output; it is output that conforms closely to Esri's actual working package.

## v0.2.0 improvement

The historical converter calculated the Web Mercator LOD resolution/scale table. v0.2.0 replaced that calculation with Esri's canonical LOD 0-23 values and copied the native Web Mercator origin/spatial-reference conventions.

Example LOD 0 scale:

```text
historical converter: 591657527.5917094
Esri native sample:    591657527.591555
```

The real Windows run completed normally and very quickly, producing `small mbtile test.tpkx`.

## Post-build structural audit — important correction

Before Field Maps testing, the finished `small mbtile test.tpkx` was compared directly against the official Esri `Usa.tpkx` byte/package structure.

### What matches

- top-level `iteminfo.json`, `root.json`, `thumbnail.png`, and `tile/.../*.bundle` concept;
- ZIP entries are stored, not deflated;
- `iteminfo.json` has the same key/type schema;
- canonical LOD 0-23 resolution/scale values now match;
- Web Mercator origin and spatial-reference objects match the Esri specimen;
- tile size 256 x 256, 96 DPI metadata, Compact Cache V2 and packet size 128 match;
- bundle naming uses lower-case hexadecimal row/column addresses and zero-padded LOD folders;
- bundle index layout and tile-record mechanics are valid;
- all 174 source MBTiles PNG payloads were recovered from the new TPKX byte-for-byte with zero mismatches.

### What still does NOT match Esri's actual package

#### 1. Compact Cache V2 bundle header bytes

The v0.2.0 writer still follows the published Compact Cache V2 header interpretation rather than Esri's actual `Usa.tpkx` bundle header.

Observed fields:

| Bundle header offset | Esri `Usa.tpkx` | v0.2.0 output |
| --- | ---: | ---: |
| 4 — Record Count | 0 | 16384 |
| 8 — field value | 131092 | actual max tile size |
| 48 — legacy field | 0 | 16 |

The remaining fixed header fields, file-size value, index size, tile offsets, tile-size prefixes, and index records match structurally.

This is a real deviation. Esri's own public Compact Cache repository also has an open report noting that the documented/sample-code bundle header does not match actual ArcGIS-produced bundle headers.

#### 2. ZIP directory entries

Esri's package explicitly contains directory entries such as:

```text
tile/
tile/L00/
tile/L01/
...
```

v0.2.0 writes only the files and relies on implicit ZIP paths. That is legal ZIP behavior but is not a literal copy of Esri's package layout.

#### 3. ZIP entry metadata

Esri's archive uses different ZIP version/external-attribute metadata than Python's default `zipfile.write()` output. This may be harmless, but it is another literal package difference and should be normalized in the next conformance build.

#### 4. `root.json` layer-information object

The Esri sample contains a `layers` array. The v0.2.0 raster package omits it. The sample's actual layer contents are map-specific and must not be blindly copied, but the structural difference is recorded for the next conformance decision.

#### 5. Thumbnail PNG metadata

Both thumbnails are 200 x 133, 24-bit RGB. Esri's sample also carries approximately 96 DPI PNG metadata; v0.2.0's generated thumbnail does not.

## Current evidence status

- Windows conversion execution: **LIVE-OBSERVED PASS**;
- source tile preservation: **PASS — 174/174 byte-identical**;
- canonical LOD/spatial-reference metadata: **PASS**;
- literal package conformance to Esri `Usa.tpkx`: **NOT YET PASS**;
- ArcGIS Field Maps acceptance of v0.2.0: **NOT TESTED — HOLD**.

Do not spend a Field Maps vote on v0.2.0 yet. Correct the remaining literal package differences first, then produce a new small candidate and compare it again before the real target test.

## Governing rule

> **Esri's actual working TPKX is the construction reference. The published specification is supporting documentation, not permission to diverge from the working specimen. Field Maps is the final judge.**
