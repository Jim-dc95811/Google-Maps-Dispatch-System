# USB Map Fountain live proof — 2026-08-16

**Status: LIVE-PROVEN**

A live `Rasta USB Map Fountain v0.2.1 TEST` session served a large `lago tif.mbtiles` file from the Windows PC/SSD to ArcGIS Earth Mobile through local HTTPS WMTS over Android USB tether.

Observed server activity showed the Android client requesting unique per-map WMTS tile URLs and receiving `200` responses across multiple zoom levels.

The same day, three different substantial MBTiles were displayed through the mobile path. Outside Internet connectivity was removed and the local map remained functional.

Operator observation: deliberate pan/zoom was smooth; rapid repeated movement could outrun the current mobile delivery/render path.

The full architecture/status record is maintained in [`ARCGIS_EARTH_MOBILE_MAP_FOUNTAIN.md`](ARCGIS_EARTH_MOBILE_MAP_FOUNTAIN.md).
