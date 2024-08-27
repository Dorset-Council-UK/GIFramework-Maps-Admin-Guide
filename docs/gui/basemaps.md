# Basemaps

All [versions](../gui/versions.md) have one or more basemaps (sometimes referred to as background maps). A basemap is made up of a layer source and a basemap definition.

### Creating the layer source

A basemap first requires a [layer source](../gui/layers.md) to be created that defines where the layer comes from.

The easiest way to create a layer source and then a basemap is to use the [layer wizard](../gui/layers.md#add-a-new-layer-using-the-wizard). This will take you through the steps to create a layer source and then present you with the basemap configuration interface.

### Configuring a basemap

A basemap is similar to a layer, but with a few less options.

- Name: The friendly name for the basemap
- Minimum viewable zoom level: This is the furthest zoomed out this basemap can be rendered at. This will restrict the map from being zoomed out any further than this
- Maximum viewable zoom level: This is the furthest zoomed in this basemap can be rendered at. This will restrict the map from being zoomed in any further than this
- Preview image URL: A URL to a preview image that will appear in the basemaps panel. This can be any valid image file. We recommend it be around 800x200 pixels
- Max bounds: The maximum extent that this basemap should render to. Can be used to prevent basemaps being shown outside of your area of interest

Once created, the basemap can be added to versions just like any other.