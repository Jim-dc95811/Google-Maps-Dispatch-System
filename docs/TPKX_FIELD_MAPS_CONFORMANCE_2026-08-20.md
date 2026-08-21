# TPKX / Field Maps Conformance — 2026-08-20

## Executive result

A strict ArcGIS Field Maps test exposed a verified compatibility defect in the project's historical MBTiles -> TPKX converter lineage.

The failure is **not** the microSD path, Field Maps Designer, public web-map configuration, or general Web Mercator setup.

The decisive control test was:

```text
same physical microSD
same Field Maps app
same Designer map
same basemaps folder

project converter TPKX -> REJECTED
Esri official Usa.tpkx -> ACCEPTED
```

Field Maps reported the project-built package as spatial-reference incompatible. Esri's official `Usa.tpkx` worked after Designer was pointed at that exact filename.

## What is now proven

### LIVE-PROVEN

- Field Maps Designer map `District 7 Local Basemap Test` was created.
- Offline was enabled.
- Basemap source was configured as **File on the device**.
- The map was shared **Everyone (public)**.
- Physical-card basemap directory works:

```text
\Android\data\com.esri.fieldmaps\files\basemaps\
```

- Esri official `Usa.tpkx` in that directory was accepted by Field Maps.

### FAILED / NEEDS REPAIR

The project-converter-built District 7 TPKX was discovered by Field Maps but rejected with the message that the spatial reference of the file was not compatible with the map.

That same converter lineage remains proven to open in:

- ArcGIS Earth Windows;
- ArcGIS Earth Mobile on multiple project packages;
- ArcGIS Pro.

Therefore the historical converter is **ArcGIS Earth-compatible but not currently accepted as Field Maps-conformant**.

## Why the ArcGIS Pro MMPK result does not repair this

ArcGIS Pro 3.7 successfully wrapped an existing TPKX into a modern MMPK, but forensic inspection showed that Pro preserved the original TPKX intact under:

```text
commondata/new_tpkx/
```

The `.mmap` referenced that packaged local TPKX.

So the MMPK bridge is still a valid packaging proof, but it is not a sanitizer or rewriter for the TPKX. A Field Maps conformance defect in the source TPKX must be corrected before the district MMPK is treated as a clean acceptance candidate.

## Official Esri specimen is now the authority

The project rule is changed deliberately:

> **When an official working reference implementation exists, reproduce/conform to it first. Do not invent an alternative until the reference path has been exhausted.**

Esri's official `Usa.tpkx` is the current golden master for TPKX construction.

Do not patch metadata by guesswork. Do not defend a merely permissive-reader-compatible package. Field Maps is the deciding target for Field Maps compatibility.

## Concrete deviation found

The historical converter calculated Web Mercator LOD resolution/scale values rather than copying Esri's canonical tiling-scheme values.

Example, LOD 0 scale:

```text
historical converter: 591657527.5917094
Esri native sample:    591657527.591555
```

The difference repeats through the LOD table.

This is a real package deviation, but it is **not yet proven to be the sole cause** of the Field Maps rejection.

## Current repair candidate

A separate test package was created without modifying the frozen historical converter:

```text
ESRI_CANONICAL_TPKX_TEST_v0_2_0
```

Its test converter copies Esri's published/native conventions for:

- canonical LOD 0-23 resolutions and scales;
- Web Mercator origin;
- spatial-reference structure;
- `root.json` conventions;
- `iteminfo.json` field types.

The Compact Cache V2 bundle writer remains based on the already-tested published format.

Bench status:

- synthetic MBTiles conversion: PASS;
- ZIP/package structure checks: PASS;
- bundle header/index checks: PASS;
- Field Maps target acceptance: **PENDING**.

## Immediate next test — resume here

Do **not** spend time rebuilding the district-scale products first.

Run the smallest controlled acceptance:

```text
small raster MBTiles
-> ESRI_CANONICAL_TPKX_TEST_v0_2_0
-> small new TPKX
-> physical microSD basemaps folder
-> Field Maps Designer exact filename
-> Field Maps
```

### Pass condition

Field Maps opens the new TPKX normally.

If it passes:

1. promote the canonical construction as the replacement converter design;
2. integrate it into Offline Map Factory and downstream Rasta TPKX output;
3. regenerate the district TPKX;
4. rebuild the district MMPK from the corrected TPKX;
5. resume cold/no-Internet district-card acceptance.

If it fails:

1. do not guess;
2. continue package-wide conformance analysis against `Usa.tpkx`;
3. inspect ZIP layout, `root.json`, `iteminfo.json`, thumbnail/top-level conventions, Compact Cache V2 bundle/index details, and metadata types;
4. make one evidence-driven correction at a time;
5. let Field Maps vote again.

## Status correction for historical releases

Do **not** erase historical evidence.

`TPKX Map Factory v1.0.0` remains RELEASE-ACCEPTED for its actual 2026-08-15 target: successful Factory manufacture and ArcGIS Earth rendering.

The newly discovered defect changes the compatibility claim, not history:

- ArcGIS Earth compatibility: proven;
- Field Maps compatibility of the historical converter output: failed on the current real target;
- canonical Field Maps repair: pending.

## Side issue — SD reader

The laptop's built-in SD reader produced write-protection behavior with multiple cards/adapters. A second computer wrote successfully.

Treat the laptop reader as suspect. The SD card is disposable test media and may be renamed, rewritten, reformatted, or wiped whenever useful to the test.

## Governing rule

> **The real target decides acceptance. Esri's native TPKX is the construction reference; Field Maps is the judge.**
