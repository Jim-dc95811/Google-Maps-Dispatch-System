# Offline GeoStack — Source and Licensing Boundary

Offline GeoStack is a geospatial manufacturing, format-conversion, and field-display project. **Technical capability and source-data rights are separate questions.**

TPKX Map Factory can render or package map content from sources configured in QGIS, but the software does not grant rights to imagery, labels, basemaps, tiles, vendor software, or external services.

Users are responsible for complying with the terms, licenses, caching rules, export restrictions, attribution requirements, and redistribution rules that apply to each source they use.

The custom MBTiles → TPKX converter operates on already-created raster MBTiles and performs deterministic addressing / Compact Cache V2 / TPKX packaging. It is source-agnostic: the binary conversion stage does not determine whether the upstream imagery was permitted to be downloaded, cached, packaged, or redistributed.

Likewise, a QGIS project that contains a working machine endpoint or tile-service configuration proves only that the software can technically request/render that source. It is not a blanket license statement.

## Repository license

The MIT License in the repository applies to original Offline GeoStack software and documentation unless a file states otherwise.

It does **not** transfer rights in third-party map content or vendor products.

See also:

- `../LICENSE`
- `../NOTICE.md`
- provider/dataset terms applicable to the source being used

## Practical project rule

Keep the engineering discussion precise:

```text
Can the stack technically render/package it?
        ≠
Does a particular license permit every intended use?
```

Both questions matter, but they are not the same question.
