# Layers

Layers are the bedrock of GIFramework Maps. Without layers, your maps are basically useless.

Layers are pretty configurable, and have lots of various options, some of which are quite complex to set properly. For this reason, you should consider using the management interface if you can.

## Relevant tables

| Table Name                        | Description                          |
| --------------------------------- | ------------------------------------ |
| Layer                             | Basic details about a published layer and how it can be used |
| LayerSource                       | Basic details about the source of a layer, including the type (TileWMS, XYZ etc.) and its attribution  |
| LayerSourceOption                 | Contains the details about where a layer comes from and the options that will be applied to it |
| LayerSourceType                   | Lookup list describing the types of layers available. **This should not be edited as it is tied directly to the application code** |  
| CategoryLayer                     | Mapping between layers and the categories they are added to |

## Adding a layer

Layers have two main parts to them, the Layer, and the Layer Source. When you add a layer, the first thing you do is define the Layer Source.

### LayerSource

The `LayerSource` table contains very basic information about the layer.

- `Name` - A friendly name for administrators.
- `Description` - A basic description of the layer. This is shown to end users when the layer has no other description metadata available from source (see more about layer metadata below)
- `LayerSourceTypeId` - The `Id` of the type of layer from the `LayerSourceType` table. This identifies the type of layer source this is. See [LayerSourceType](#layersourcetype) details below for more information.
- `AttributionId` - The `Id` of the relevant `Attribution` that will be applied to this layer. Learn more about attributions in the [attributions documentation](../db/attributions.md)

### LayerSourceOption

The `LayerSourceOption` table contains the majority of the technical information required to show a layer. It is a one-to-many table, so one `LayerSource` can have many linked `LayerSourceOption`s, depending on the requirements of the layer. It is a simple key/value store with the following columns:

- `Name` - This is the key, and should be set to one of the following understood values:
    - `url`
    - `params`
    - `cswendpoint`
    - `projection`
    - `tilegrid`
- `Value` - This is the value. See below for details on what this should contain
- `LayerSourceId` - The `Id` of the relevant `LayerSource` that this option applies to

#### XYZ Layers
The only required option required for XYZ layers is `url`. This should be set to the URL endpoint for the service, with templates for the X, Y and Z portions. The provider normally provides this for you.

!!! example
    https://api.os.uk/maps/raster/v1/zxy/layer/{z}/{x}/{y}.png

This assumes the layer is provided in the standard Spherical Mercator EPSG:3857 projection. If the service is providing tiles in a different projection, see the [advanced configuration](#xyz-reprojection) section below.

#### WMS layers

For WMS layers (TileWMS or ImageWMS), you need a minimum of `url` and `params` set.

`url`

This should be set to the 'base' url of the WMS service. This is normally provided to you by the service, and will look something like `https://<service-url>/wms`

`params`

This is a JSON object of additional parameters that are applied to the layer.

The `params` object should at a minimum contain the following

```
{
    "LAYERS": "LAYERNAME", 
    "FORMAT": "image/png", /*replace with required format*/
    "TILED":"true"
}
```

These parameters will be used by OpenLayers to make appropriate requests to the service. Additional parameters as required by the service can be added be appending them onto the JSON object.

Common additional parameters you may want to use include:

- `CQL_FILTER` - Will apply a CQL filter to the layer
- `STYLES` - Will set the style of the layer to a specific style available to the server
- `AUTHKEY` - If the service uses AUTHKEY authentication (or any other type of key based authentication)

!!! warning
    Incorrectly formatting this JSON object can result in the layer or the entire map failing to load correctly. Edit with caution.

#### Other options

- `projection` - If the projection is anything other than EPSG:3857, set it here. For WMS based layers, this is enough. For XYZ layers, see the section on [XYZ reprojection](#xyz-reprojection)
- `cswendpoint` - An endpoint to retrieve a CSW Metadata document, describing the layer. The metadata document should use Dublin Core and will be available via the 'i' button next to the layer name in the layer control.

### LayerSourceType

There are currently 3 supported layer types in GIFramework Maps. More may be added in the future.

#### XYZ
The XYZ source is used for tile data that is accessed through URLs that include a zoom level and tile grid x/y coordinates. Examples include OpenStreetMap and OpenCycleMap.

#### TileWMS
The TileWMS source is used for WMS layers that are provided 'tiled', normally in 256px squares.

This is normally the best option, as it is more efficient and quicker, and can be cached by the users browser, but it can sometimes have issues with labels, or some services might not provide it. In these cases, use ImageWMS.

#### ImageWMS
The ImageWMS source is used for WMS layers that are provided 'untiled', so a single image is returned for the entire map screen. Normally you would choose TileWMS when available, but ImageWMS is particularly good if you have labels, or, if the layer is very complex, a single tile can load quicker than many smaller tiles.

### CategoryLayer

The `CategoryLayer` table defines which layers are available in which categories.

- `LayerId` - The `Id` from the `Layer` table
- `CategoryId` - The `Id` from the `Category` table
- `SortOrder` - The position this layer should appear within this category

## Advanced configuration

### XYZ reprojection

XYZ layers can be provided in different projections. To make use of on the fly reprojection, you need to provide an appropriate `tilegrid` option, describing the resolutions and origins of the XYZ layer. The service provider should be able to provide this.

!!! example
    The `tilegrid' for British National Grid EPSG:27700 is
    ```
    {
        "resolutions": [896.0, 448.0, 224.0, 112.0, 56.0, 28.0, 14.0, 7.0, 3.5, 1.75],
        "origin": [-238375.0, 1376256.0]
    }
    ```