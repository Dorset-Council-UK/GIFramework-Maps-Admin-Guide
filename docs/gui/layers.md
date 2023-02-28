# Layers

Layers are the bedrock of GIFramework Maps. Without layers, your maps are basically useless.

Layers are pretty configurable, and have lots of various options.

## Add a new layer

There are three parts to creating a layer: layer sources, layer details and layer categories.

### Layer sources

This section covers where your layers come from. Select **Add new layer source** and fill in the details:

- Name - a friendly name for administrators
- Description - a basic description of the layer. This is shown to end users when the layer has no other description metadata available from source
- Layer type - choose the type
- Attribution - the [attribution](../gui/attributions.md) you want your layer to use

Tick the *Create layer source option on save* box to automatically fill in details that will appear on the right side of the screen. You can edit these manually if you need to, but you will need to know what you are doing. For more detailed information on these options, see [database layers](../db/layers.md#LayerSourceOption).

###Layer details

This section is where you add in the details for your layers. Select **Add new layer**, you will be prompted to pick a layer source from the list. Fill in the details:

- Name
- Minimum viewable zoom level (optional) - the minimum zoom this layer will be turned on for, for example if set to 12, the layer will turn off once you zoom out past level 12
- Maximum viewable zoom level (optional) - the maximum zoom this layer will be turned on for, for example if set to 15, the layer will turn off once you zoom in past level 15. Set to blank for no restriction
- Layer Z-Index - this is the 'layer order' on the map. Higher numbers will, by default, appear above lower numbers when both layers are turned on. For things like Aerial Photography, this should generally be set very low (such as -500). Leave blank for default of 0
- Info List Template - the template for what appears when you click multiple items and are presented with a list of features. See [Info Templates](../db/layers.md#info-templates) for more information
- Info Template - the template for what appears when you select a single map feature. See [Info Templates](../db/layers.md#info-templates) for more information
- Querayable - whether you want the layer to be queryable (clicking on a feature will display further information)
- Filterable - whether you want the layer to be filterable

You'll also see a button for *Advanced settings*, which are optional. You can change the default opacity and saturation here if you want to.

###Layer categories

This section is where you manage the categories that layers are organised into. Select **Create new category** and fill in the details:

- Name
- Description
- Order - the sort order you want your category to appear
- Parent category (optional) - select a parent category if the category you are creating is a child category

On the right side of the screen, you'll be able to select all the layers you want to appear in your category.

## Edit a layer

Select the section then layer you want to edit. Make the changes you want and hit Save.

## Delete a layer

Select the section then layer you want to delete. You will be asked if you're sure, press Delete again to confirm.