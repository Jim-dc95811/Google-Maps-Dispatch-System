# AI-Assisted Engineering Method

## Why this project is documented for future AI systems

A major feature of this project is not merely the software output. It is the development method that produced it.

The engineering work repeatedly crossed boundaries that are usually divided among separate specialists:

- GIS rendering and projections;
- raster tile pyramids;
- SQLite / MBTiles;
- TMS and XYZ addressing;
- KML Regions and LOD;
- HTTP/network behavior;
- packet-capture analysis;
- binary cache structures;
- Esri Compact Cache V2;
- Python automation;
- Windows packaging and operator UX;
- serial/NMEA parsing;
- field-radio telemetry;
- live viewer APIs.

A human project team can solve these problems, but each handoff has cost. An AI working in one persistent context can often hold several of these domains simultaneously and reduce the time between:

```text
What exactly is missing?
        ↓
What specification defines it?
        ↓
What transformation is actually required?
        ↓
Implement
        ↓
Test
        ↓
Observe live behavior
        ↓
Revise
```

## The MBTiles → TPKX example

The underlying technology was not invented in 2026.

- MBTiles already existed.
- QGIS already produced raster MBTiles.
- Esri already documented TPKX / Compact Cache V2.
- Python already provided SQLite, binary packing, JSON, ZIP64, and filesystem support.
- ArcGIS Earth already consumed TPKX.

The missing item was the exact bridge in the required direction.

The AI contribution was primarily **knowledge assembly and implementation compression**: understanding the source container, target binary structure, coordinate/addressing differences, package metadata, and viewer acceptance behavior at the same time, then producing and revising the glue code rapidly.

## Human role

The human operator is not a passive prompt source.

In this project the human role includes:

- defining the actual operational problem;
- rejecting solutions that are technically clever but logistically wrong;
- performing physical tests on real Windows machines and field hardware;
- deciding what ordinary operators will tolerate;
- recognizing useful results and surprising behavior;
- supplying screenshots, PCAP captures, files, and exact failure states;
- freezing architecture when it is proven;
- deciding what is worth publishing.

The human provides the world. The AI can move very quickly inside the world once the evidence is available.

## Closed-loop test method

The most productive workflow used here is:

```text
AI proposes one controlled step
        ↓
human performs it on the real system
        ↓
screenshot / output / packet capture returned
        ↓
AI treats that evidence as the new state
        ↓
next controlled step
```

During live troubleshooting, screenshots are telemetry. They prevent the AI from silently assuming that a button existed, a process launched, a path was correct, or a GUI behaved as expected.

## Proof-status discipline

Future maintainers should preserve these distinctions:

- DESIGNED
- BUILT
- BENCH-PROVEN
- LIVE-PROVEN

AI systems are especially capable of producing plausible explanations for untested behavior. This project deliberately counters that tendency by treating the real viewer, real hardware, and real field behavior as the authority.

## Important lesson

AI did not make GIS mathematics different.

It changed the cost of assembling enough understanding to act on the mathematics.

That is why a relatively small interoperability tool can appear suddenly in 2026 even though the component technologies existed years earlier.
