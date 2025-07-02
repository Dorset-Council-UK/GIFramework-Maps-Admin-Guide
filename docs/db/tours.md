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

- `Name` - a friendly name for the tour used by admins
- `Frequency` - a number indicating how often to show the tour. Available options are:
    - `-1` - indicates that the tour should only be shown once, and never again
    - `0` - indicates that the tour should always be shown
    - `Any positive number` - indicates the number of days to leave between showing the tour again.
- `UpdateDate` - a date when this tour has been updated enough to re-show it to the user. For example, if you make significant changes to the tour and want to forcibly re-trigger it for all users, set this to the current date, and anyone who hasn't viewed or dismissed the tour since that date will be re-prompted

### TourSteps

This table contains the individual steps used in a tour

- `Title` - this text will appear in bold at the top of the tour step
- `Content` - what you want your step to say. You should include HTML markup for links and also target="_blank" as this will make sure the link opens in a new window
- `AttachToSelector` - a CSS selector you want the tour step to attach to (include the '.'), if you leave this blank the tour step will float in the middle of the screen
- `AttachToPosition` - where on the selector you want the tour step to attach (if you've chosen one). Should be one of `top`, `left`, `bottom`, `right`
- `StepNumber` - the order in which the step will appear within the tour
- `TourDetailId` - the ID from the `TourDetails` table of the tour this step is attached to

### Versions

Within the `Versions` table, there is a `TourDetailsId` column. Set this to the `Id` in the `TourDetails` table of the relevant tour you want to use with this version. Leave blank for no tour.

!!! warning
    This feature relies on `localStorage`, a browser feature that allows us to store small amounts of data on the users browser. Some users or organisation may disable `localStorage`, in which case the tour will always trigger, regardless of the frequency setting
