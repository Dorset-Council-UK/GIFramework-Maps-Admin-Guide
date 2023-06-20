# Analytics definitions

The `AnalyticsDefinitions` table contains details about supported analytics tools for adding analytics functionality to the site. The `VersionAnalytic` table specifies which versions to apply the analytics to (default is to be applied to all versions).

## Relevant tables

| Table Name                        | Description                          |
| --------------------------------- | ------------------------------------ |
| AnalyticsDefinitions				| Contains the pre-defined analytics providers |
| VersionAnalytic			        | Contains specified versions for using analytics |

### AnalyticsDefinitions

This table contains the details of each analytics provider that is available.

- `ProductName` - Name of the analytics provider
- `ProductKey` - They key or token to be used for the analytics provider
- `DateModified` - The date the analytics have been created or amended
- `Enabled` - Whether the analytics are switched on or not
- `CookieControl` - Defines which cookie control is used, currently only supports Civica

### VersionAnalytic

This table contains the details of which analytics should be used on specific versions..

- `VersionID` - The ID of the [version](../db/versions.md)
- `AnalyticsDefinitionID` - The ID of the analytics definition from the `AnalyticsDefinitions` table

!!! Note on versions
    If you don't specify any versions the analytics tool will be applied to all of the versions. 

