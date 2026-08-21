# TPKX / Field Maps Conformance — 2026-08-20

## Control result

A strict ArcGIS Field Maps test proved:

```text
same physical microSD
same Field Maps app
same Designer map
same basemaps folder

historical project TPKX -> REJECTED
Esri official Usa.tpkx  -> ACCEPTED
```

Therefore the historical converter/package construction was the defect boundary. The Field Maps path, public Designer map, physical-card `basemaps` directory and general Web Mercator setup are proven.

## Governing rule

> **Esri's actual working TPKX is the construction reference. Field Maps is the final judge.**

The written specification remains supporting documentation. Where the actual Esri package differs, the working package wins.

## Historical converter

The historical converter remains valid evidence for its actual tested targets:

- ArcGIS Earth Windows: LIVE-PROVEN;
- ArcGIS Earth Mobile: multiple packages accepted;
- ArcGIS Pro: packages accepted.

It is not approved as Field Maps-conformant.

The frozen `TPKX Map Factory v1.0.0` archive remains frozen; repair belongs in a new lineage.

## Repair lineage

### v0.2.0

Corrected the first verified metadata deviation: the historical converter calculated Web Mercator LOD values instead of copying Esri's canonical values.

It still differed from Esri's actual package in bundle headers, ZIP directory/entry metadata, `layers` structure and thumbnail DPI metadata. Field Maps testing of v0.2.0 was held.

### v0.3.0

Copied the actual Esri bundle-header and ZIP conventions and passed the first full specimen comparison.

### v0.3.1 — current bench candidate

v0.3.1 preserves the v0.3.0 construction and strengthens the code so the converter itself verifies the invariant Esri structure before declaring success.

Current artifact:

```text
ESRI_CANONICAL_TPKX_TEST_v0_3_1.zip
12,018 bytes
SHA-256 dcdac0cbfcb3276e392e71f76aaa73e1e71581728ba2bb64c76efefdd753f1ec
```

Exact source SHA-256:

```text
0f4257fab6205f423c576cfd8341292e5b0f547f7387911b14b3e81b0bea32a9
```

## What v0.3.1 reproduces

Structural values copied from the official working `Usa.tpkx` include:

- canonical Web Mercator LOD 0-23 table;
- Web Mercator origin and spatial-reference objects;
- 256 x 256 / 96 DPI cache metadata;
- Compact Cache V2 packet size 128;
- actual Esri bundle-header fixed-byte pattern:

```text
(3, 0, 131092, 5, 0, FILE_SIZE, 40, 131092, 3, 0, 16384, 5, 131072)
```

- 64-byte bundle header;
- 131,072-byte row-major bundle index;
- 4-byte tile-size prefixes and packed tile offsets;
- explicit `tile/` and `tile/Lxx/` ZIP directory entries;
- Esri-style ZIP creator/extract versions, DOS attributes and NTFS timestamp-extra-field shape;
- `root.json` and `iteminfo.json` top-level schema/order;
- 200 x 133 RGB thumbnail with Esri-style 96-DPI PNG metadata.

For prerendered raster MBTiles, original GIS layer/legend information does not exist. v0.3.1 therefore uses an honest `layers: []` rather than fabricating data.

## Bench test

Input:

```text
small mbtile test(1).mbtiles
174 PNG tiles
Z0-Z18
```

Output:

```text
small mbtile test v031.tpkx
29,239,000 bytes
SHA-256 91f1f93f2485c5a344b7ac94d30746df8c6b7c1ac5a9c80bb9aa97f6274a3797
19 Compact Cache V2 bundles
```

Conversion completed in under one second on the current bench.

## Independent post-build verification

Result:

- ZIP structural signature matches Esri for files, directories and bundles;
- root/iteminfo schema and order match;
- canonical LOD / Web Mercator / Compact V2 metadata match;
- all 19 bundle headers match the actual Esri fixed-byte pattern;
- thumbnail 96-DPI metadata matches;
- 174 / 174 source MBTiles PNGs recovered from the finished TPKX byte-for-byte;
- 0 missing bundles;
- 0 missing index records;
- 0 payload mismatches;
- no remaining structural defect is currently known from the bench comparison.

v0.3.1 performs the invariant structural checks itself before reporting success. Bench-sized inputs also receive automatic full byte-level source-to-package verification. Large inputs skip the expensive full reread by default; `--deep-verify` forces it.

## Current evidence state

- v0.3.1 conversion: **BENCH PASS**;
- Esri specimen structural audit: **PASS**;
- tile preservation: **174 / 174 BYTE-IDENTICAL PASS**;
- remaining known structural defect: **NONE**;
- ArcGIS Field Maps acceptance: **PENDING ONE FINAL REAL-TARGET VOTE**.

## Next action

Use the already-built candidate:

```text
small mbtile test v031.tpkx
-> physical microSD basemaps folder
-> Field Maps Designer exact filename
-> ArcGIS Field Maps
```

If Field Maps accepts it:

1. promote v0.3.1 construction into Offline Map Factory;
2. propagate it into Rasta TPKX output;
3. regenerate the district TPKX;
4. rebuild the district MMPK from the corrected TPKX;
5. resume cold/no-Internet district-card acceptance.

If Field Maps rejects it, capture that exact failure and resume forensic analysis. Do not change the QGIS MBTiles recipe or unrelated architecture without evidence.

## Side issue — SD reader

The laptop's built-in SD reader produced write-protection behavior with multiple cards/adapters. A second computer wrote successfully. Treat the laptop reader as suspect. The SD card is disposable test media.

> **Do the science on the bench. Ask the field operator for one acceptance vote, not a stream of debugging experiments.**
