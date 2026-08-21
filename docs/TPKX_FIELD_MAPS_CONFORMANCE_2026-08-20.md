# TPKX / Field Maps Conformance — 2026-08-20

## Executive result

ArcGIS Field Maps rejected a project-converter TPKX while accepting Esri's official `Usa.tpkx` through the same physical-card, Designer map, `basemaps` directory and general Web Mercator setup.

Therefore:

- the Field Maps path is proven;
- the historical converter output is not Field Maps-conformant;
- Esri's actual working `Usa.tpkx` is the golden master;
- the frozen historical Factory release remains valid for its actual ArcGIS Earth acceptance history, but its converter must not be promoted as generally Field Maps-compatible.

## Decisive control

```text
same physical microSD
same Field Maps app
same Designer map
same basemaps folder

project converter TPKX -> REJECTED
Esri official Usa.tpkx -> ACCEPTED
```

Field Maps reported the project-built package as spatial-reference incompatible.

## Why the ArcGIS Pro MMPK does not repair the TPKX

ArcGIS Pro 3.7 successfully created small and district-scale MMPKs from existing project TPKX files. Forensic inspection showed that Pro preserved the source TPKX intact under `commondata/new_tpkx/` and referenced it locally from the MMPK.

The Pro bridge is valid packaging proof, but it is not a TPKX sanitizer. Correct the TPKX first; then rebuild the district MMPK.

## First verified metadata deviation

The historical converter calculated the Web Mercator LOD resolution/scale values instead of copying Esri's canonical values.

Example LOD 0 scale:

```text
historical converter: 591657527.5917094
Esri native sample:    591657527.591555
```

`ESRI_CANONICAL_TPKX_TEST_v0_2_0` corrected that table and copied Esri's origin/spatial-reference conventions.

## v0.2.0 live conversion

The v0.2.0 test converter was run on the real Windows machine against `small mbtile test(1).mbtiles`.

Result:

- started normally;
- completed normally;
- produced `small mbtile test.tpkx`;
- operator reported that conversion completed very quickly.

Status: **LIVE-OBSERVED CONVERSION PASS**.

## Direct structural comparison — v0.2.0 vs official Esri `Usa.tpkx`

The produced `small mbtile test.tpkx` was compared package-wide and byte-level against the exact official Esri `Usa.tpkx` specimen before Field Maps testing.

The supplied `Usa.tpkx` is byte-identical to the file in Esri's public `tile-package-spec` repository: 1,635,803 bytes and Git blob SHA `d6bb368e041174cb12e9aa839f74552ef405f7a5`.

### Confirmed matches

- top-level TPKX concept: `iteminfo.json`, `root.json`, thumbnail, `tile` hierarchy and `.bundle` files;
- ZIP storage method: stored/uncompressed;
- `iteminfo.json` key/type schema;
- canonical LOD 0-23 resolution/scale table;
- Web Mercator origin;
- spatial-reference object structure;
- 256 x 256 tiles;
- root cache DPI 96;
- `esriMapCacheStorageModeCompactV2`;
- packet size 128;
- LOD folder naming and lower-case hexadecimal bundle row/column naming;
- 64-byte bundle header location;
- 131,072-byte bundle index location/size;
- 8-byte row-major tile index records;
- 4-byte tile-size prefixes;
- tile offsets and payload layout.

### Complete source-tile preservation check

The source MBTiles contains **174 PNG tiles** across Z0-Z18.

Every source tile was independently located in the new TPKX using the MBTiles TMS-to-ArcGIS row conversion, bundle address, index record and tile offset.

Result:

```text
174 / 174 tile payloads byte-identical
0 missing bundles
0 zero/missing index records
0 payload mismatches
```

The raster data and index mechanics are therefore not the current suspect.

## Remaining literal differences — important

### 1. Bundle header bytes do not match the actual Esri TPKX

The v0.2.0 writer still follows the published Compact Cache V2 header interpretation. Esri's actual `Usa.tpkx` uses different values in three fixed header fields.

| Offset | Interpreted field | Esri `Usa.tpkx` | v0.2.0 |
| ---: | --- | ---: | ---: |
| 4 | Record Count | 0 | 16384 |
| 8 | header field | 131092 | actual maximum tile size |
| 48 | legacy field | 0 | 16 |

The following fields match structurally:

- Version = 3;
- Offset Byte Count = 5;
- Slack Space = 0;
- File Size = actual bundle file size;
- User Header Offset = 40;
- User Header Size = 131092;
- legacy field at 44 = 3;
- legacy field at 52 = 16384;
- legacy field at 56 = 5;
- Index Size = 131072.

This matters because the project rule is now to reproduce Esri's actual working structure, not merely our reading of the published white paper.

Esri's public `raster-tiles-compactcache` repository also currently contains an open issue reporting that its documented/sample-code bundle header does not match actual ArcGIS-produced bundle files.

### 2. Explicit ZIP directory entries

Esri's archive explicitly contains entries such as:

```text
tile/
tile/L00/
tile/L01/
...
```

v0.2.0 writes only the files and relies on implicit ZIP paths.

That is valid ZIP behavior, but it is not a literal copy of the Esri package.

### 3. ZIP entry metadata

Esri's archive uses different ZIP version/external-attribute metadata from Python's default `zipfile.write()` output. This may be harmless to a tolerant reader, but it is another literal structural difference and should be normalized in the next candidate.

### 4. `root.json` layer information

Esri's sample contains a `layers` array. v0.2.0 omits it.

The sample's actual layer records (`wind`, `ushigh`, `counties`, `states`) are map-specific and must not be copied into unrelated imagery. The structural difference is real; the next build needs a correct non-fabricated representation rather than blindly cloning data-specific values.

### 5. Thumbnail PNG metadata

Both packages contain a 200 x 133, 24-bit RGB PNG thumbnail.

Esri's thumbnail contains approximately 96 DPI PNG metadata. v0.2.0's generated thumbnail has no DPI metadata.

## Current status correction

`ESRI_CANONICAL_TPKX_TEST_v0_2_0` is **not** ready for the Field Maps vote yet.

Evidence state:

- conversion execution: **LIVE-OBSERVED PASS**;
- canonical LOD/spatial-reference metadata: **PASS**;
- tile/index/payload preservation: **PASS**;
- literal package conformance to Esri specimen: **NOT YET PASS**;
- Field Maps acceptance: **HOLD / NOT TESTED**.

## Immediate next engineering action

Build the next small conformance candidate by copying Esri's actual package conventions more literally:

1. reproduce the observed Esri bundle-header pattern;
2. emit explicit ZIP `tile/` and LOD directory entries;
3. normalize ZIP entry metadata where practical;
4. determine a correct non-fabricated `layers` representation or verify omission is accepted;
5. add 96 DPI thumbnail metadata;
6. compare the finished package again against `Usa.tpkx`;
7. only then give Field Maps the deciding vote.

Do not rebuild the 52 GB district TPKX or MMPK until the small candidate passes.

## Historical release boundary

`TPKX Map Factory v1.0.0` remains RELEASE-ACCEPTED for its actual 2026-08-15 target: Factory manufacture and ArcGIS Earth rendering.

The new finding narrows the compatibility claim; it does not erase history.

## Side issue — SD reader

The laptop's built-in SD reader produced write-protection behavior with multiple cards/adapters. A second computer wrote successfully. Treat the laptop reader as suspect. The SD card is disposable test media.

## Governing rule

> **Esri's actual working TPKX is the construction reference. The real target decides acceptance.**
