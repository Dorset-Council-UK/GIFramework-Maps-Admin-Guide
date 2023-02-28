# Versions

Versions are the best way to split maps up into different themes, with different layers, permissions and functionality.

## Add a new version

Select **Create new version** and fill in the details:

- Name
- Slug - the bit at the end of the URL. For example: 'highways' -> `https://<your-application-root>/highways`
- Description
- Theme - the [theme](../gui/themes.md) you want your version to use
- Start extents - the [bound](../gui/bounds.md) to set the map to
- Enabled - sets whether the version is enabled or not
- Require login - choose whether you want the version to require a user to login to use it
- Welcome message (optional) - the [welcome message](../gui/welcome-messages.md) you want your version to use
- Tour (optional) -  the [tour](../gui/tours.md) you want your version to use
- Show login option - choose whether you want to show an option for users to login
- Help URL (optional) - include a link to custom documentation
- Feedback URL (optional) - include a link to a feedback form
- Redirection URL (optional) - a URL to redirect the user to instead of loading the version. Can be useful if a version changes slug, or you want to point people elsewhere
- Purge cache - ticking this box will purge the cache and allow your version to be available for testing or use straight away

On the right side of the screen, you'll see options for:

- Basemaps - choose which basemaps you want to include in your version and which one you want to set as the default
- Categories - choose which layer categories you want to include in your version


## Edit a version

Select the version you want to edit. Make the changes you want and hit Save.

## Delete a version

Select the version you want to delete. You will be asked if you're sure, press Delete again to confirm.