# PRAVE Live — Remote Units in ArcGIS Earth

**Status: LIVE-PROVEN**

PRAVE Live is an optional Offline GeoStack field feature that places live remote-unit positions directly into **ArcGIS Earth** using the local Automation API.

It is separate from map manufacturing. The Offline Map Factory makes the basemap; PRAVE Live adds live remote field units on top of that map.

## What the user gets

```text
PRAVE radio position reports
→ Windows serial input
→ PRAVE Live
→ ArcGIS Earth local Automation API
→ live remote-unit markers
```

Each remote unit appears in ArcGIS Earth with:

- its normal district + three-digit unit label, such as `7-101`;
- its current latitude / longitude;
- the established RSSI fire-truck icon showing signal level;
- direct replacement of the same logical unit drawing when a new report arrives.

The feature does **not** require public Internet access.

## Own position

PRAVE Live intentionally does not draw the operator's own position from RMC.

ArcGIS Earth native GNSS/GPS owns the local blue-dot position. RMC from the mixed receiver stream is still checksum-validated and logged so the entire input stream remains observable.

This keeps the roles clean:

```text
ArcGIS Earth native GNSS → ME / own position
PRAVE Live              → remote PRAVE units
```

## Live proof

The controlled Windows / ArcGIS Earth acceptance test displayed six representative units:

```text
7-101
7-102
7-103
7-104
7-105
7-106
```

with RSSI states spanning unknown through 5 bars.

Observed healthy state included:

```text
UNITS=6
API_OK=47
API_BAD=0
BAD_RMC=0
BAD_PRAVE=0
RMC=FRESH
```

That moved the PRAVE → ArcGIS Earth path to **LIVE-PROVEN**.

## Original live-proven package

The preserved original package is:

`AE_PRAVE_LIVE_v0_1_0_TEST.zip`

It contains:

```text
AE_PRAVE_LIVE_v0_1_0_TEST.py
README.txt
Run_AE_PRAVE_LIVE_v0_1_0_TEST.bat
Run_AE_PRAVE_SELF_TEST.bat
```

The source and launchers are also published individually in this folder for inspection.

### Original package assumptions

The original proof package was built around:

```text
Serial: COM12 @ 19200 baud, 8-N-1, no flow control
ArcGIS Earth Automation API: http://localhost:8000
RSSI icon folder: C:\MyData\PRAVE_ME\Icons
```

If Windows assigns a different COM port, the original test package requires changing `INPUT_PORT` near the top of the Python file. That is test-era behavior and is not the preferred long-term novice packaging standard.

The Python program also requires `pyserial` for the serial input path.

## ArcGIS Earth setup

1. Open ArcGIS Earth.
2. Open **Settings**.
3. Open **Advanced application settings**.
4. Enable **Automation API**.
5. Leave ArcGIS Earth running.
6. Run the PRAVE Live launcher.

## RSSI icon family

The established icon names are:

```text
firetruck_rssi_unknown.png
firetruck_rssi_1.png
firetruck_rssi_2.png
firetruck_rssi_3.png
firetruck_rssi_4.png
firetruck_rssi_5.png
```

Signal-state thresholds used by the proven implementation:

```text
blank / invalid   unknown
< -110 dBm        1 bar
-110 .. -101      2 bars
-100 .. -91       3 bars
-90 .. -81        4 bars
>= -80 dBm        5 bars
```

## Why it matters

Offline GeoStack is not only about carrying prepared imagery into a dead-coverage area. It can also place local live operational information on top of that geography.

The two jobs stay independent:

```text
Offline Map Factory → prepared local basemap
PRAVE Live          → live remote-unit positions
ArcGIS Earth        → one operational view
```

## Engineering record

For field mapping, parser details, RSSI behavior, and acceptance history, see:

[PRAVE → ArcGIS Earth Integration](../../docs/PRAVE_ARCGIS_EARTH_INTEGRATION.md)

---

**Prepared geography underneath. Live field units on top. No public Internet required.**
