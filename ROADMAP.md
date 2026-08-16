# Offline GeoStack Roadmap

The v1.0 map-manufacturing baseline is frozen. The roadmap expands the stack **around** proven components rather than reopening them casually.

## v1.0 baseline — frozen

- ✅ TPKX Map Factory v1.0.0 release accepted
- ✅ QGIS 3.44.9 raster manufacturing
- ✅ custom MBTiles → Compact Cache V2 / TPKX bridge
- ✅ advanced existing-MBTiles conversion
- ✅ ArcGIS Earth native TPKX runtime
- ✅ PRAVE → ArcGIS Earth Automation API proof
- ✅ no operational Internet dependency for core map display

## Near-term field integration

### Native GNSS acceptance

**Status:** field acceptance pending

Use the actual field receiver and COM behavior with ArcGIS Earth native NMEA support. Acceptance means reliable own-position display/centering on the real target machine without breaking the PRAVE serial architecture.

### F22 → common live-position manager

**Status:** designed

Decode F22 at the protocol edge and normalize it into the same ArcGIS Earth live-position abstraction used by other remote-unit inputs. Do not create a second renderer merely because the transport differs.

### QR → ArcGIS Earth

**Status:** modernization candidate

Preserve QR as an optical/physical dispatch and command input. Preferred modern output is a bounded Automation API action: destination marker, fly-to, layer toggle, operating-view reset, or other allowlisted command.

## Map-production expansion

### More QGIS recipes

**Status:** open for v1.1+

The four-source v1.0 menu stays frozen. Additional cartographic recipes should be added only after small-area visual acceptance and should not make the beginner GUI harder to operate.

### Advanced raster compatibility

**Status:** potential

Current converter baseline is raster PNG/JPEG MBTiles. Additional raster variations may be considered only with controlled fixtures and ArcGIS Earth acceptance. Vector/PBF support is not a v1.0 goal.

## Deployment polish

### ArcGIS Earth workspace profile

**Status:** partially explored

Investigate a deliberate field workspace using startup layers, local packages, custom icons, autosave, and other administrator-supported controls. Freeze only after cold-start and offline acceptance.

### ArcGIS Field Maps crossover

**Status:** not yet live-proven

Test an exact Factory-produced TPKX on the intended Android/iOS Field Maps workflow before making a public compatibility claim.

## Public documentation / community

- Publish the exact accepted v1.0 ZIP through a direct GitHub binary upload.
- Publish a clean-machine start-to-finish map-manufacturing demonstration.
- Present the MBTiles → TPKX bridge to GIS/QGIS/ArcGIS Earth technical audiences.
- Keep legacy Google Earth material available as lineage, not as the current baseline.

## Non-goals

- Rebuilding QGIS inside the Factory
- Rebuilding ArcGIS Earth
- Turning the baseline into a multi-user map server
- Making cloud connectivity mandatory
- Hiding evidence status behind marketing language
- Rewriting proven components merely because a cleaner implementation seems possible

## Governing rule

> **New capability must earn its way into the baseline by answering to the same live target that accepted the old capability.**
