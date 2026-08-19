# Offline GeoStack — Required QGIS Projects

These are the two QGIS project files supplied with **Offline Map Factory 1.0**.

## Install location

Create this exact folder:

```text
C:\Google Earth Project\QGIS\
```

Copy both supplied files into that folder with their names unchanged:

```text
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
```

## What they do

### `REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz`

Primary Factory reference project used by the standard source-selection workflow.

### `ESRI and Google Labels.qgz`

Reference project for the Esri World / Google Labels source choice.

## Protection rule

These are reference masters, not ordinary editable working projects.

Recommended installation step:

- right-click `REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz`;
- Properties;
- mark it **Read-only**;
- Apply.

Do not rename, move, or casually edit either QGZ file after installation.

The Factory uses working copies during manufacturing rather than intentionally rewriting the reference master.

## Current product baseline

- Factory: **Offline Map Factory 1.0**
- Factory status: **BUILT / SELF-TESTED — LIVE ACCEPTANCE PENDING**
- QGIS: **3.44.9**
- Python: **3.14.5**

The earlier **TPKX Map Factory v1.0.0** used the same project lineage and remains a separate RELEASE-ACCEPTED / FROZEN historical milestone.
