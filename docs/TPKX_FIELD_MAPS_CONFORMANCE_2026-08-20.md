# TPKX / Field Maps Conformance — 2026-08-20

## Executive result

A strict ArcGIS Field Maps control test exposed a verified compatibility defect in the project's historical MBTiles -> TPKX converter lineage.

The decisive control was:

```text
same physical microSD
same Field Maps app
same Designer map
same basemaps folder

historical project TPKX -> REJECTED
Esri official Usa.tpkx  -> ACCEPTED
```

That proves the Field Maps Designer workflow, public map, physical-card `basemaps` path, and general Web Mercator setup. The historical converter/package construction is the engineering subject.

## Governing rule

> **Esri's actual working TPKX is the construction reference. Field Maps is the final judge.**

The official Esri `Usa.tpkx` specimen is the golden master. The project no longer treats the written Compact Cache interpretation as sufficient when the actual Esri-produced package differs.

Official control specimen:

```text
Usa.tpkx
1,635,803 bytes
SHA-256 9d014cee353106eced55c747b1b200b62ec6f145596200240e1c4653f7d23e95
```

## Historical converter status

The historical converter remains valid evidence for its actual tested targets:

- ArcGIS Earth Windows: LIVE-PROVEN;
- ArcGIS Earth Mobile: multiple project packages accepted;
- ArcGIS Pro: packages accepted.

It is **not Field Maps-conformant** based on the real 2026-08-20 test.

Do not rewrite the frozen `TPKX Map Factory v1.0.0` archive. Repair belongs in a new converter lineage.

## v0.2.0 — useful intermediate, not literal conformance

`ESRI_CANONICAL_TPKX_TEST_v0_2_0` corrected the first known deviation: the old converter calculated Web Mercator LOD values instead of copying Esri's exact canonical values.

Example LOD 0 scale:

```text
historical converter: 591657527.5917094
Esri native sample:    591657527.591555
```

The v0.2.0 Windows conversion ran successfully and very quickly, but a post-build comparison found additional structural differences. Field Maps testing of v0.2.0 was intentionally held.

### Remaining v0.2.0 differences that were found

- bundle-header fields differed from the actual `Usa.tpkx` bundle headers;
- explicit ZIP directory entries were missing;
- ZIP creator/extract/attribute metadata differed from Esri's archive;
- `root.json` omitted the structural `layers` member;
- generated thumbnail lacked Esri-style ~96-DPI `pHYs` metadata.

Most importantly, the actual Esri bundle header did not match the older published/sample-code interpretation. An open issue in Esri's own Compact Cache repository independently reports the same documentation-versus-actual-bundle discrepancy.

## v0.3.0 — specimen-conformant bench candidate

A new test branch was built:

```text
ESRI_CANONICAL_TPKX_TEST_v0_3_0
```

v0.3.0 copies the actual conventions observed in the official working `Usa.tpkx` wherever the values are structural rather than map-specific.

### Bundle header correction

Every official `Usa.tpkx` bundle inspected uses this fixed header pattern, with only file size varying:

```text
(3, 0, 131092, 5, 0, FILE_SIZE, 40, 131092, 3, 0, 16384, 5, 131072)
```

v0.3.0 now writes that actual Esri pattern instead of the previous interpreted header.

### ZIP construction correction

v0.3.0 reproduces the Esri archive shape:

```text
iteminfo.json
root.json
thumbnail.png
tile/
tile/L00/
tile/L00/R....bundle
tile/L01/
tile/L01/R....bundle
...
```

For the small specimen, ZIP entry metadata now matches Esri's pattern:

- storage method: STORED;
- creator system: MS-DOS / `create_system = 0`;
- creator version: 63;
- extract version: 10 for files, 20 for directories;
- external attribute: `0x20` files, `0x10` directories;
- NTFS timestamp extra-field shape present;
- explicit `tile/` and `tile/Lxx/` directory entries present;
- root entry order matches the official specimen.

### Metadata correction

The following fixed/root structural values match the official specimen:

- exact LOD 0-23 resolution/scale table;
- Web Mercator origin;
- spatial-reference object structure and values;
- 256 x 256 tiles;
- 96 DPI;
- `esriMapCacheStorageModeCompactV2`;
- packet size 128;
- `iteminfo.json` key/type structure;
- `root.json` key ordering/structure;
- `layers` structural member present as an empty array rather than fabricating source-layer/legend metadata;
- 200 x 133 RGB thumbnail with Esri-style 3780 x 3780 pixels/meter `pHYs` metadata.

Map-specific values such as name, GUID, extent, represented zoom range, timestamps, tile bytes, and package file sizes are intentionally allowed to differ.

## Real v0.3.0 local test

The new converter was run locally against the already-supplied small MBTiles and then forensically checked against the official Esri specimen.

Input:

```text
small mbtile test(1).mbtiles
26,906,624 bytes
SHA-256 5b2818217899cd93e6f634f9231ea0a02dbf9dd0825e55ffca44ced0dc28ab6e
174 raster PNG tiles
Z0-Z18
```

Output:

```text
small mbtile test v030.tpkx
29,239,000 bytes
SHA-256 e6a648683a16ef37cdd2eb61465310153858b11e9b288270fda307f8b1c1068e
19 Compact Cache V2 bundles
```

Conversion completed in under one second on the current bench environment.

## 28/28 structural acceptance result

The finished v0.3.0 output passed every local conformance check performed:

1. source tile count preserved: **174 / 174**;
2. TMS -> ArcGIS tile addressing exact: **PASS**;
3. tile image bytes recovered from TPKX: **174 / 174 byte-for-byte SHA-256 matches**;
4. tile size prefixes: **PASS**;
5. `root.json` key structure/order versus Esri specimen: **PASS**;
6. `iteminfo.json` key structure/order: **PASS**;
7. `tileImageInfo`: **PASS**;
8. specification version: **PASS**;
9. service description convention: **PASS**;
10. tile bundle path convention: **PASS**;
11. package spatial reference: **PASS**;
12. units: **PASS**;
13. resampling flag: **PASS**;
14. tile rows: **PASS**;
15. tile columns: **PASS**;
16. DPI: **PASS**;
17. tile origin: **PASS**;
18. tile spatial reference: **PASS**;
19. complete canonical LOD table: **PASS**;
20. export-tiles flag: **PASS**;
21. storage info: **PASS**;
22. `layers` structural member: **PASS** (`[]`, no fabricated metadata);
23. every bundle header matches actual Esri specimen pattern: **PASS**;
24. every ZIP entry metadata pattern matches Esri: **PASS**;
25. explicit `tile/` directory: **PASS**;
26. explicit represented-level directories: **PASS**;
27. root ZIP entry ordering: **PASS**;
28. thumbnail 96-DPI `pHYs`: **PASS**.

**Bench result: 28 / 28 PASS.**

At this point no remaining structural defect has been found in v0.3.0 relative to the official working Esri package conventions that can be reproduced without inventing map-specific data.

## Current artifact identity

```text
ESRI_CANONICAL_TPKX_TEST_v0_3_0.zip
31,448 bytes
SHA-256 7d2b8003cf6f27be9fbf17ea5069018fea30ea3165c4e5d3d981f7fda96287aa
```

The exact tested artifact is preserved in the current workbench / persistent Library.

## Next and only remaining acceptance for v0.3.0

The iterative engineering loop is complete enough for the real-target vote.

The next human test should be one controlled Field Maps acceptance using the already-built v0.3.0 TPKX:

```text
small mbtile test v030.tpkx
-> physical microSD basemaps folder
-> Field Maps Designer exact filename
-> Field Maps
```

### Pass condition

Field Maps accepts and renders the TPKX normally.

If it passes:

1. promote the v0.3.0 construction rules as the replacement converter design;
2. integrate them into Offline Map Factory;
3. propagate them into Rasta TPKX output;
4. regenerate the district TPKX;
5. rebuild the district MMPK from the corrected TPKX;
6. resume cold/no-Internet district-card acceptance.

If it fails, do not return to guesswork. The failure would mean Field Maps depends on some additional behavior not exposed by the current official sample comparison; capture the exact Field Maps failure and resume forensic analysis from that evidence.

## Side issue — SD reader

The laptop's built-in SD reader produced write-protection behavior with multiple cards/adapters. A second computer wrote successfully.

Treat the laptop reader as suspect. The SD card is disposable test media and may be renamed, rewritten, reformatted, or wiped whenever useful to the test.

## Final rule

> **Do the science on the bench. Ask the field operator for one acceptance vote, not a stream of debugging experiments.**
