# Offline Operation and Persistent Geographic Awareness

## Hard architectural requirement

The project has a non-negotiable operational rule:

> **There can be no operational dependence on Internet connectivity. Period.**

This does not mean the Internet is useless. It means the system must distinguish between **preparation-time connectivity** and **showtime operation**.

Internet access may be useful for:

- manufacturing or refreshing map packages;
- obtaining updated imagery or labels;
- optional online routing/directions;
- downloading software or updates;
- nonessential cloud services.

But loss of Internet connectivity must not prevent essential map viewing or collapse the command picture.

## Why this matters operationally

A laptop can theoretically obtain Internet through:

- a cellular hotspot;
- an LTE/5G modem;
- tethering;
- local Wi-Fi;
- a vehicle router;
- an incident network.

In practice, each adds dependencies:

- signal availability;
- device presence;
- batteries/power;
- account state;
- operator configuration;
- credentials;
- policy restrictions;
- human error;
- last-minute troubleshooting.

A workflow that is easy during routine office use can become unreliable precisely when the incident becomes important.

The system therefore treats locally stored TPKX maps as **operational inventory**, not as a fallback cache.

## Build it online. Carry it offline.

The manufacturing model is:

```text
Before the mission / incident
  use available connectivity
  build or refresh TPKX packages
        ↓
At showtime
  open ArcGIS Earth
  load local TPKX
  operate without network dependence
```

The map is already in the trunk.

## Persistent Geographic Awareness

**Persistent Geographic Awareness** describes the operating condition created when:

- the map is already loaded;
- high-resolution local imagery is available;
- the display is large enough to preserve spatial context;
- own-position GNSS keeps the operator geographically oriented;
- the map remains visible without repeated searches or network requests.

The operator no longer has to repeatedly ask a device:

```text
Where am I?
What is down that road?
What is around me?
```

The information remains present in the visual field.

## Position versus place

A traditional 2D location marker answers:

```text
I am at the X.
```

A continuously visible high-resolution geographic display can answer:

```text
I am on this road,
in this forest,
inside this drainage/terrain,
with these access routes and features around me.
```

That is the difference between **positional awareness** and **geographic awareness**.

## Why display size matters

High-resolution satellite imagery is not merely a collection of isolated objects. Human interpretation depends heavily on relationships and pattern recognition across space:

- road geometry;
- vegetation transitions;
- clearings;
- structures;
- ridges and drainages;
- access routes;
- surrounding development;
- relative distances and orientation.

A phone can be excellent for personal navigation and close inspection of one feature, but a command/planning function benefits from a larger display because more spatial context remains visible simultaneously.

The project therefore treats phones as useful field devices while preserving a role for a proper PC display as the larger geographic command surface.

## Broad non-emergency use

The same architecture is useful outside emergency operations.

Examples include:

- rural delivery and service work;
- forestry;
- utility crews;
- property inspection;
- hunting/farm/land management;
- surveying support;
- real-estate/property context;
- remote-area travel.

A driver approaching an unfamiliar forest road can inspect what lies ahead even where cell service is absent. Operationally, a local satellite map can function like a pre-flown aerial reconnaissance view.

## ArcGIS Earth session behavior

Live observation during this project showed that ArcGIS Earth restores previously loaded TPKX files when the application is restarted. That supports appliance-like behavior: once the desired map stack is loaded, the operator does not have to rebuild it manually after every restart.

## Final doctrine

Internet connectivity is welcome when it is available.

It is never allowed to become the single point of failure for essential operation.
