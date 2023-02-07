# Tours

Tours are used to give users a quick overview of the features of GIFramework Maps. Tours are highly configurable, and different tours can be applied to specific versions.

## Relevant tables

| Table Name                        | Description                          |
| --------------------------------- | ------------------------------------ |
| TourDetails                       | Basic details about available tours that can be applied to versions, including frequency and update dates |
| TourStep                          | Contains the individual steps of a tour |
| Versions                          | Contains an optional `TourDetailsId` column used to define which tour to use |

### TourDetails

This table contains the basic, top level tour details

- `Name` - A friendly name for the tour used by admins
- `Frequency` - A number indicating how often to show the tour. Available options are:
    - `-1` - Indicates that the tour should only be shown once, and never again
    - `0` - Indicates that the tour should always be shown
    - `Any positive number` - Indicates the number of days to leave between showing the tour again.
- `UpdateDate` - A date when this tour has been updated enough to re-show it to the user. For example, if you make significant changes to the tour and want to forcibly re-trigger it for all users, set this to the current date, and anyone who hasn't viewed or dismissed the tour since that date will be re-prompted

### Versions

Within the `Versions` table, there is a `TourDetailsId` column. Set this to the `Id` in the `TourDetails` table of the relevant tour you want to use with this version. Leave blank for no tour.

!!! warning
    This feature relies on `localStorage`, a browser feature that allows us to store small amounts of data on the users browser. Some users or organisation may disable `localStorage`, in which case the tour will always trigger, regardless of the frequency setting
