# Search definitions

Search definitions define what searches are available in the search bar and how they work.

## Add a new search definition

There are three different types of search definition: API search definitions, database search definitions and local search definitions.

To add a new search definition, select the **Add new** button for the type you want to add. All three search definitions will ask you for the following details:

- Name - a friendly name for administrators
- Title - the name that will appear in the search results list
- Attribution HTML - optional HTML to add to the bottom of the search results as an attribution
- Maximum number of results to return
- Zoom level you want the map to zoom to (optional)
- ESPG - the EPSG code of the geometry returned
- Regex validation (leave this blank for no validation) - an optional Regular Expression to validate the search query against. If a search query doesn't match the regualr expression, it won't even be attempted
- Supress geometry - ticking this prevents a pin, line or polygon from being drawn on the map when a user clicks on a search result

### API search definitions

If you're creating an API search definition, you will also be asked to fill in the following details:

- URL template -  the full URL to do the search, with the placeholder {{search}} where the search query would go
- Title field path - a JSONPath expression to an appropriate 'Title' field, used for displaying the search result

Plus one of the following:

- X and Y field paths -  a JSONPath expression to an appropriate 'X' or 'Y' field in the JSON
- Geometry path - a JSONPath expression to appopriate 'Geometry' field. The geometry must be valid GeoJSON
- Bounding rectangle fields - a JSONPath expression to a minimum bounding rectangle field

### Database search definitions

If you're creating a database search definition, you will also be asked to fill in the following details:

- Table name - the fully qualified name of the table to query
- X field - the name of an appropriate 'X' column in the table
- Y field - the name of an appropriate 'Y' column in the table
- Geometry field - the name of an appopriate GeoJSON geometry column in the table. You may need to use a database function to convert the geometry to GeoJSON
- Title field - the name of an appropriate 'Title' field, used for displaying the search result
- SQL WHERE clause - the WHERE clause used to do the actual search, with the placeholder {{search}} where the search query would go
- SQL ORDER BY clause (optional)

### Local search definitions

Local search definitions are a bit different. They are hard-coded into the application, so if you enter one of these you need to know what you are doing.

- Local search name - the hard-coded name in the application

## Edit a search definition

Select the search definition you want to edit. Make the changes you want and hit Save.

## Delete a search definition

Select the search definition you want to delete. You will be asked if you're sure, press Delete again to confirm.
