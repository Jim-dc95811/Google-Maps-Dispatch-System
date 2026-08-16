# Offline GeoStack — Software & Downloads

This page is the **one-stop dependency list** for TPKX Map Factory v1.0.0.

If you are setting up a Windows machine from scratch, use the versions below unless a later Offline GeoStack release explicitly changes the baseline.

## Required software

| Component | Required / supported version | Why it is here |
| --- | --- | --- |
| **QGIS** | **3.44.9 Solothurn — 64-bit Windows** | Frozen rendering / `qgis_process` baseline used by TPKX Map Factory v1.0.0 |
| **Python** | **3.14.5 — 64-bit Windows** | Established known-good Python baseline for the Factory and converter |
| **ArcGIS Earth** | Current supported Windows desktop release | Primary runtime/viewer for finished TPKX packages |
| **TPKX Map Factory** | **v1.0.0** | Offline GeoStack map-manufacturing subsystem |

---

## 1. QGIS 3.44.9 Solothurn

**Use the exact 3.44.9 build for the v1.0.0 Factory baseline.**

QGIS has newer 3.44.x maintenance builds now, but Offline GeoStack v1.0.0 was developed and live-proven against **QGIS 3.44.9**. Do not silently substitute a later version when reproducing the accepted baseline.

### Official direct Windows installer

**[Download QGIS 3.44.9 — QGIS-OSGeo4W-3.44.9-1.msi](https://download.qgis.org/downloads/QGIS-OSGeo4W-3.44.9-1.msi)**

### Official QGIS download site

**[QGIS Downloads](https://qgis.org/download/)**

Current QGIS download pages may advertise a newer LTR maintenance build. The direct installer link above is intentionally pinned to the exact **3.44.9** release used by this project.

Expected default project configuration assumes QGIS 3.44.9 is installed in the normal Windows location used by the Factory.

---

## 2. Python 3.14.5

Offline GeoStack v1.0.0 uses **Python 3.14.5** as its established known-good baseline.

### Official Python 3.14.5 release page

**[Python 3.14.5 — Python.org](https://www.python.org/downloads/release/python-3145/)**

On Windows, choose:

**Windows installer (64-bit)**

The Python 3.14 series may have newer maintenance releases. For reproducing the v1.0.0 accepted configuration, use **3.14.5** unless the project baseline is deliberately reopened and retested.

### Python library requirement

**No additional Python packages are required for the core TPKX Map Factory / MBTiles-to-TPKX converter path.**

The converter uses the Python standard library.

---

## 3. ArcGIS Earth

ArcGIS Earth is the primary Offline GeoStack runtime for finished `.tpkx` packages.

### Official Esri download page

**[Download ArcGIS Earth for Windows — Esri](https://www.esri.com/en-us/arcgis/products/arcgis-earth/downloads)**

The project does not currently freeze ArcGIS Earth to one historical installer in the same way it freezes QGIS 3.44.9 and Python 3.14.5. Use the current supported Windows desktop release unless a future compatibility note says otherwise.

---

## 4. Required QGIS project files

TPKX Map Factory v1.0.0 uses two project files supplied in this repository:

**[Open the required_qgis_projects folder](../required_qgis_projects/)**

Download:

- `REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz`
- `ESRI and Google Labels.qgz`

Create this folder on the Windows machine:

```text
C:\Google Earth Project\QGIS\
```

Place both `.qgz` files there with their exact filenames.

These are reference projects. The Factory works from disposable copies during manufacturing; do not use the reference files as ordinary editable QGIS projects.

---

## 5. TPKX Map Factory v1.0.0

The accepted Windows archive is:

```text
TPKX_MAP_FACTORY_v1_0_0.zip
```

See:

**[v1.0.0 Release Record](../releases/README.md)**

The exact accepted archive must be used for public distribution. Do not substitute a test build or a newly reconstructed ZIP and silently call it the accepted v1.0.0 package.

---

# Clean-machine setup order

For the simplest first installation:

1. **Install ArcGIS Earth.**
2. **Install Python 3.14.5 (64-bit).**
3. **Install QGIS 3.44.9 (64-bit).**
4. Create `C:\Google Earth Project\QGIS\`.
5. Put the two required QGZ files in that folder.
6. Extract TPKX Map Factory v1.0.0 completely.
7. Launch the Factory using its packaged BAT launcher.
8. Build a very small test TPKX first.
9. Open the finished TPKX in ArcGIS Earth.

---

## Reproduction rule

If your goal is to reproduce the **known-good v1.0.0 environment**, the important distinction is:

```text
QGIS 3.44.9     PINNED
Python 3.14.5   PINNED
ArcGIS Earth    current supported Windows desktop release
```

Do not assume that “newer must be better” when validating an established production baseline. New dependency versions can be tested for later Offline GeoStack releases without changing what v1.0.0 means.

---

## Source-data reminder

Installing the software stack does not grant rights to third-party imagery, labels, basemaps, or services. Source licensing, caching, attribution, export, and redistribution rules remain source-specific. See [`SOURCE_AND_LICENSING_NOTE.md`](SOURCE_AND_LICENSING_NOTE.md).
