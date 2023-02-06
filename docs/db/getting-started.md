# Getting started with the database

!!! danger "Here be dragons"
    Making changes direct to the database without fully understanding the implications can result in GIFramework Maps being unusable. Be **very** careful

Most settings related to the day to day use of GIFramework Maps is held in the database. You can directly edit these values if the administration interface is not working or you need to do things in bulk. You'll need to be logged in to the database as a user with create and edit permission.

## Understanding what the tables do

There are a number of tables in the database that manage different parts of the application. Below is a list of all the tables and their primary purpose. You should look up the related documentation for each feature to understand exactly how the tables work.

| Table Name                        | Description                          | Detailed documentation |
| --------------------------------- | ------------------------------------ | ---------------------- |
| ApplicationRoles                  | Contains all the available Roles users can have. **This should not be edited as it is tied directly to the application code** | [Administrative roles](../db/admin-roles.md) |
| ApplicationUserRoles              | Mapping between user identifiers and the roles they have | [Administrative roles](../db/admin-roles.md) |
| Attribution                       | Contains the available attributions that can be applied to a layer | [Attributions](../db/attributions.md) |
| Basemap                           | Basic details about available basemaps  | [Basemaps](../db/basemaps.md) |
| Bound                             | Geographic bounding box definitions that can be applied to layers or used as starting bounds in versions | [Bounds](../db/bounds.md) |
| Category                          | Basic details about categories that layers can be sorted into | [Categories](../db/categories.md) |
| CategoryLayer                     | Mapping between layers and teh categories they are added to | [Categories](../db/categories.md) |
| Layer                             | Basic details about a published layer and how it can be used | [Layers](../db/layers.md) |
| LayerSource                       | Basic details about the source of a layer, including the type (TileWMS, XYZ etc.) and its attribution  | [Layers](../db/layers.md) |
| LayerSourceOption                 | Contains the details about where a layer comes from and the options that will be applied to it | [Layers](../db/layers.md) |
| LayerSourceType                   | Lookup list describing the types of layers available. **This should not be edited as it is tied directly to the application code** |  [Layers](../db/layers.md) |
| PrintConfigurations               | Contains the configurations for prints that can be applied to a version | [Print configuration](../db/print-config.md) |
| ProxyAllowedHosts                 | Contains a list of allowed hosts that can use the proxy capabilities. Anything not in this list will be rejected by the proxy  | [Proxy](../db/proxy.md) |
| SearchDefinitions                 | Contains details of the searches that can be used in versions | [Search definitions](../db/search-definitions.md) |
| Theme                             | Basic theme information that can be applied to versions, including logos and colours | [Theming](../db/theming.md) |
| TourDetails                       | Basic details about available tours that can be applied to versions, including frequency and update dates | [Tours](../db/tours.md) |
| TourStep                          | Contains the individual steps of a tour | [Tours](../db/tours.md) |
| VersionBasemap                    | Mapping between basemaps and versions, showing which basemaps are available in which version | [Versions](../db/versions.md) |
| VersionCategory                   | Mapping between categories and versions, showing which categories are available in which version | [Versions](../db/versions.md) |
| VersionPrintConfiguration         | Mapping between print configurations and versions, showing which print configurations are available in which version | [Versions](../db/versions.md) |
| VersionSearchDefinition           | Mapping between search definitions and versions, showing which search definitions are available in which version | [Versions](../db/versions.md) |
| VersionUser                       | Mapping between user identifiers and versions, showing which users have access to which login required versions | [Versions](../db/versions.md) |
| Version                           | Contains the basic details about a version, including name, slug, start bound, theme and more | [Versions](../db/versions.md) |
| WebLayerServiceDefinitions        | Contains all the pre-defined external web services that can be used to add additional layers to the map. Applied globally | [Web Service definitions](../db/web-service-definitions.md) |
| WelcomeMessages                   | Contains the welcome message definitions that can be applied to a version | [Welcome messages](../db/welcome-messages.md) |
| __EfMigrationsHistory             | A table used by the application to keep track of the current state of the database. **This should not be edited as it is tied directly to the application code** | N/A |