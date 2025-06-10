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
| LayerDisclaimers                  | List of disclaimers that can be added to a layer |

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

#### Vector layers

For vector layers, you will need a minimum of the `url` option. Additionally, unless you want the default OpenLayers styles, you will need a `style` option as well. See [Styling vector layers](../gui/layers.md#styling-vector-layers) for more information.

Additional options include:
- `typename` - When using a WFS service, you should set the `url` to the base server URL, and the `typename` as the layer name you are requesting
- `format` - The format the data is in. Defaults to 'application/json' unless specified.
- `loadingstrategy` - Can be `bbox` or `all`. This defines how the vector layer is loaded, either with a bbox strategy (loading just a bounding box worth of data at a time) or loading everything at once. In reality, WFS based layers will default to `bbox` unless specifically set to `all`, and non-WFS layers will default to `all`

!!! info "Supported vector formats"
    - JSON (`application/json`, `text/json`, `geojson` or `json`)
    - GML3 (`text/xml; subtype=gml/3.1.1`, `gml3`)
    - GML2 (`text/xml; subtype=gml/2.1.2`, `gml2`)
    - KML (`application/vnd.google-earth.kml xml`, `application/vnd.google-earth.kml+xml`, `kml`)

!!! warning "Limitation"
    Vectors cannot have a filter pre-applied to them.

#### Other options

- `projection` - If the layer is only available in a projection that is not the same as the map you are putting it in to, set the projection here, otherwise you can not include it, and the layer will be requested in the projection of the map. For XYZ layers, see the section on [XYZ reprojection](#xyz-reprojection)

### Layer

A layer first requires a [layer source](#layersource) to be created that defines where the layer comes from.

Once this has been created, the layer table has the following fields to fill in:

- `Name` - The friendly name that will appear in the layer control
- `LayerSourceId` - The `Id` from the `LayerSource` table
- `BoundId` - An optional `Id` from the [`Bound`](../db/bounds.md) table that defines what the max extent of this layer is. Setting this prevents GIFramework Maps from requesting tiles or doing feature requests outside of the set bounds. This improves performance and efficiency, but is not required. Leave blank for no restriction
- `MaxZoom` - The maximum zoom this layer will be turned on for, for example if set to 15, the layer will turn off once you zoom in past level 15. Set to blank for no restriction
- `MinZoom` - As above, but the other way round, for example if set to 12, the layer will turn off once you zoom out past level 12
- `ZIndex` - This is the 'layer order' on the map. Higher numbers will, by default, appear above lower numbers when both layers are turned on. For things like Aerial Photography, this should generally be set very low (such as -500). Leave blank for default of 0
- `DefaultOpacity` - The default opacity (or transparency) of the layer between 0 (invisible) and 100 (opaque). Leave blank for default of 100
- `DefaultSaturation` - The default saturation of the layer between 0 (greyscale) and 100 (full colour). Leave blank for default of 100
- `InfoTemplate` - The template for what appears when you select a single map feature.. See [Info Templates](#info-templates) below for more information
- `InfoListTitleTemplate` - The template for what appears when you click multiple items and are presented with a list of features. See [Info Templates](#info-templates) below for more information
- `Queryable` - A Boolean indicating whether the user is allowed to query (info click) this layer
- `DefaultFilterEditable` - A Boolean indicating if the user is allowed to edit any filters already applied to the layer in the layer source
- `Filterable` - A Boolean indicating if the user is allowed to apply filters to this layer
- `ProxyMapRequests` - A Boolean indicating if all GetMap requests should be proxied via the [application proxy](../db/proxy.md). Only use this if a remote layer can't handle CORS requests (errors will appear in the console and layer control when using this layer if this is the case). See [Proxying](../db/proxy.md) for more details
- `ProxyMetaRequests` - As above, but related to all metadata and query requests, such as `GetCapabilities` and `GetFeatureInfo`. See [Proxying](../db/proxy.md) for more details
- `LayerDisclaimerId` - An optional `Id` from the [`Layer Disclaimers`](#layer-disclaimers) table that defines which disclaimer to show for this layer. Leave blank for no disclaimer
- `RefreshInterval` - Optional. How often this layer should automatically refresh with new data from the server, in seconds.

#### Info Templates

See ['Creating info templates'](../gui/layers.md#info-templates)

### CategoryLayer

The `CategoryLayer` table defines which layers are available in which categories.

- `LayerId` - The `Id` from the `Layer` table
- `CategoryId` - The `Id` from the `Category` table
- `SortOrder` - The position this layer should appear within this category

### LayerSourceType

There are currently 7 supported layer types in GIFramework Maps. More may be added in the future.

#### XYZ
The XYZ source is used for tile data that is accessed through URLs that include a zoom level and tile grid x/y coordinates. Examples include OpenStreetMap and OpenCycleMap.

#### TileWMS
The TileWMS source is used for WMS layers that are provided 'tiled', normally in 256px squares.

This is normally the best option, as it is more efficient and quicker, and can be cached by the users browser, but it can sometimes have issues with labels, or some services might not provide it. In these cases, use ImageWMS.

#### ImageWMS
The ImageWMS source is used for WMS layers that are provided 'untiled', so a single image is returned for the entire map screen. Normally you would choose TileWMS when available, but ImageWMS is particularly good if you have labels, or, if the layer is very complex, a single tile can load quicker than many smaller tiles.

#### Vector
The Vector source is used for WFS layers or file based layers (such as a KML or GeoJSON file at a specific URL). Currently, GIFramework Maps can handle GML2, GML3, GeoJSON, JSON and KML formats as a vector source. This source type uses standard vector rendering, so is very precise and can handle things like rotating labels, but because of this it is not suitable for large datasets or those with complex geometries.

#### VectorImage
The VectorImage source is fundamentally the same as the Vector source, but can handle larger datasets and geometries slightly better, by rendering the vector as an image on the client. This does mean some sharpness is occasionally lost, and things like labels don't rotate, but its much less 'laggy' when moving the map around with large or complex datasets.

#### VectorTile
The VectorTile source is used to render VectorTiles, a common format for things like basemaps which splits vectors up into tiles and delivers them efficiently to the browser ([learn more](https://en.wikipedia.org/wiki/Vector_tiles)). MVT (Mapbox Vector Tiles) is the most common standard for this.

#### OGC VectorTile
The OGC VectorTile format is the new OGC standard for VectorTiles. It works in a similar way to VectorTiles, but is the standard promoted by the Open Geospatial Consortium. 

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

## Layer Disclaimers

You can add popup disclaimers to your layers that show when a user turns on a layer. The first step is to add a new disclaimer with the details you need.

- `Name` - A friendly name for administrators
- `Disclaimer` - The disclaimer to show. This can be plain text or HTML
- `Frequency` - A number indicating how often to show the disclaimer. Available options are:
    - `-1` - Indicates that the disclaimer should only be shown once, and never again
    - `0` - Indicates that the disclaimer should be shown once per browsing session. Refreshes do not count as a new session, but new tabs do. This prevents users from constantly being bombarded with the message every time they turn the layer on/off
    - `Any positive number` - Indicates the number of days to leave between showing the disclaimer again.
- `Dismiss Text` - Optional text to show on the dismiss button. Defaults to 'Close' if you leave it blank
