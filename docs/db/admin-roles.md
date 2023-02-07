# Administrative roles

In order to use the [management interface](../gui/getting-started.md), users need to be assigned the appropriate roles.

!!! info
    This section assumes you are using Microsoft Azure AD B2C authentication, the only currently supported authentication scheme in GIFramework Maps. If you are not using authentication, this section is not relevant.

## Relevant tables

| Table Name                        | Description                          |
| --------------------------------- | ------------------------------------ |
| ApplicationRoles                  | Contains all the available Roles users can have. **This should not be edited as it is tied directly to the application code** |
| ApplicationUserRoles              | Mapping between user identifiers and the roles they have |

### ApplicationRoles

This table contains the role names available in the application. Currently there is only one role, GIFWAdmin. This role gives access to **all** the administrative functions of the application, so should only be given to highly trusted users. 

!!! warning
    The data in this table is relied on by the application directly, so should not be edited

### ApplicationUserRoles

This table contains the mapping between a user and the roles they have been given. To give a user a role, simply provide their user identifier and the ID from the ApplicationRoles table.

!!! hint
    You can get a user's identifier (or your own) by getting them to go to `https://<your-application-root>/account/diagnostics` and looking up the `nameidentifier` value.

