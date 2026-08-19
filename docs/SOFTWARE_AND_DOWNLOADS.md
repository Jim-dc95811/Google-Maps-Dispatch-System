# Offline GeoStack — Software & Downloads

This page is the dependency/setup reference for **Offline Map Factory 1.0**.

Current Factory status: **BUILT / SELF-TESTED — LIVE ACCEPTANCE PENDING**.

## Required software

| Component | Version | Role |
| --- | --- | --- |
| **QGIS** | **3.44.9 Solothurn — 64-bit Windows** | Pinned raster rendering engine |
| **Python** | **3.14.5 — 64-bit Windows** | Known-good Factory/converter runtime |
| **ArcGIS Earth** | Current supported Windows release | TPKX live-acceptance/runtime target |
| **Offline Map Factory** | **1.0** | Current clean map-manufacturing product line |

---

## 1. QGIS 3.44.9 Solothurn

Use the exact **3.44.9** build for the current Factory baseline.

Official direct Windows installer:

**[QGIS-OSGeo4W-3.44.9-1.msi](https://download.qgis.org/downloads/QGIS-OSGeo4W-3.44.9-1.msi)**

Official QGIS download site:

**[QGIS Downloads](https://qgis.org/download/)**

Expected default install location:

```text
C:\Program Files\QGIS 3.44.9
```

Do not silently substitute a newer QGIS version while trying to reproduce the current Factory environment.

---

## 2. Python 3.14.5

Official release page:

**[Python 3.14.5 — Python.org](https://www.python.org/downloads/release/python-3145/)**

Choose:

**Windows installer (64-bit)**

During installation, leave the Python launcher enabled and add Python to PATH when offered.

No additional Python packages are required for the core MBTiles → TPKX converter path.

---

## 3. ArcGIS Earth

ArcGIS Earth is the current Windows acceptance/runtime target for finished `.tpkx` packages.

Official Esri download page:

**[ArcGIS Earth for Windows](https://www.esri.com/en-us/arcgis/products/arcgis-earth/downloads)**

The project does not currently pin ArcGIS Earth to one historical maintenance installer in the same way it pins QGIS and Python.

---

## 4. Required QGIS project files

Offline Map Factory 1.0 ships with:

```text
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
```

Create:

```text
C:\Google Earth Project\QGIS\
```

Copy both files there with their names unchanged.

Recommended protection:

- mark `REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz` read-only;
- do not rename, move, or casually edit either reference project.

See [Required QGIS Projects](../required_qgis_projects/).

---

## 5. Offline Map Factory 1.0 package

Finished distribution layout:

```text
OFFLINE MAP FACTORY 1.0 - Installation Guide.pdf
OFFLINE MAP FACTORY 1.0 - User Guide.pdf
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
RUN OFFLINE MAP FACTORY.bat
System Files\
```

The operator launches only:

```text
RUN OFFLINE MAP FACTORY.bat
```

Keep `System Files` beside the BAT file. Do not scatter its internal files into the package root.

---

## Clean-machine setup order

1. Install Python 3.14.5 (64-bit).
2. Install QGIS 3.44.9 (64-bit).
3. Install ArcGIS Earth if the machine will perform TPKX acceptance/viewing.
4. Create `C:\Google Earth Project\QGIS\`.
5. Copy the two supplied QGZ files there.
6. Mark the required Factory reference project read-only.
7. Keep `RUN OFFLINE MAP FACTORY.bat` and `System Files\` together.
8. Launch the Factory.
9. Build a small test product before starting a monster build.

---

## Historical release distinction

**TPKX Map Factory v1.0.0** remains a separate RELEASE-ACCEPTED / FROZEN historical milestone.

**Offline Map Factory 1.0** is a new clean product line with reset numbering. It must earn its own live acceptance; do not transfer the old release label automatically.

---

## Source-data reminder

Installing this software does not grant rights to third-party imagery, labels, basemaps, or services. Source licensing, caching, attribution, export, and redistribution rules remain source-specific.
