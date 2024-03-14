# Versions

Versions are the best way to split maps up into different themes, with different layers, permissions and functionality.

The `Versions` table contains all the basic information about a version of GIFramework Maps. 

## Relevant tables

| Table Name                          | Description                          |
| ----------------------------------- | ------------------------------------ |
| Versions                            | Contains the basic details about a version, including name, slug, start bound, theme and more |
| VersionAnalytic                     | Identifies which analytics providers are enabled for a version |
| VersionBasemaps                     | Contains details of the basemaps that a version has available and their default options |
| VersionCategory                     | Contains a list of layer categories that a version has |
| VersionContact                      | Lists the users that should be contacted regarding a version |
| VersionLayer                        | Contains per-layer customisations applied to a version |
| VersionPrintConfiguration           | Identifies which print configuration a version uses |
| VersionProjections                  | Lists the projections available to a version and what the defaults are |
| VersionSearchDefinition             | Lists the search definitions that are enabled in a version and their default settings |
| VersionUser                         | Contains the users that have access to a version |

### Versions

- `Name` - The name of the version. This also appears to the user in the top left
- `Description` - A friendly description of the version. This also appears in the HTML meta description which is shown to search engines
- `Slug` - The `Slug` is the bit on the end of the URL. You can have up to 3 parts to a slug, seperated by slashes. See [slugs](../gui/versions.md#slugs) for more info
- `Enabled` - A boolean indicating whether this version is enabled or not. Disabled versions will show a specific 'Disabled' message, rather than the standard 'Not found'
- `RequireLogin` - A boolean indicating whether this version requires the user to login or not. Permissions need to be given to users using the [`VersionUser`](#versionuser) table.
- `RedirectionURL` - An optional URL to redirect the user to instead of loading the version. Can be useful if a version changes slug, or you want to point people elsewhere. Will issue a `HTTP 302 Found` response with the URL provided
- `BoundId` - The `Id` of a `Bound` to use as the start extent for this version
- `ThemeId` - The `Id` of the `Theme` to use in this version
- `HelpURL` - An optional URL to help documentation. A link will be put in the header of GIFramework Maps and in various other places if this URL is filled in. If left blank, no help link will be generated.
- `WelcomeMessageId` - The `Id` of the `WelcomeMessage` to use in this version. Leave blank for no welcome message.
- `FeedbackURL` - An optional URL to a feedback form. A link will be put in the header of GIFramework Maps if this URL is filled in. If left blank, no feedback link will be generated.
- `TourDetailsId` - The `Id` of a `TourDetails` to use in this version. Leave blank for no tour.
- `ShowLogin` - A boolean indicating whether to show a login button on the version. If a user is already logged in, the account box will still always show, regardless of this setting
- `VersionNotes` - An optional description of the version shown to administrators

### VersionAnalytic
The `VersionAnalytic` table defines which analytics providers are available in which versions.

- `VersionId` - The `Id` from the `Versions` table
- `AnalyticsDefinitionId` - The `Id` from the `AnalyticsDefinition` table

### VersionBasemaps

The `VersionBasemap` table defines which basemaps are available in which versions.

- `VersionId` - The `Id` from the `Versions` table
- `BasemapId` - The `Id` from the `Basemap` table
- `IsDefault` - Boolean indicating whether this basemap is the default one for that version
- `DefaultOpacity` - The default opacity (or transparency) of the basemap between 0 (invisible) and 100 (opaque). Leave blank for default of 100
- `DefaultSaturation` - The default saturation of the basemap between 0 (greyscale) and 100 (full colour). Leave blank for default of 100
- `SortOrder` - The position the basemap will appear in the basemaps panel

### VersionCategory

The `VersionCategory` table defines which categories are available in which versions.

- `VersionId` - The `Id` from the `Versions` table
- `CategoryId` - The `Id` from the `Category` table

!!! bug
    If you want this category to appear in many versions, but in different orders, you will need to make different categories, as the ordering cannot be set by version

!!! info
    If your category is a child, both the parent AND child categories need to be added to this table.

### VersionContact
The `VersionContact` table defines which users should be contacted about a version.

- `VersionContactId` - Unique ID for this entry
- `VersionId` - The `Id` from the `Versions` table
- `UserId` - The users unique identifier provided by the identity provider
- `DisplayName` - The users display name
- `Enabled` - Whether they should be included in the email drafting list

### VersionLayer
The `VersionLayer` table contains any per-layer customisations that have been applied to this version.

- `VersionId` - The `Id` from the `Versions` table
- `LayerId` - The `Id` from the `Layer` table
- `CategoryId` - The `Id` from the `Category` table
- `IsDefault` - Whether this layer is turned on by default or not
- `DefaultOpacity` - The default opacity of the layer
- `DefaultSaturation` - The default saturation of the layer
- `SortOrder` - The position this layer appears within its category
- `MaxZoom` - The maximum viewable zoom level of the layer
- `MinZoom` - The minimum viewable zoom level of the layer
- `Id` - Unique autogenerated ID for this customisation

### VersionPrintConfiguration

The `VersionPrintConfiguration` table defines which print configurations are used in which versions.

- `VersionId` - The `Id` from the `Versions` table
- `PrintConfigurationId` - The `Id` from the `PrintConfigurations` table

!!! note
    If a specific configuration is not set for a version, it will fall back to that defined for the 'general' version

### VersionProjection

The `VersionProjection` table defines which projection the map renders in and what projections are available for viewing.

- `VersionId` - The `Id` from the `Versions` table
- `ProjectionId` - The `Id` from the `Projections` table
- `IsDefaultMapProjection` - Whether this projection is the one used for map rendering
- `IsDefaultViewProjection` - Whether this projection is the default one set as the display coordinates

### VersionSearchDefinition

The `VersionSearchDefinition` table defines which searches are available in which versions.

- `VersionId` - The `Id` from the `Versions` table
- `SearchDefinitionId` - The `Id` from the `SearchDefinition` table
- `Enabled` - A boolean indicating whether this search is enabled by default (users can override this in the search options dialog)
- `Order` - The order in which the search results are searched. Particularly important if the `StopIfFound` boolean is used
- `StopIfFound` - Determines whether the further searches are conducted if a result has been found with this search

!!! example
    When you do a search, GIFramework Maps starts from the top of the list (sorted by the `Order` column) and works its way down until it finds a result. When it does, if the `StopIfFound` boolean is set to true, GIFramework Maps will not continue with any of the other searches. This prevents users from getting lots of potentially irrelevant results when a more relevant result has already been found. 

!!! note
    If a specific search definition configuration is not found for a version, it will fall back to using search definitions defined for the 'general' version

### VersionUser

The `VersionUser` table defines which individual users are allowed to access which versions. This only applies to versions with `RequireLogin` set to true.

To give a user acess to a version, simply provide their user identifier and the ID from the `Versions` table.

!!! hint
    You can get a user's identifier (or your own) by getting them to go to `https://<your-application-root>/account/diagnostics` and looking up the `nameidentifier` value.
