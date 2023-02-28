#  Clearing the cache

Most of the data in the database tables listed here are cached for varying amounts of time, to improve performance.

You would usually use the [management interface](../gui/system.md) to clear the cache. If you do not have access to the management interface, you can either wait for the cache to invalidate by itself, or you will have to restart the application/recycle the application pool. This is dependent on your particular server configuration and is outside the scope of this documentation.

## Cached items

| Name                           | Key                                     | Cache length |
| ------------------------------ | --------------------------------------- | ------------ |
| Version Configuration by Slug  | VersionBySlug/{slug}                    | 10 minutes   |
| Version Configuration by ID    | Version/{id}                            | 10 minutes   |
| User Roles by User ID          | UserRole/{userId}                       | 2 minutes    |
| Web Layer Service Definitions  | WebLayerServiceDefinitions              | 10 minutes   |
| Proxy Allowed Hosts            | ProxyAllowedHosts                       | 12 hours     |
| Print Configuration by Version | PrintConfigurationByVersion/{versionId} | 10 minutes   |
| Search Definitions by Version  | SearchDefinitions/{versionId}           | 10 minutes   |
| API Search Definitions         | APISearchDefinitions                    | 1 hour       |
| Database Search Definitions    | DBSearchDefinitions                     | 1 hour       |
| Local Search Definitions       | LocalSearchDefinitions                  | 1 hour       |