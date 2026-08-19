# Contributors

Offline GeoStack is a **human-led, AI-assisted engineering project**.

The collaboration itself is part of the project record: field-domain experience supplies the mission, operational judgment, constraints, and real-world acceptance; AI supplies much of the cross-domain implementation required to turn those ideas into working software and technical systems.

## Jim Gaddy

**Project architect, owner, operational designer, and live-test authority**

Jim originated the field problems, defined the operational requirements, selected and rejected architectural directions, performed the real Windows and field-hardware tests, supplied live telemetry and screenshots, made the product-level decisions, and serves as the final authority for what is considered operationally useful and proven.

Primary contributions include:

- overall project architecture and mission;
- offline-first field doctrine;
- terrestrial chart plotter / AVL system concept;
- PRAVE, F22, GNSS, QR, and dispatch workflow design;
- firefighter / dispatch use-case definition;
- terrain-imagery and training direction;
- live hardware and Windows acceptance testing;
- map-source and cartographic acceptance;
- operator-interface requirements;
- release go/no-go decisions;
- public project direction and publication.

## ChatGPT / Tool Master

**AI engineering contributor**

ChatGPT, working under the project nickname **Tool Master**, has served as an engineering, coding, GIS research, diagnostic, documentation, packaging, and repository-development partner throughout the project.

Primary contributions include:

- cross-domain system architecture and technical design;
- Python development and Windows tooling;
- the custom raster **MBTiles → TPKX / Esri Compact Cache V2 converter**;
- QGIS automation and Factory integration;
- ArcGIS Earth Automation API integration;
- PRAVE parsing/display integration and test tooling;
- QR receiver / command-bridge engineering lineage;
- KML / Super Overlay / Blooming Onion / Network Earth lineage engineering;
- Rasta Pyramid Factory implementation;
- Map Fountain diagnostic and compatibility work;
- packet-capture and protocol analysis;
- debugging and controlled test design;
- release packaging and regression discipline;
- diagrams, posters, user guides, professional GIS documentation, and future-AI continuity records;
- public repository architecture, curation, documentation, and release structure.

## Attribution note

GitHub's automatic **Contributors** sidebar is generated from commit authorship associated with GitHub accounts. The connected GitHub tooling used for this project performs repository writes through Jim Gaddy's authenticated GitHub account, so those commits may appear under Jim's account rather than as a separate ChatGPT contributor identity.

This file records the engineering contribution explicitly rather than inventing or impersonating a GitHub user account for ChatGPT.

## Development model

The project uses a closed-loop human/AI engineering method:

```text
operational problem / live system state
        ↓
AI research, architecture, code, or diagnostic step
        ↓
human executes on the real target system
        ↓
screenshot / output / packet capture / field result
        ↓
AI analyzes the new evidence
        ↓
next controlled iteration
```

The collaboration does not treat generated code as proof.

The project deliberately distinguishes:

- **DESIGNED**
- **BUILT / SELF-TESTED**
- **LIVE-OBSERVED**
- **LIVE-PROVEN**
- **RELEASE-ACCEPTED / FROZEN**

Real target-system behavior outranks plausible-looking code.

The larger story of the collaboration is told in [The Journey of Ideas](docs/JOURNEY_OF_IDEAS.md), while the cross-domain technical results are summarized in [The Bridges We Had to Build](docs/THE_BRIDGES_WE_HAD_TO_BUILD.md).
