# Bounds

The `Bound` table contains the geographic bounding box definitions that can be applied to layers or used as starting bounds in versions.

## Relevant tables

| Table Name                        | Description                          |
| --------------------------------- | ------------------------------------ |
| Bound                             | Geographic bounding box definitions that can be applied to layers or used as starting bounds in versions |
| Versions                          | Contains a `BoundId` column used to define where the map starts on load |
| Layer                             | Contains an optional `BoundId` column used to define what bounds the layer covers |
| Basemap                           | Contains a `BoundId` column used to define what bounds the basemap covers |

### Bound

This table contains the bound details. The coordinates are defined in Spherical Mercator EPSG:3857.

- `Name` - A friendly name for the bound used by admins
- `Description` - A more detailed description for the bound used by admins
- `BottomLeftX` - The X coordinate for the bottom left of the bounding box
- `BottomLeftY` - The Y coordinate for the bottom left of the bounding box
- `TopRightX` - The X coordinate for the top right of the bounding box
- `TopRightY` - The Y coordinate for the top right of the bounding box

### Versions

Within the `Versions` table, there is a `BoundId` column. Set this to the `Id` in the `Bound` table of the relevant bound and the version will load with that initial extent. 

!!! note

    This does not stop users panning outside of those bounds (basemaps do that), it just sets the start extent when they first load the map.


## Layer

Within the `Layer` table, there is an optional `BoundId` column. Set this to the `Id` in the `Bound` table of the relevant bound and the layer will not attempt to render or allow feature clicks outside of this bound. This can improve performance and efficiency, but is not required. Leave it blank for no bounds.

## Basemap

Within the `Basemap` table, there is a `BoundId` column. Set this to the `Id` in the `Bound` table of the relevant bound to restrict this basemap to that bound. This will also prevent users from panning outside of this bound. 
