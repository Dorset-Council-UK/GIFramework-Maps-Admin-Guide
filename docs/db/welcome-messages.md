# Welcome messages

The welcome message is a popup that can appear when you first load the map. Welcome messages are configurable per version.

## Relevant tables

| Table Name                        | Description                          |
| --------------------------------- | ------------------------------------ |
| WelcomeMessages                   | Contains the welcome message definitions that can be applied to a version |
| Versions                          | Contains an optional `WelcomeMessageId` column used to define which welcome message to us in this version |


### WelcomeMessages

This table contains the welcome message details.

- `Name` - A friendly name for the welcome message used by admins
- `Title` - The title used in the popup of the welcome message
- `Content` - The HTML content of the popup message
- `Frequency` - A number indicating how often to show the welcome messages. Available options are:
    - `-1` - Indicates that the message should only be shown once, and never again
    - `0` - Indicates that the message should always be shown
    - `Any positive number` - Indicates the number of days to leave between showing the message again.
- `UpdateDate` - A date when this message has been updated enough to re-show it to the user. For example, if you make significant changes to the message and want to forcibly re-trigger it for all users, set this to the current date, and anyone who hasn't viewed or dismissed the message since that date will be re-prompted
- `DismissOnButtonOnly` - A boolean indicating whether the welcome message should **only** be closed by users clicking the dismiss button at the bottom, rather than the close button in the top or by clicking outside of the popup
- `DismissText` - An optional string for the text that will appear in the dismiss button. Leave blank for default of 'Close'

!!! hint
    Setting `DismissOnButtonOnly` to `true` along with a `Frequency` of `0` or `1` and a custom `DismissText` can work as a *reasonable* alternative to a standard 'Agree to our terms' screen. For user experience reasons, try not to do this too much if you don't need to

### Versions

Within the `Versions` table, there is an optional `WelcomeMessageId` column. Set this to the `Id` in the `WelcomeMessages` table of the relevant welcome message you want the version to have.  Set to null for no welcome message.

!!! warning
    This feature relies on `localStorage`, a browser feature that allows us to store small amounts of data on the users browser. Some users or organisation may disable `localStorage`, in which case the welcome message will always trigger, regardless of the frequency setting