# Print Configuration

Print configurations are basic details on the layout of prints in a version.

!!! info "Work in progress"
    Currently the only supported customisation is the logo that appears on the print. More options will be added in the future

## Relevant tables

| Table Name                        | Description                          |
| --------------------------------- | ------------------------------------ |
| PrintConfigurations               | Contains the configurations for prints that can be applied to a version |
| VersionPrintConfiguration         | Mapping between print configurations and versions, showing which print configurations are available in which version | 

### PrintConfigurations

This table contains the details of all your custom print configurations.

- `Name` - A friendly name for the configuration used by admins
- `LogoURL` - The URL to a logo that will be drawn on to the map

### VersionPrintConfiguration

The `VersionPrintConfiguration` table defines which print configurations are used in which versions.

- `VersionId` - The `Id` from the `Versions` table
- `PrintConfigurationId` - The `Id` from the `PrintConfigurations` table

!!! note
    If a specific configuration is not set for a version, it will fall back to that defined for the 'general' version

