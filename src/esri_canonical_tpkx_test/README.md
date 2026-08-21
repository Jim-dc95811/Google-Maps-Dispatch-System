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

The current package is preserved in the project Library and was bench-tested before this GitHub continuity update.

## Why this branch exists

ArcGIS Field Maps rejected a TPKX created by the historical project converter while accepting Esri's official `Usa.tpkx` through the same physical-card and Field Maps Designer workflow.

That is a verified defect sufficient to reopen converter engineering without altering the frozen historical release.

## Main construction change

The historical converter calculated the Web Mercator LOD resolution/scale table.

This TEST branch copies Esri's canonical LOD 0-23 values and native metadata conventions.

Example LOD 0 scale:

```text
historical converter: 591657527.5917094
Esri native sample:    591657527.591555
```

The test branch also follows Esri's native conventions for:

- Web Mercator origin;
- spatial-reference object structure;
- `root.json` conventions;
- `iteminfo.json` field types.

The Compact Cache V2 bundle writer remains based on the existing published-format implementation.

## Evidence status

- synthetic MBTiles conversion: PASS;
- ZIP/package checks: PASS;
- bundle header/index checks: PASS;
- ArcGIS Field Maps acceptance: **PENDING**.

## Exact next test

```text
small raster MBTiles
-> ESRI_CANONICAL_TPKX_TEST_v0_2_0
-> small TPKX
-> physical microSD basemaps folder
-> Field Maps Designer exact filename
-> ArcGIS Field Maps
```

Do not merge this test branch into production merely because bench checks pass.

## Source-publication note

The exact TEST ZIP/source remains preserved in the Library/current workbench. This repository record documents its identity and behavior. If the exact source is published here later, copy the exact tested file rather than reconstructing it from this description.

## Governing rule

> **Esri's official working TPKX is the reference. Field Maps is the judge.**
