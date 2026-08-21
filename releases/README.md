# Offline GeoStack Releases

## Current release warning — 2026-08-20

A strict ArcGIS Field Maps control test found that the historical MBTiles -> TPKX converter lineage is accepted by ArcGIS Earth but rejected by Field Maps, while Esri's official `Usa.tpkx` succeeds through the same physical-card/Designer workflow.

This does **not** revoke historical release acceptance. It changes the compatibility boundary.

Use precise language:

- historical TPKX Map Factory v1.0.0: **RELEASE-ACCEPTED / FROZEN for the ArcGIS Earth target actually tested**;
- historical converter output in Field Maps: **FAILED / NEEDS REPAIR**;
- Offline Map Factory 1.0: **not release-accepted; converter conformance repair in progress**;
- Esri-canonical converter v0.2.0 TEST: **BUILT / SELF-TESTED; Field Maps acceptance pending**.

See `../docs/TPKX_FIELD_MAPS_CONFORMANCE_2026-08-20.md`.

---

## Offline Map Factory 1.0

**Status: BUILT / SELF-TESTED — RELEASE ACCEPTANCE BLOCKED ON TPKX CONFORMANCE**

This is the current clean Factory product line.

Feature set:

- four map sources;
- Z0-Z20;
- TPKX / MBTiles / Both;
- one Advanced Tool: existing MBTiles -> TPKX;
- REST / Static WMTS removed from the clean Factory.

Finished-package layout:

```text
OFFLINE MAP FACTORY 1.0 - Installation Guide.pdf
OFFLINE MAP FACTORY 1.0 - User Guide.pdf
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
RUN OFFLINE MAP FACTORY.bat
System Files\
```

The QGIS -> MBTiles side remains valid. The TPKX stage must move to the corrected Esri-canonical construction before the release can be promoted for the current Field Maps deployment mission.

Current candidate records:

- [Offline Map Factory 1.0 Candidate Notes](OFFLINE_MAP_FACTORY_1_0_CANDIDATE_NOTES.md)
- [Offline Map Factory 1.0 Acceptance Checklist](OFFLINE_MAP_FACTORY_1_0_ACCEPTANCE_CHECKLIST.md)
- [Installation Guide PDF](../docs/guides/OFFLINE_MAP_FACTORY_1_0_INSTALLATION_GUIDE.pdf)
- [User Guide PDF](../docs/guides/OFFLINE_MAP_FACTORY_1_0_USER_GUIDE.pdf)

### Revised acceptance gate

After the canonical small-TPKX Field Maps test passes:

1. integrate corrected converter;
2. run real Windows/QGIS MBTiles-only, TPKX-only, Both, and Advanced conversion paths;
3. verify ArcGIS Earth rendering;
4. verify representative Field Maps compatibility when Field Maps is part of the claimed deployment target;
5. verify cleanup/final output state.

Do not promote the new product line while it still contains the historical nonconformant converter.

---

## Historical milestone — TPKX Map Factory v1.0.0

**Status: RELEASE-ACCEPTED / LIVE-PROVEN — 2026-08-15 — ARCGIS EARTH TARGET**

The exact accepted Windows archive is:

```text
TPKX_MAP_FACTORY_v1_0_0.zip
```

That package remains a frozen historical milestone and is not silently replaced by Offline Map Factory 1.0 or by the new converter repair branch.

The accepted archive is preserved in the canonical working archive. A bad/truncated GitHub copy was deliberately removed rather than leaving a false public artifact.

- [v1.0.0 Release Notes](TPKX_MAP_FACTORY_v1_0_0_RELEASE_NOTES.md)
- [Historical v1.0.0 Public Release Checklist](PUBLIC_RELEASE_CHECKLIST.md)
- [Release Lineage](RELEASE_LINEAGE.md)
- [Required QGIS Projects](../required_qgis_projects/)

### Exact acceptance record

The v1.0.0 release smoke test completed:

- manual decimal-degree GPS diagonal-point entry;
- normal QGIS -> temporary MBTiles -> TPKX build;
- finished `test2 small.tpkx`;
- Windows-visible output size: **12,852 KB**;
- elapsed: **0:00:12**;
- direct ArcGIS Earth rendering: **PASS**.

Large normal-Factory and advanced existing-MBTiles conversion paths had also passed ArcGIS Earth at production scale.

### Compatibility notice added 2026-08-20

The v1.0.0 release was never Field Maps-tested at acceptance time. A later strict Field Maps test of the same converter lineage failed while Esri's official TPKX passed.

Therefore do not describe v1.0.0 as Field Maps-conformant. Preserve the accepted binary and historical evidence exactly; repair belongs in a new converter/product lineage.

---

## Release discipline

Different product names and compatibility targets are different release claims.

- **TPKX Map Factory v1.0.0** remains frozen accepted history for ArcGIS Earth.
- **Offline Map Factory 1.0** is current and must earn new acceptance with the corrected converter.
- **Esri-canonical v0.2.0** is a TEST repair branch until Field Maps accepts it.

> **Do not rewrite history. Narrow claims when new evidence requires it.**
