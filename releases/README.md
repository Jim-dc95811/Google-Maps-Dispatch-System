# Offline GeoStack Releases

## TPKX Map Factory v1.0.0

**Status: RELEASE-ACCEPTED / LIVE-PROVEN — 2026-08-15**

The exact accepted Windows archive is named:

```text
TPKX_MAP_FACTORY_v1_0_0.zip
```

The accepted archive is preserved in the project’s canonical working archive. The GitHub connector used during the repository rebuild could not transmit that binary ZIP intact, so a truncated copy was deliberately removed rather than leaving a false release artifact in public view.

**Do not substitute a reconstructed or partial ZIP and call it the accepted release.**

Until the exact archive is attached directly through GitHub, use this directory for the release record and the root documentation for the architecture.

- [v1.0.0 Release Notes](TPKX_MAP_FACTORY_v1_0_0_RELEASE_NOTES.md)
- [Public Release Checklist](PUBLIC_RELEASE_CHECKLIST.md)
- [Release Lineage](RELEASE_LINEAGE.md)
- [Required QGIS Projects](../required_qgis_projects/)

## Exact acceptance record

The v1.0.0 release smoke test completed:

- manual decimal-degree GPS diagonal-point entry;
- normal QGIS → temporary MBTiles → TPKX build;
- finished `test2 small.tpkx`;
- Windows-visible output size: **12,852 KB**;
- elapsed: **0:00:12**;
- direct ArcGIS Earth rendering: **PASS**.

The large v0.1.6 mechanics frozen into v1.0.0 had already passed both the normal Factory path and the advanced existing-MBTiles conversion path at production-scale tile counts.

## Release discipline

v1.0.0 is feature-frozen. Functional expansion belongs in v1.1+ unless a verified defect requires a maintenance release.
