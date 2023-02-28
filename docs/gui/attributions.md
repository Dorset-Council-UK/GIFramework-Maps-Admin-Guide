# Attributions

All [layers](../gui/layers.md) have an attribution, which appears at the bottom of the map and details basic copyright and licence information. We keep these in a database rather than relying on fetching metadata from the layer source for two main reasons:

- Speed - retrieving individual attribution information from every layer is dependent on the speed of the web server, so can be slow
- Availability - from experience, many services simply do not provide attribution information or it is wrong. Some types of layer (such as XYZ layers) do not even have this capability

## Add a new attribution

Select the **Add new attribution** button and fill in the details:

- Name - a friendly name for the attribution used by admins
- Attribution HTML - the HTML used to display the attribution. Can be written in plain text, but if you need links you'll need to use HTML for that. Use the placeholder `{{CURRENT_YEAR}}` to inject the current year into the string

!!! example
    `Copyright <a href="https://www.dorsetcouncil.gov.uk" target="blank">Dorset Council</a> {{CURRENT_YEAR}}.`

    Renders as 
    
    Copyright [Dorset Council](https://www.dorsetcouncil.gov.uk) 2023.

## Edit an attribution

Select the attribution you want to edit. Make the changes you want and hit Save.

## Delete an attribution

Select the attribution you want to delete. You will be asked if you're sure, press Delete again to confirm.