# System

## Cache

You can clear the cache in the System section. Click the big red button to clear the in memory cache for the application.

Most of the data is cached for varying amounts of time, to improve performance.


### Cached items

| Name                           | Key                                     | Cache length |
| ------------------------------ | --------------------------------------- | ------------ |
| Version Configuration by Slug  | VersionBySlug/{slug}                    | 10 minutes   |
| Version Configuration by ID    | Version/{id}                            | 10 minutes   |
| User Roles by User ID          | UserRole/{userId}                       | 2 minutes    |
| Web Layer Service Definitions  | WebLayerServiceDefinitions              | 10 minutes   |
| Proxy Allowed Hosts            | ProxyAllowedHosts                       | 12 hours     |
| Print Configuration by Version | PrintConfigurationByVersion/{versionId} | 10 minutes   |
| Search Definitions by Version  | SearchDefinitions/{versionId}           | 10 minutes   |
| API Search Definitions         | APISearchDefinitions                    | 1 hour       |
| Database Search Definitions    | DBSearchDefinitions                     | 1 hour       |
| Local Search Definitions       | LocalSearchDefinitions                  | 1 hour       |

## Web layer service definitions

Web layer service definitions detail pre-defined services that users can add layers from onto their map, and that Admins can choose to add layers from in the [Add Layer wizard](layers.md#add-a-new-layer-using-the-wizard). These services are defined just once for all versions.

### Add a new web layer service definition

Select **Manage web layer service definitions** then **Add new web layer service definition** and fill in the details:

- Name - a friendly name for the service shown to end users
- Description - a more detailed description for the service if you need one
- URL - the base URL for the service
- Type - the type of service. Currently only WMS is supported
- Version - the version of the service. Leave blank and it will use version 1.1.0
- Category - a category to group the list by. All services with the same category will be grouped in the select list presented to users
- Sort order - the order the service appears in the list. Services are first grouped by category, then ordered by this number
- Whether you want to enable proxy map requests - only tick this if the layer can't be used with [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)
- Whether you want to enable proxy metadata requests - only tick this if the layer can't be used with [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)
- Available to Admins only? - makes this service only visible to administrators on the map and in the [Add Layer wizard](layers.md#add-a-new-layer-using-the-wizard)

!!! warning
    Proxying requests can reduce performance and may even be blocked by the service provider. If in doubt, check with the service provider. 

### Edit a web layer service definition

Select the web layer service definition you want to edit. Make the changes you want and hit Save.

### Delete a web layer service definition

Select the web layer service definition you want to delete. You will be asked if you're sure, press Delete again to confirm.

## Site analytics and cookie control

You can configure from a number of supported analytics tools including the ability to enable associated cookie controls. 

### Add a new analytics tool

Select **Site analytics and cookie control** then **Add a new analytics tracker** and fill in the details:

- Select from the supported tool list
- Add the token or key provided by the supplier
- Select any associated cookie control (currently only Civica supported)
- Check the box if you wish to enable it right away
- Finally, select which versions you want to apply the tool to if required. 

!!! Note on versions
    If you don't select any versions the analytics tool will be applied to all of the versions. 

### Edit an analytics tool

Select the tool you wish to edit from the tool list by product name. Make the changes you want and hit Save.

### Delete an analytics tool

Select the **Remove** link on the right of the tool list. This will remove your analytics entry. 

## Projections

GIFramework Maps can use multiple projections for both the actual map rendering and the display coordinates. The Projections section lets you manage what projections are available.

### Register new projection

To add a new projection to the list of available projections, choose 'Register new projection'. See [Getting projection details](#getting-projection-details) below to find out how to get the information you need.

- `EPSG Code` - The EPSG code of the projection
- `Name` - The name of the projection
- `Description` - A description of what this projection is and where it covers
- `Proj4 or WKT Definition` - A Proj4 or WKT definition of the projection
- `Bottom Left X (Min X)` - The bottom left X coordinate of this projections maximum bounds, in Lat/Lon
- `Bottom Left Y (Min Y)` - The bottom left Y coordinate of this projections maximum bounds, in Lat/Lon
- `Top Right X (Max X)` - The top right X coordinate of this projections maximum bounds, in Lat/Lon
- `Top Right Y (Max Y)` - The top right Y coordinate of this projections maximum bounds, in Lat/Lon
- `Default display decimal places` - The number of decimal places shown by default when showing coordinates in this projection

### Edit a projection

Select the projection you want to edit from the list. Make the changes you want and hit Save.

!!! warning
    Be careful editing projections, as these can have a dramatic effect on the application

### Delete a projection

Select the projection you want to delete from the list. At the bottom, hit Delete and confirm your choice.

!!! danger
    Make sure your projection is not being used anywhere before deleting it

### Getting projection details

Projections are defined using the EPSG Code, Proj4Definition and bounds. You can get these using websites such as <a href="https://epsg.io">https://epsg.io</a> or <a href="https://epsg.org/">https://epsg.org/</a>. You can use a Proj4 or WKT style definition for the projection definition. You do not have to provide a definition for the [built-in projections](#built-in-projections).

### Built-in projections

The following projections are built-in, and do not require a Proj4 or WKT definition. 

- EPSG:3857 - Spherical Mercator
- EPSG:4326 - WGS84 Lat/Lon
- EPSG:4269 - NAD83 (North America)

You will still need to add the projection to the list to make it available to the application.