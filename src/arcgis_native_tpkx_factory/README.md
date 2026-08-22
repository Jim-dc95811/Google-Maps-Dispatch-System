# ArcGIS Native TPKX Factory

## Current test artifact

```text
ARCGIS_NATIVE_TPKX_FACTORY_0_1_0_TEST.zip
7,241 bytes
SHA-256 2e1f50fb7b3186855dc88816355c6de395d4a0f08bd645f72a5563289e4d9404
```

Status: **BUILT / LOCAL SYNTAX-TESTED — WINDOWS ARCGIS PRO LIVE TEST PENDING.**

The exact ZIP is preserved in the project Library.

## Purpose

Prove the ArcGIS Pro packaging side by itself before combining it with GeoTIFF Factory.

```text
finished GeoTIFF
-> ArcGIS Pro propy.bat
-> ArcPy
-> arcpy.management.CreateMapTilePackage
-> native Esri TPKX
```

There is no custom TPKX writer in this branch.

## Why this branch is deliberately separate

The project already proved the manual ArcGIS Pro workflow. This test isolates the vendor-native automation stage so it can earn its own live acceptance before it is connected to the GeoTIFF Factory.

After both halves are proven independently, they can be combined into the next TPKX Factory.

## Official Esri wheel being used

The implementation follows Esri's documented standalone-script path:

- `propy.bat` launches the active ArcGIS Pro Python environment;
- `arcpy.mp.ArcGISProject()` opens an existing `.aprx`;
- `Map.addDataFromPath()` adds the finished GeoTIFF;
- `arcpy.management.CreateMapTilePackage()` creates the native tile package.

No mouse automation is used.

## First-test operator inputs

The GUI asks for:

1. finished GeoTIFF;
2. known-good ArcGIS Pro `.aprx` from the manually proven workflow;
3. target maximum zoom Z16-Z20;
4. finished `.tpkx` destination.

The selected APRX is never edited. The worker makes a temporary copy and operates on that copy.

Once this path is live-proven, a frozen known-good APRX template can be included inside the product so the operator no longer has to select one.

## Locked native TPKX recipe

```text
service_type              ONLINE
format_type               PNG24
minimum level of detail   0
maximum level of detail   Z16-Z20 operator choice
package_type               tpkx / CompactV2
create_multiple_packages  CREATE_SINGLE_PACKAGE
extent                     exact GeoTIFF extent
```

The worker also:

- verifies the GeoTIFF is Web Mercator;
- removes existing layers from the temporary map;
- sets the map to EPSG:3857;
- adds the GeoTIFF;
- writes map description/tags because Esri requires them for Create Map Tile Package;
- reports ArcGIS Pro/ArcPy version and geoprocessing messages;
- refuses to overwrite an existing TPKX.

## Clean package root

```text
RUN ARCGIS NATIVE TPKX FACTORY.bat
System Files/
```

## Live acceptance gate

Use the small GeoTIFF that already succeeded manually in ArcGIS Pro, plus the clean APRX from that same manual test.

Pass condition:

1. Factory launches.
2. ArcGIS Pro `propy.bat` is found.
3. ArcPy opens the temporary APRX copy.
4. GeoTIFF is added.
5. Create Map Tile Package runs with the locked recipe.
6. A native `.tpkx` is created.
7. The resulting TPKX opens normally in ArcGIS Earth Mobile and/or the intended local-basemap workflow.
8. Package structure identifies ArcGIS Pro / CreateMapTilePackage as the creator, consistent with the manually created native specimen.

Do not combine this stage with GeoTIFF Factory until this gate passes.
