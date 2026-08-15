# Offline GeoStack — Required QGIS Projects

These are the two reference QGIS projects used by the current **TPKX Map Factory v1.0.0** workflow.

## Install location

Create this directory on the Windows map-manufacturing machine:

```text
C:\Google Earth Project\QGIS\
```

Place both files there with these exact names:

```text
REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz
ESRI and Google Labels.qgz
```

## What they do

### `REQUIRED_FACTORY_PROJECT_DO_NOT_EDIT.qgz`

Primary Factory reference project used for the standard source-selection workflow.

### `ESRI and Google Labels.qgz`

Reference project for the accepted **Esri World / Google Labels** cartographic blend. QGIS performs the layer composition before MBTiles creation; the MBTiles → TPKX converter remains unaware of the individual layers that produced the pixels.

## Protection model

These are reference masters. The Factory uses disposable working copies during production rather than intentionally rewriting the reference file in place.

The project intentionally does **not** use a SHA-256/hash gate in the public Factory. Keep a known-good archive/download copy and mark the installed reference files read-only if desired.

## Version baseline

- QGIS: **3.44.9**
- Factory: **TPKX Map Factory v1.0.0**
- Current master project: **Offline GeoStack**

Do not casually modify these reference projects and then assume the resulting cartography is still the accepted v1.0 baseline. If a new recipe is desired, make a controlled copy, test it on a small area, visually accept it in ArcGIS Earth, and treat the change as a new release/recipe.
