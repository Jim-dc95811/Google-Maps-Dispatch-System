# Offline GeoStack Roadmap

## Immediate priority — final Field Maps vote on v0.3.1

A live control test proved:

```text
historical project TPKX -> Field Maps REJECTED
Esri official Usa.tpkx  -> Field Maps ACCEPTED
```

Both used the same physical-card `basemaps` path and the same Field Maps Designer workflow. The defect was therefore isolated to TPKX package construction.

The iterative bench work is now complete enough for one real-target vote.

Current candidate:

```text
ESRI_CANONICAL_TPKX_TEST_v0_3_1.zip
12,018 bytes
SHA-256 dcdac0cbfcb3276e392e71f76aaa73e1e71581728ba2bb64c76efefdd753f1ec
```

Ready-made test package:

```text
small mbtile test v031.tpkx
29,239,000 bytes
SHA-256 91f1f93f2485c5a344b7ac94d30746df8c6b7c1ac5a9c80bb9aa97f6274a3797
```

Bench result:

- Esri ZIP structural signature: PASS;
- actual Esri bundle-header pattern: PASS on all 19 bundles;
- root/iteminfo schema: PASS;
- canonical LOD / Web Mercator / Compact V2 metadata: PASS;
- thumbnail 96-DPI metadata: PASS;
- source tile preservation: 174 / 174 byte-identical;
- remaining structural defect currently known: NONE.

### Resume here

1. copy `small mbtile test v031.tpkx` to `\Android\data\com.esri.fieldmaps\files\basemaps\`;
2. set Field Maps Designer to that exact filename;
3. open it in Field Maps;
4. if it passes, promote v0.3.1 construction into Offline Map Factory and Rasta;
5. regenerate the district TPKX;
6. rebuild the district MMPK from the corrected TPKX;
7. resume full cold/no-Internet card acceptance.

Do not run another operator-side converter debugging loop unless this final Field Maps vote reveals a real defect.

- [TPKX / Field Maps Conformance — 2026-08-20](docs/TPKX_FIELD_MAPS_CONFORMANCE_2026-08-20.md)
- [Canonical TPKX test branch](src/esri_canonical_tpkx_test/README.md)

---

## Converter rule

Esri's official `Usa.tpkx` is the golden master.

The historical converter remains valid evidence for ArcGIS Earth compatibility, but its output failed strict Field Maps acceptance.

v0.3.1 reproduces the actual specimen conventions for the canonical LOD table, Web Mercator metadata, Compact Cache V2 bundle header/index layout, ZIP hierarchy/metadata, item/root schema and thumbnail DPI metadata.

For prerendered raster MBTiles, source-layer/legend data does not exist and is not fabricated; `layers` remains an honest empty array.

Governing rule:

> **When an official working reference implementation exists, reproduce/conform to it first.**

---

## Offline Map Factory 1.0

**Status: BUILT / SELF-TESTED — RELEASE ACCEPTANCE BLOCKED ON FINAL v0.3.1 FIELD MAPS VOTE.**

Current operator feature set remains:

- Google Earth;
- Google Hybrid;
- Esri World;
- Esri World / Google Labels;
- HOME EXTENT, Clipboard History diagonal points, or two manual GPS points;
- Z0-Z20;
- TPKX / MBTiles / Both;
- Advanced existing MBTiles -> TPKX;
- no REST / Static WMTS output.

The QGIS -> MBTiles side remains live-proven. If v0.3.1 passes Field Maps, replace the historical TPKX stage with this construction and then run the normal Factory acceptance sequence.

---

## Historical TPKX Map Factory v1.0.0

**RELEASE-ACCEPTED / FROZEN — for the tested ArcGIS Earth target.**

Do not rewrite or re-zip the accepted artifact. The Field Maps failure narrows the compatibility claim; it does not erase the historical ArcGIS Earth acceptance.

---

## District-card mission

> **A Field Maps user must be able to open the app with zero public Internet and use a district-wide Esri Hybrid map through Z17. The same local map should stop the heavy basemap from burning cellular data when service exists.**

Intended chain after the v0.3.1 vote:

```text
Offline Map Factory
-> corrected district TPKX
-> ArcGIS Pro minimal MMPK wrapper
-> physical microSD
   +-- Field Maps mappackages\DISTRICT.mmpk
   +-- Field Maps basemaps\DISTRICT.tpkx
-> Android
-> Field Maps + ArcGIS Earth Mobile
```

ArcGIS Pro packaging remains PASS, but Pro preserves the source TPKX intact. Rebuild the district MMPK only after corrected TPKX acceptance.

---

## ArcGIS Earth Mobile

Local TPKX remains LIVE-PROVEN on multiple project packages. The strict Field Maps failure must not be generalized into an Earth Mobile failure.

---

## Rasta Pyramid Factory

Rasta v0.1.3 remains LIVE-PROVEN for giant-raster manufacturing and ArcGIS Earth display. Its TPKX stage should inherit v0.3.1 only after the Field Maps vote.

---

## Map Fountain

Map Fountain remains LIVE-PROVEN / PARKED. Preserve it for real shared-storage needs; do not revive it because the converter needed repair.

---

## Governing rules

> **Bench first. Field Maps gets the final vote.**

> **The real target decides acceptance.**
