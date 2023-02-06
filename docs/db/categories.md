# Categories

All [layers](../db/layers.md) need to be within a category. Layers can appear in many categories. Categories can appear in many versions.

## Relevant tables

| Table Name                        | Description                          |
| --------------------------------- | ------------------------------------ |
| Category                          | Basic details about categories that layers can be sorted into |
| CategoryLayer                     | Mapping between layers and the categories they are added to |
| VersionCategory                   | Mapping between categories and versions, showing which categories are available in which version |

### Category

This table contains the basic category details. 

- `Name` - The name of the category as it will appear in the layer control
- `Description` - A friendly description of the category for administrators
- `Order` - The order the category will appear in the layer control
- `ParentCategoryId` - If this category is a child of another category, put the parents’ category ID in here. If not, leave it blank.

### CategoryLayer

The `CategoryLayer` table defines which layers are available in which categories.

- `LayerId` - The `Id` from the `Layer` table
- `CategoryId` - The `Id` from the `Category` table
- `SortOrder` - The position this layer should appear within this category

## VersionCategory

The `VersionCategory` table defines which categories are available in which versions.

- `VersionId` - The `Id` from the `Version` table
- `CategoryId` - The `Id` from the `Category` table

!!! bug
    If you want this category to appear in many versions, but in different orders, you will need to make different categories, as the ordering cannot be set by version

!!! info
    If your category is a child, both the parent AND child categories need to be added to this table.

