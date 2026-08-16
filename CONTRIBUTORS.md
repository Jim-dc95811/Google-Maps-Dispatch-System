# Contributors

Offline GeoStack is a human-led, AI-assisted engineering project.

## Jim Gaddy

**Project architect, owner, operational designer, and live-test authority**

Jim originated the field problem, defined the operational requirements, selected and rejected architectural directions, performed the real Windows and field-hardware tests, supplied live telemetry and screenshots, made the product-level decisions, and serves as the final authority for what is considered operationally proven.

Primary contributions include:

- overall project architecture and mission;
- offline-first field doctrine;
- terrestrial chartplotter / AVL system concept;
- PRAVE, F22, GNSS, QR, and dispatch workflow design;
- live hardware and Windows acceptance testing;
- map-source and cartographic acceptance;
- operator-interface requirements;
- release go/no-go decisions;
- public project direction and publication.

## ChatGPT / Tool Master

**AI engineering contributor**

ChatGPT, working under the project nickname **Tool Master**, has served as an engineering, coding, GIS research, diagnostic, documentation, and packaging partner throughout the project.

Primary contributions include:

- cross-domain system architecture and technical design;
- Python development and Windows tooling;
- the custom raster **MBTiles → TPKX / Esri Compact Cache V2 converter**;
- QGIS automation and TPKX Map Factory integration;
- ArcGIS Earth Automation API integration design and implementation support;
- PRAVE parsing/display integration and test tooling;
- KML / Super Overlay / Network Earth lineage engineering;
- packet-capture and protocol analysis;
- debugging and controlled test design;
- release packaging and regression discipline;
- professional GIS documentation and future-AI continuity records;
- public repository architecture, documentation, and release structure.

### Attribution note

GitHub's automatic **Contributors** sidebar is generated from commit authorship associated with GitHub accounts. The connected GitHub tooling used for this project performs repository writes through Jim Gaddy's authenticated GitHub account, so those commits may appear under Jim's account rather than as a separate ChatGPT contributor identity.

This file records the engineering contribution explicitly rather than inventing or impersonating a GitHub user account for ChatGPT.

## Development model

The project uses a closed-loop human/AI engineering method:

```text
operational problem / live system state
        ↓
AI research, design, code, or diagnostic step
        ↓
human executes on the real target system
        ↓
screenshot / output / packet capture / field result
        ↓
AI analyzes the new evidence
        ↓
next controlled iteration
```

The project deliberately distinguishes **DESIGNED**, **BUILT**, **BENCH-PROVEN**, **LIVE-PROVEN**, and **RELEASE-ACCEPTED** states. Real target-system behavior outranks plausible-looking code.
