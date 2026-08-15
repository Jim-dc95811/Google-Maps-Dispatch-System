# PRAVE → ArcGIS Earth Integration

## Status

**LIVE-PROVEN**

The project’s `$PRAVE` live-position path has been migrated from the earlier Google Earth-oriented display architecture to the **ArcGIS Earth Automation API**.

## Input model

The field/receiver stream can contain:

- `$GPRMC` / `$GNRMC` own-position data;
- `$PRAVE` remote-unit position messages.

The PRAVE decoder validates checksums and extracts the established fields used by the project.

Important established PRAVE field mapping includes:

```text
field 3   latitude
field 4   longitude
field 5   UTC
field 6   GPS status
field 7   satellites
field 8   district / ATPF
field 10  voltage
field 12  RSSI
field 13  individual / ATCO
field 14  state / ATUS
```

Display ID rule:

```text
raw ID = field 8 + field 13 padded to 3 digits
example: 7 + 004 -> 7004 -> display 7-004
```

## RSSI icon states

The established fire-truck icon family is:

```text
firetruck_rssi_unknown.png
firetruck_rssi_1.png
firetruck_rssi_2.png
firetruck_rssi_3.png
firetruck_rssi_4.png
firetruck_rssi_5.png
```

RSSI bands:

```text
blank / invalid   unknown
< -110 dBm        1 bar
-110 .. -101      2 bars
-100 .. -91       3 bars
-90 .. -81        4 bars
>= -80            5 bars
```

## ArcGIS Earth display path

The current test implementation uses the ArcGIS Earth Automation API and native drawing objects rather than creating KML for every live update.

The architecture is conceptually:

```text
mixed serial stream
      ↓
PRAVE / RMC parser
      ↓
normalized unit state
      ↓
ArcGIS Earth Automation API
      ↓
native drawing / picture marker + label
```

The current Drawing API implementation may delete/re-add a drawing with the same logical unit identity when updating because the relevant drawing path does not expose the same update semantics as a conventional PATCH-style live object. If visible flicker ever becomes operationally objectionable, a Graphics API-based implementation can be evaluated separately rather than casually redesigning a proven baseline.

## Controlled live proof

The field tester generated six representative units:

```text
7-101
7-102
7-103
7-104
7-105
7-106
```

with RSSI states spanning unknown through strong signal.

A live ArcGIS Earth test successfully displayed all six units with the custom fire-truck RSSI icon family and labels.

Observed healthy console state included:

```text
UNITS=6
API_OK=47
API_BAD=0
BAD_RMC=0
BAD_PRAVE=0
RMC=FRESH
```

This moved the PRAVE → ArcGIS Earth path from conceptual/built status to **LIVE-PROVEN**.

## Forward architecture

The project should not force all positioning protocols through a single legacy transport merely because the earlier Google Earth implementation used KML.

The preferred pattern is:

```text
protocol-specific decoder
      ↓
normalized live-position record
      ↓
one ArcGIS Earth live-position manager
```

Potential inputs include:

- PRAVE
- F22
- dispatch/QR destination coordinates
- other future position transports

Metadata remains protocol-specific. For example, PRAVE RSSI should not be invented for F22 unless F22 actually supplies equivalent information.

## KML role

KML remains first-class for:

- interoperability;
- saved/static content;
- NetworkLinks;
- external feeds;
- migration of existing material;
- use cases where KML is the appropriate persistent interchange format.

The Automation API simply removes the need to use KML as the default live-position transport when a native API path is cleaner.
