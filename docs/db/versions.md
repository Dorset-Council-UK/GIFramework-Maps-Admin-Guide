# Versions

Versions are the best way to split maps up into different themes, with different layers, permissions and functionality.

The `Versions` table contains all the basic information about a version of GIFramework Maps. 

## Relevant tables

| Table Name                          | Description                          |
| ----------------------------------- | ------------------------------------ |
| Versions                            | Contains the basic details about a version, including name, slug, start bound, theme and more |
| VersionBasemaps                     | Contains an optional `BoundId` column used to define what bounds the layer covers |
| VersionCategory                     | Contains a `BoundId` column used to define what bounds the basemap covers |
| VersionPrintConfiguration           | Contains a `BoundId` column used to define what bounds the basemap covers |
| VersionSearchDefinition             | Contains a `BoundId` column used to define what bounds the basemap covers |
| VersionUser                         | Contains a `BoundId` column used to define what bounds the basemap covers |

### Versions

- `Name` - The name of the version. This also appears to the user in the top left
- `Description` - A friendly description of the version. This also appears in the HTML meta description which is shown to search engines
- `Slug` - The `Slug` is the bit on the end of the URL. You can have up to 3 parts to a slug, seperated by slashes. See section below on [slugs](#slugs) for more info
- `Enabled` - A boolean indicating whether this version is enabled or not. Disabled versions will show a specific 'Disabled' message, rather than the stanard 'Not found'
- `RequireLogin` - A boolean indicating whether this version requires the user to login or not. Permissions need to be given to users using the [`VersionUser`](#versionuser) table.
- `RedirectionURL` - An optional URL to redirect the user to instead of loading the version. Can be useful if a version changes slug, or you want to point people elsewhere. Will issue a `HTTP 302 Found` response with the URL provided
- `BoundId` - The `Id` of a `Bound` to use as the start extent for this version
- `ThemeId` - The `Id` of the `Theme` to use in this version
- `HelpURL` - An optional URL to help documentation. A link will be put in the header of GIFramework Maps and in various other places if this URL is filled in. If left blank, no help link will be generated.
- `WelcomeMessageId` - The `Id` of the `WelcomeMessage` to use in this version. Leave blank for no welcome message.
- `FeedbackURL` - An optional URL to a feedback form. A link will be put in the header of GIFramework Maps if this URL is filled in. If left blank, no feedback link will be generated.
- `TourDetailsId` - The `Id` of a `TourDetails` to use in this version. Leave blank for no tour.
- `ShowLogin` - A boolean indicating whether to show a login button on the version. If a user is already logged in, the account box will still always show, regardless of this setting

#### Slugs

Slugs are the bit on the end of your application URL which direct you to different versions of GIFramework Maps. You can have a maximum of three slugs seperated by forward slashes. 

By default, there should be one called 'general' which is where you will be directed if you have no slug on your URL.

!!! danger "Reserved slugs"
    There are a number of slugs that are reserved for use by the GIFramework Maps application. Using these will not work and may cause other unintended consequences. 
    
    - `general`
    - `account`
    - `api`
    - `print`
    - `search`
    - `broadcasthub`
    - `css`
    - `img`
    - `lib`

    You should not use these as the first part of the slug, regardless of any additional parts you put on the end, e.g. `lib/myversion` is **not** valid



!!! example "Examples"
    'general' -> Root of application e.g. `https://<your-application-root>/`

    'highways' -> `https://<your-application-root>/highways`

    'very/long/slug' -> `https://<your-application-root>/very/long/slug`


    

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

### VersionPrintConfiguration

The `VersionPrintConfiguration` table defines which print configurations are used in which versions.

- `VersionId` - The `Id` from the `Versions` table
- `PrintConfigurationId` - The `Id` from the `PrintConfigurations` table

!!! note
    If a specific configuration is not set for a version, it will fall back to that defined for the 'general' version

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