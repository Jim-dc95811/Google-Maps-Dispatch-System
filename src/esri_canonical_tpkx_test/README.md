# Esri Canonical TPKX Test Branch

## Current artifact

```text
ESRI_CANONICAL_TPKX_TEST_v0_3_1.zip
```

Clean package layout:

```text
ESRI_CANONICAL_TPKX_TEST_v0_3_1/
  RUN ESRI CANONICAL TPKX TEST.bat
  Engine/
    MBTiles_to_TPKX_ESRI_CANONICAL_v0_3_1_TEST.py
```

Exact package identity:

```text
12,018 bytes
SHA-256 dcdac0cbfcb3276e392e71f76aaa73e1e71581728ba2bb64c76efefdd753f1ec
```

Exact source identity:

```text
MBTiles_to_TPKX_ESRI_CANONICAL_v0_3_1_TEST.py
SHA-256 0f4257fab6205f423c576cfd8341292e5b0f547f7387911b14b3e81b0bea32a9
```

## Why this branch exists

ArcGIS Field Maps rejected a TPKX created by the historical project converter while accepting Esri's official `Usa.tpkx` through the same physical-card and Field Maps Designer workflow.

That verified defect reopened converter engineering without modifying the frozen historical Factory release.

## What v0.3.1 copies from the actual Esri specimen

The target is Esri's working `Usa.tpkx`, not merely an interpretation of the written specification.

v0.3.1 reproduces the observed invariant package conventions for:

- canonical Web Mercator LOD 0-23 table;
- Web Mercator origin and spatial-reference objects;
- 256 x 256 / 96 DPI cache metadata;
- Compact Cache V2 packet size 128;
- actual Esri bundle-header fixed values;
- 64-byte bundle header + 131,072-byte row-major index;
- 4-byte tile-size prefixes and 40-bit tile offsets;
- explicit `tile/` and `tile/Lxx/` ZIP directory entries;
- Esri-style ZIP creator/extract versions, DOS attributes and NTFS timestamp-extra-field shape;
- `root.json` and `iteminfo.json` top-level schema;
- `layers: []` for prerendered raster MBTiles, because no honest source-layer/legend dataset exists to reconstruct;
- 200 x 133 RGB thumbnail with Esri-style 96-DPI PNG metadata.

## v0.3.1 self-verification

The converter now refuses to declare success unless the finished TPKX passes its structural checks against the Esri specimen invariants.

For bench-sized MBTiles it also performs automatic byte-level source-to-TPKX verification. Large production inputs skip the full reread by default for speed; `--deep-verify` forces it.

## Bench test — project QGIS MBTiles

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
19 bundles
```

Observed conversion time on the current bench: under one second.

### Independent post-build audit

- ZIP structural signature matches Esri for root files, directories and bundles;
- `root.json` top-level schema/order matches;
- `iteminfo.json` top-level schema/order matches;
- canonical LOD table matches;
- Web Mercator origin and spatial-reference structures match;
- Compact V2 storage metadata matches;
- all 19 bundle headers match the actual Esri fixed-byte pattern;
- thumbnail 96-DPI metadata matches;
- 174 / 174 source MBTiles PNG payloads recovered byte-for-byte;
- 0 missing bundles;
- 0 missing index records;
- 0 payload mismatches;
- no remaining structural defect is currently known from the bench comparison.

## Evidence status

- v0.3.1 conversion: **BENCH PASS**;
- Esri specimen structural audit: **PASS**;
- source tile preservation: **174 / 174 BYTE-IDENTICAL PASS**;
- remaining structural defect found by local analysis: **NONE CURRENTLY KNOWN**;
- ArcGIS Field Maps acceptance: **PENDING ONE FINAL REAL-TARGET VOTE**.

## Next test

Use the already-built candidate:

```text
small mbtile test v031.tpkx
-> physical microSD basemaps folder
-> Field Maps Designer exact filename
-> ArcGIS Field Maps
```

If Field Maps accepts it, promote the v0.3.1 construction into Offline Map Factory and Rasta. If it fails, capture that exact failure and resume forensic analysis without changing unrelated parts of the pipeline.

## Governing rule

> **Do the iterative engineering on the bench. Esri's actual working TPKX is the reference. Field Maps gets the final vote.**
