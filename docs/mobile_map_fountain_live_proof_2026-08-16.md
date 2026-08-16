# USB Map Fountain live proof — 2026-08-16

**Status: LIVE-PROVEN**

The Windows GUI below is the live `Rasta USB Map Fountain v0.2.1 TEST` session serving a large `lago tif.mbtiles` file from the PC/SSD to ArcGIS Earth Mobile through local HTTPS WMTS over Android USB tether.

![USB Map Fountain v0.2.1 live session](images/map_fountain_usb_https_live_2026-08-16.png)

Observed server activity shows the Android client requesting unique per-map WMTS tile URLs and receiving `200` responses.

The same day, three different substantial MBTiles were displayed through the mobile path. Outside Internet connectivity was removed and the local map remained functional.

Operator observation: deliberate pan/zoom was smooth; rapid repeated movement could outrun the current mobile delivery/render path.
