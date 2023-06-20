# Analytics definitions

The `AnalyticsDefinitions` table contains details about supported analytics tools for adding analytics functionality to the site.

## Relevant tables

| Table Name                        | Description                          |
| --------------------------------- | ------------------------------------ |
| AnalyticsDefinitions         | Contains the pre-defined analytics providers |

### AnalyticsDefinitions

This table contains the details of each analytics provider that is available.

- `ProductName` - Name of the analytics provider
- `ProductKey` - They key or token to be used for the analytics provider
- `DateModified` - The date the analytics have been created or amended
- `Enabled` - Whether the analytics are switched on or not
- `CookieControl` - Defines which cookie control is used, currently only supports Civica
