# Web service definitions

The `WebLayerServiceDefinition` table contains details about pre defined services that users can add layers from onto their map. These services are defined just once for all versions.

## Relevant tables

| Table Name                        | Description                          |
| --------------------------------- | ------------------------------------ |
| WebLayerServiceDefinition         | Contains all the pre-defined external web services that can be used to add additional layers to the map. Applied globally |

### WebLayerServiceDefinition

This table contains the details of each web service that is available to users.

- `Name` - A friendly name for the service shown to end users
- `Description` - A more detailed description for the service
- `Url` - The base URL for the service
- `Type` - The type of service. Currently only `WMS` is supported
- `Version` - The version of the service. Leave blank and it will use version 1.1.0
- `Category` - A category to group the list by. All services with the same category will be grouped in the select list presented to users
- `SortOrder` - The order the service appears in the list. Services are first grouped by category, then ordered
- `ProxyMapRequests` - A boolean indicating whether all `GetMap` requests for layers added by this service will be proxied by the [application proxy](../db/proxy.md)
- `ProxyMetaRequests` - A boolean indicating whether all metadata and feature requests for this service will be proxied by the [application proxy](../db/proxy.md)

!!! warning
    Proxying requests can reduce performance and may even be blocked by the service provider. If in doubt, check with the service provider. 

!!! info
    Proxied `GetMap` requests are automatically switched to use a 'Single Tile' methodolgy, to improve performance. This may be changed in future versions.