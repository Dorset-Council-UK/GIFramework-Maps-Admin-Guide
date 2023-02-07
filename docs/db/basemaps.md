# Basemaps

All [versions](../db/versions.md) have one or more basemaps (sometimes referred to as background maps). A basemap is made up of a layer source and a basemap definition.

## Relevant tables

| Table Name                        | Description                          |
| --------------------------------- | ------------------------------------ |
| Basemap                           | Basic details about available basemaps  |
| LayerSource                       | Defines the source of the basemap |
| VersionBasemap                    | Mapping between basemaps and versions, showing which basemaps are available in which version |

### Basemap

A basemap first requires a [layer source](../db/layers.md) to be created that defines where the layer comes from.

Once this has been created, the basemap table has the following fields to fill in:

- `LayerSourceId` - The `Id` from the `LayerSource` table
- `PreviewImageURL` - A link to a suitable image that can be used in the preview window in the basemaps panel. This should be no more than 1000px wide and 200px tall
- `BoundId` - The `Id` from the [`Bound`](../db/bounds.md) table that defines what the max extent of this basemap is. By setting this to a non-global bound, the user will not be able to pan outside the defined bounding box when this basemap is turned on
- `MaxZoom` - The maximum zoom level this basemap can be used at. This will prevent the user from zooming beyond what the basemap is capable of showing
- `MinZoom` - As above, but for the minimum

### LayerSource

For more information on how to create a suitable layer source, check the [Layer Source](../db/layers.md) documentation

### VersionBasemap

The `VersionBasemap` table defines which basemaps are available in which versions.

- `VersionId` - The `Id` from the `Versions` table
- `BasemapId` - The `Id` from the `Basemap` table
- `IsDefault` - Boolean indicating whether this basemap is the default one for that version
- `DefaultOpacity` - The default opacity (or transparency) of the basemap between 0 (invisible) and 100 (opaque). Leave blank for default of 100
- `DefaultSaturation` - The default saturation of the basemap between 0 (greyscale) and 100 (full colour). Leave blank for default of 100
- `SortOrder` - The position the basemap will appear in the basemaps panel
