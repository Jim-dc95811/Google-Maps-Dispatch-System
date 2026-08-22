# Esri Canonical TPKX Test Branch

## Status correction — 2026-08-21

The custom canonical converter is now **RESEARCH / BACKLOG**, not the Field Maps production path.

The key target result is:

```text
historical project TPKX -> Field Maps REJECTED
canonical v0.3.1 TPKX  -> Field Maps REJECTED
Esri official Usa.tpkx  -> Field Maps ACCEPTED
```

v0.3.1 failed even after the local structural audit could not find a remaining defect and all 174 test tiles were preserved byte-for-byte.

That means local specimen matching was not sufficient to prove native Field Maps equivalence.

---

## v0.3.1 evidence preserved

Artifact:

```text
ESRI_CANONICAL_TPKX_TEST_v0_3_1.zip
12,018 bytes
SHA-256 dcdac0cbfcb3276e392e71f76aaa73e1e71581728ba2bb64c76efefdd753f1ec
```

Source:

```text
MBTiles_to_TPKX_ESRI_CANONICAL_v0_3_1_TEST.py
SHA-256 0f4257fab6205f423c576cfd8341292e5b0f547f7387911b14b3e81b0bea32a9
```

Bench input/output:

```text
small mbtile test(1).mbtiles
174 PNG tiles
Z0-Z18

->

small mbtile test v031.tpkx
29,239,000 bytes
19 bundles
```

Bench result:

- source tile preservation: 174 / 174 byte-identical;
- bundle/index mechanics: PASS;
- then-current Esri specimen structural audit: PASS;
- Field Maps: **FAIL — spatial-reference incompatible**.

The bench evidence remains valid; it simply did not predict the stricter target behavior.

---

## v0.3.2 follow-up

After the v0.3.1 failure, PNG `pHYs` metadata was compared more deeply.

Observed:

```text
Usa.tpkx tiles: 3780 x 3780 pixels/meter
QGIS small MBTiles tiles: 3779 x 3779 pixels/meter
AE SYSTEM CHECK synthetic tiles: no pHYs chunk
```

`ESRI_CANONICAL_TPKX_TEST_v0_3_2` normalizes that PNG metadata without re-encoding pixel data.

Bench status: PASS.

Field Maps status: not required for the active production path.

---

## New native ArcGIS Pro reference

A real TPKX produced by ArcGIS Pro **Create Map Tile Package** is now available:

```text
tiff test 66.tpkx
38,306,245 bytes
Z0-Z18
PNG24
19 bundles
creator: CreateMapTilePackage ArcGIS Pro
```

This package exposed important differences from assumptions made while using `Usa.tpkx` as the only golden specimen:

- no explicit ZIP directory records;
- simple root/tile spatial-reference objects containing WKID 102100 / latestWKID 3857;
- populated `layers` containing a Raster Layer record and legend information for the source GeoTIFF;
- native ArcGIS Pro creator metadata.

The populated Raster Layer structure is now a concrete future research lead because v0.3.1 used `layers: []`.

Do not claim that this is the sole root cause until tested independently.

---

## Production path

Field Maps production now uses:

```text
QGIS
-> GeoTIFF
-> ArcGIS Pro Create Map Tile Package
-> native TPKX
-> Field Maps
```

The converter branch should only be reopened when there is a reason to eliminate the ArcGIS Pro dependency.

When reopened, compare against the real ArcGIS Pro-generated raster TPKX first, not only against `Usa.tpkx`.

> **Production uses ArcGIS Pro. Converter work remains preserved research.**
