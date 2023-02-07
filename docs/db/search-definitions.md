# Search Definitions

Search definitions define what searches are available in the search bar and how they work.

## Relevant tables

| Table Name                        | Description                          |
| --------------------------------- | ------------------------------------ |
| SearchDefinitions                 | Contains details of the searches that can be used in versions |
| VersionSearchDefinition           | Mapping between search definitions and versions, showing which search definitions are available in which version |

### SearchDefinitions

This table contains all the details about the available search definitions.

The first block of columns is the basic details.

- `Name` - A friendly name for administrators
- `Title` - The name that will appear in the search results list
- `AttributionHtml` - Optional HTML to add to the bottom of the search results as an attribution
- `MaxResults` - The maximum number of results to return from the service
- `ZoomLevel` - The zoom level to zoom to when a user clicks a search result. Optional if a geometry path, column or minimum bounding rectangle is defined
- `EPSG` - The EPSG code of the geometry returned
- `ValidationRegex` - An optional Regular Expression to validate the search qurey against. If a search query doesn't match the regualr expression, it won't even be attempted. Leave blank for no validation
- `SupressGeom` - A boolean indicating if the returned geometry should be supressed or not. This prevents a pin, line or polygon from being drawn on the map when a user clicks on a search result

The next block of columns are filled in depending on the `Discriminator' column. These are different depending on the type of search definition you are creating.

- `Discriminator` - Defines the type of search definition this is. There are 3 possible options:
    - `APISearchDefinition` - Defines a search that calls a remote web API
    - `DatabaseSearchDefinition` - Defines a search that uses a locally accessible database table
    - `LocalSearchDefinition` - Definies a search that is built in to the application itself.

#### APISearchDefinition

If you choose `APISearchDefinition`, the following columns are relevant:

!!! note
    Only `GET` requests that return JSON are currently supported for API calls

- `URLTemplate` - The full URL to do the search, with the placeholder {{search}} where the search query would go
- `XFieldPath` - A JSONPath expression to an appropriate 'X' field in the JSON. Optional if you use `GeomFieldPath` or the `MBRPath...` columns.
- `YFieldPath` - A JSONPath expression to an appropriate 'Y' field in the JSON. Optional if you use `GeomFieldPath` or the `MBRPath...` columns.
- `TitleFieldPath` - A JSONPath expression to an appropriate 'Title' field, used for displaying the search result.
- `GeomFieldPath` - A JSONPath expression to appopriate 'Geometry' field. The geometry must be valid GeoJSON. Optional if you use `XFieldPath`/`YFieldPath` or the `MBRPath...` columns.
- `MBRXMinPath` - A JSONPath expression to an appropriate bottom left X coordinate minimum bounding rectangle field. Optional if you use `XFieldPath`/`YFieldPath` or`GeomFieldPath`. 
- `MBRXMaxPath` - A JSONPath expression to an appropriate top right X coordinate minimum bounding rectangle field. Optional if you use `XFieldPath`/`YFieldPath` or`GeomFieldPath`. 
- `MBRYMinPath` - A JSONPath expression to an appropriate bottom left Y coordinate minimum bounding rectangle field. Optional if you use `XFieldPath`/`YFieldPath` or`GeomFieldPath`. 
- `MBRYMaxPath` - A JSONPath expression to an appropriate top right Y coordinate minimum bounding rectangle field. Optional if you use `XFieldPath`/`YFieldPath` or`GeomFieldPath`. 

!!! info
    `JSONPath` is a query language for JSON, similar to XPath for XML. It allows you to select and extract data from a JSON document. You can use tools such as [JSON Path Finder](https://jsonpathfinder.com/) or [JSONPath Online Evaluator](https://jsonpath.com/) to build JSONPath expressions.

#### DatabaseSearchDefinition

If you choose `DatabaseSearchDefinition , the following columns are relevant:

- `TableName` - The fully qualified name of the table to query
- `XField` - The name of an appropriate 'X' column in the table
- `YField` - The name of an appropriate 'Y' column in the table
- `GeomField` - The name of an appopriate GeoJSON geometry column in the table. You may need to use a database function to convert the geometry to GeoJSON, such as Postgres' `ST_AsGeoJson(geom)`
- `TitleField` - The name of an appropriate 'Title' field, used for displaying the search result.
- `WhereClause` - The `WHERE` clause used to do the actual search, with the placeholder {{search}} where the search query would go
- `OrderByClause` - An optional `ORDER BY` to append to the query

!!! note
    The same user that is used to access the GIFramework Maps database must be able to access the tables you use in these search definitions. You may want to consider using foreign tables to avoid duplicating data

#### LocalSearchDefinition

`LocalSearchDefinition`s are a little different. These refer to searches that are in-built to the application, and have specific names. The only relevant column is `LocalSearchName`, which refers to the hard-coded name in the application. The following in-built searches are available:

- `BNG12Figure` - Searches for 12 Figure British National Grid coordinates
- `BNGAlphaNumeric` - Searches for British National Grid Alphanumeric coordinates
- `LatLonDecimal` - Searches for Latitiude/Longitude coordinates in Decimal format
- `LatLonDMS` - Searches for Latitiude/Longitude coordinates in Degrees/Minutes/Seconds format
- `SphericalMercator` - Searches for Spheric Mercator (EPSG:3857) coordinates
- `PlusCode` - Searches for [PlusCodes](https://maps.google.com/pluscodes/)


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
