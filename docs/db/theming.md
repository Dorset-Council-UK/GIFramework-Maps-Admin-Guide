# Theming

Versions in GIFramework Maps can have different themes applied to them.

## Relevant tables

| Table Name                        | Description                          |
| --------------------------------- | ------------------------------------ |
| Theme                             | Basic theme information that can be applied to versions, including logos and colours |
| Versions                           | Contains a `ThemeId` column used to define what theme is applied to this version |

### Theme

This table contains the theme details.

- `Name` - A friendly name for the theme used by admins
- `Description` - A more detailed description for the theme used by admins
- `PrimaryColour` - The hex code (without the `#`) for the primary colour used in the theme
- `LogoURL` - A URL to the logo that appears in the top right. Ideally this should be an SVG or PNG
- `CustomFaviconURL` - An  optional URL to a folder containing the following four favicon items:
    - `favicon.ico`
    - `apple-touch-icon-precomposed.png`
    - `android-chrome-192x192.png`
    - `android-chrome-512x512.png`

### Versions

Within the `Versions` table, there is a `ThemeId` column. Set this to the `Id` in the `Theme` table of the theme you want to apply.
