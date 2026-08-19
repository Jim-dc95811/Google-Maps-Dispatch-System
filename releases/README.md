# Offline GeoStack Releases

## Offline Map Factory 1.0

**Status: BUILT / SELF-TESTED — LIVE ACCEPTANCE PENDING**

This is the new clean product line for the main Factory.

Current feature set:

- four map sources;
- Z0–Z20;
- TPKX / MBTiles / Both;
- one Advanced Tool: existing MBTiles → TPKX;
- REST / Static WMTS removed from the current Factory.

Current finished-package layout:

```text
OFFLINE MAP FACTORY 1.0 - Installation Guide.pdf
OFFLINE MAP FACTORY 1.0 - User Guide.pdf
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
RUN OFFLINE MAP FACTORY.bat
System Files\
```

The package has passed internal compile/self-test checks and a controlled MBTiles → TPKX conversion test, but it has **not yet earned RELEASE-ACCEPTED status under the new product line**.

The next gate is a real Windows/QGIS run proving MBTiles-only, TPKX-only, Both, and Advanced MBTiles → TPKX behavior, followed by ArcGIS Earth acceptance of the produced TPKX.

Do not call this a Gold/release-accepted build before that target run passes.

Current candidate records:

- [Offline Map Factory 1.0 Candidate Notes](OFFLINE_MAP_FACTORY_1_0_CANDIDATE_NOTES.md)
- [Offline Map Factory 1.0 Acceptance Checklist](OFFLINE_MAP_FACTORY_1_0_ACCEPTANCE_CHECKLIST.md)
- [Installation Guide PDF](../docs/guides/OFFLINE_MAP_FACTORY_1_0_INSTALLATION_GUIDE.pdf)
- [User Guide PDF](../docs/guides/OFFLINE_MAP_FACTORY_1_0_USER_GUIDE.pdf)

---

## Historical milestone — TPKX Map Factory v1.0.0

**Status: RELEASE-ACCEPTED / LIVE-PROVEN — 2026-08-15**

The exact accepted Windows archive is named:

```text
TPKX_MAP_FACTORY_v1_0_0.zip
```

That package remains a frozen historical milestone and is not silently replaced by Offline Map Factory 1.0.

The accepted archive is preserved in the canonical working archive. A bad/truncated GitHub copy was deliberately removed rather than leaving a false artifact in public view.

- [v1.0.0 Release Notes](TPKX_MAP_FACTORY_v1_0_0_RELEASE_NOTES.md)
- [Historical v1.0.0 Public Release Checklist](PUBLIC_RELEASE_CHECKLIST.md)
- [Release Lineage](RELEASE_LINEAGE.md)
- [Required QGIS Projects](../required_qgis_projects/)

### Exact acceptance record

The v1.0.0 release smoke test completed:

- manual decimal-degree GPS diagonal-point entry;
- normal QGIS → temporary MBTiles → TPKX build;
- finished `test2 small.tpkx`;
- Windows-visible output size: **12,852 KB**;
- elapsed: **0:00:12**;
- direct ArcGIS Earth rendering: **PASS**.

The large v0.1.6 mechanics frozen into v1.0.0 had already passed both the normal Factory path and the advanced existing-MBTiles conversion path at production-scale tile counts.

---

## Release discipline

Different product names are different release lines.

- **TPKX Map Factory v1.0.0** remains the frozen accepted historical line.
- **Offline Map Factory 1.0** is the current clean line and must earn its own live acceptance.

Do not mix evidence status between them.
