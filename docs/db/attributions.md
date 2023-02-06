# Attributions

All [layers](../db/layers.md) have an attribution, which appears at the bottom of the map and details basic copyright and licence information. We keep these in a database rather than relying on fetching metadata from the layer source for two main reasons:
- Speed - Retrieving individual attribution information from every layers GetCapabilities is dependent on the speed of the web server, so can be slow.
- Availability - From experience, many services simply do not provide attribution information in their GetCapabilities, or it is wrong. Some types of layer (such as XYZ layers) do not even have this capability.

## Relevant tables

| Table Name                        | Description                          |
| --------------------------------- | ------------------------------------ |
| Attribution                       | Contains the available attributions that can be applied to a layer |
| LayerSource                       | Contains the field `AttributionId` to indicate which attribution applies to this layer |

### Attribution

This table contains the attribution details. 

- `Name` - A friendly name for the attribution used by admins
- `AttributionHTML` - The HTML used to display the attribution. Can be written in plain text, but if you need links you'll need to use HTML for that. Use the placeholder `{{CURRENT_YEAR}}` to inject the current year into the string.

!!! example
    `© <a href="https://www.dorsetcouncil.gov.uk" target="blank">Dorset Council</a> {{CURRENT_YEAR}}.`

    Renders as

    © [Dorset Council](https://www.dorsetcouncil.gov.uk) 2023.

### LayerSource

Within the `LayerSource` table, there is an `AttributionId` column. Set this to the `Id` in the `Attribution` table of the relevant attribution.


