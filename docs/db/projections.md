# Projections

GIFramework Maps can use multiple projections for both the actual map rendering and the display coordinates. The Projections table defines what projections are available to the application.

## Relevant tables

| Table Name                        | Description                          |
| --------------------------------- | ------------------------------------ |
| Projections                       | The projection definitions                               |
| VersionProjections                | Table that defines which versions have which projections |

### Projections

This table contains the projection definition.

- `EPSGCode` - The EPSG code of the projection. 
- `Name` - The name of the projection
- `Description` - A description of what this projection is and where it covers
- `Proj4Definition` - A Proj4 or WKT definition of the projection
- `MinBoundX` - The bottom left X coordinate of this projections maximum bounds, in Lat/Lon
- `MinBoundY` - The bottom left Y coordinate of this projections maximum bounds, in Lat/Lon
- `MaxBoundX` - The top right X coordinate of this projections maximum bounds, in Lat/Lon
- `MaxBoundY` - The top right Y coordinate of this projections maximum bounds, in Lat/Lon
- `DefaultRenderedDecimalPlaces` - The number of decimal places shown by default when showing coordinates in this projection

### VersionProjections

See [VersionProjections](../db/versions.md#versionprojection)
