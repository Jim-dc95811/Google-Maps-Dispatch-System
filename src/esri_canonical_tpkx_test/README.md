# Esri Canonical TPKX Test Branch

## Current artifact

```text
ESRI_CANONICAL_TPKX_TEST_v0_3_0.zip
```

Package layout remains intentionally clean:

```text
ESRI_CANONICAL_TPKX_TEST_v0_3_0/
  RUN ESRI CANONICAL TPKX TEST.bat
  Engine/
    MBTiles_to_TPKX_ESRI_CANONICAL_v0_3_0_TEST.py
```

Exact tested package identity:

```text
31,448 bytes
SHA-256 7d2b8003cf6f27be9fbf17ea5069018fea30ea3165c4e5d3d981f7fda96287aa
```

## Why this branch exists

ArcGIS Field Maps rejected a TPKX created by the historical project converter while accepting Esri's official `Usa.tpkx` through the same physical-card and Field Maps Designer workflow.

That verified defect reopened converter engineering without modifying the frozen historical Factory release.

## v0.2.0 lesson

v0.2.0 fixed the first known metadata difference by copying Esri's exact Web Mercator LOD table instead of calculating it.

A post-build comparison then found that v0.2.0 still differed from Esri's actual working package in bundle headers, ZIP directory/entry metadata, root `layers` structure and thumbnail DPI metadata.

Field Maps testing of v0.2.0 was deliberately held.

## v0.3.0 construction rule

v0.3.0 copies the **actual official `Usa.tpkx` specimen conventions**, not merely the older written Compact Cache interpretation.

### Bundle header

Actual Esri specimen pattern:

```text
(3, 0, 131092, 5, 0, FILE_SIZE, 40, 131092, 3, 0, 16384, 5, 131072)
```

Every v0.3.0 bundle is self-checked against that pattern before conversion is declared complete.

### ZIP package shape

v0.3.0 writes:

```text
iteminfo.json
root.json
thumbnail.png
tile/
tile/Lxx/
tile/Lxx/R....C....bundle
```

and reproduces the official specimen's ZIP creator/extract versions, DOS file/directory attributes, NTFS timestamp extra-field shape, explicit directory entries and root entry order.

### Root metadata

v0.3.0 matches the official fixed structure for:

- canonical LOD 0-23 table;
- Web Mercator origin;
- spatial-reference objects;
- 256 x 256 / 96 DPI;
- Compact V2 storage info / packet size 128;
- `root.json` key structure/order;
- `iteminfo.json` key/type structure;
- `layers` member present as `[]` because raster MBTiles contains no honest source-layer/legend metadata to fabricate;
- 200 x 133 RGB thumbnail carrying Esri-style 3780 x 3780 pixels/meter `pHYs` metadata.

## Local real-data validation

Input:

```text
small mbtile test(1).mbtiles
26,906,624 bytes
SHA-256 5b2818217899cd93e6f634f9231ea0a02dbf9dd0825e55ffca44ced0dc28ab6e
174 PNG tiles
Z0-Z18
```

Output:

```text
small mbtile test v030.tpkx
29,239,000 bytes
SHA-256 e6a648683a16ef37cdd2eb61465310153858b11e9b288270fda307f8b1c1068e
19 bundles
```

Conversion completed in under one second on the current bench.

### Verification

- 174 / 174 source tiles recovered from the TPKX;
- 174 / 174 tile payloads byte-for-byte identical;
- tile addressing and size prefixes exact;
- all bundle headers match official Esri pattern;
- all ZIP metadata checks match official Esri pattern;
- root/iteminfo structures match;
- thumbnail DPI metadata matches;
- total conformance checklist: **28 / 28 PASS**.

## Evidence status

- v0.3.0 conversion: **BENCH PASS**;
- official-specimen structural comparison: **28 / 28 PASS**;
- tile preservation: **174 / 174 PASS**;
- remaining structural defect found by local analysis: **NONE CURRENTLY KNOWN**;
- ArcGIS Field Maps acceptance: **PENDING ONE FINAL REAL-TARGET VOTE**.

## Next test

Do not ask the operator to rerun iterative conversion experiments.

Use the already-built candidate:

```text
small mbtile test v030.tpkx
-> physical microSD basemaps folder
-> Field Maps Designer exact filename
-> ArcGIS Field Maps
```

If Field Maps accepts it, promote these construction rules into Offline Map Factory and Rasta.

If it fails, capture that exact failure and resume forensic analysis. Do not guess.

## Governing rule

> **Do the iterative engineering on the bench. Esri's actual working TPKX is the reference. Field Maps gets the final vote.**
