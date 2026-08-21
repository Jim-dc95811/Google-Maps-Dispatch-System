# AE SYSTEM CHECK — Manual Canonical TPKX Rebuild — 2026-08-20

## Purpose

Use the existing live-proven `AE_SYSTEM_CHECK_v0_1_0.tpkx` as a controlled legacy specimen and manually rebuild the package around the same raster payload using the new Esri-specimen-conformant structure.

This test does **not** require QGIS or MBTiles. It proves that an existing project TPKX can be structurally rebuilt while preserving its actual map tiles.

## Source

```text
AE_SYSTEM_CHECK_v0_1_0(1).tpkx
Z16-Z20
5 Compact Cache V2 bundles
341 raster tiles
```

The source package used the historical converter structure and historical calculated Web Mercator LOD values.

## Reconstruction method

The rebuild preserved the actual source tile index/payload data and map-specific identity/extent information, while replacing the package/container conventions with the current canonical rules:

- exact Esri Web Mercator LOD 0-23 values;
- canonical Web Mercator spatial-reference objects;
- actual Esri bundle-header fixed-byte pattern;
- existing Compact V2 index and tile payload bytes preserved;
- explicit `tile/` and represented `tile/Lxx/` ZIP directory entries;
- Esri-style ZIP creator/extract versions, DOS attributes and NTFS extra-field shape;
- `root.json` canonical top-level structure;
- `layers: []` rather than fabricated source-layer metadata;
- `iteminfo.json` normalized to Esri key/type structure while preserving honest project metadata;
- original 200 x 133 thumbnail preserved with Esri-style 96-DPI `pHYs` metadata added.

## Output

```text
AE_SYSTEM_CHECK_v0_1_0_ESRI_CANONICAL_REBUILD.tpkx
4,198,914 bytes
SHA-256 4ce792c326c062e4a76e3d92da1b3f9ff1558f8a9ca1c367da12c3025f63d0ea
5 bundles
```

## Verification

- canonical v0.3.1 invariant structure check: **PASS**;
- source/rebuild tile addresses: **PASS**;
- source/rebuild tile payloads: **341 / 341 byte-identical**;
- tile payload mismatches: **0**;
- missing index records: **0**;
- remaining structural defect found by bench inspection: **NONE CURRENTLY KNOWN**.

The exact rebuilt TPKX is preserved in the persistent Library under `/AE SYSTEM CHECK/`.

## Evidence boundary

This is a **BENCH RECONSTRUCTION PASS**. ArcGIS Earth / Field Maps runtime acceptance of this rebuilt binary is a separate real-target test.

> Preserve the map data. Replace the nonconformant container structure. Let the real application make the final acceptance decision.
