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