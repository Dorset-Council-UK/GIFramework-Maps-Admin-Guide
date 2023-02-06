# Proxying

GIFramework Maps has an in-built proxy based on Microsoft's [YARP](https://microsoft.github.io/reverse-proxy/). This can be used when layers can't be used with [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS), which is required for rendering layers and making metadata and feature requests.

The proxy can be enabled for specific [layers](../db/layers.md) or [web service definitions](../db/web-service-definitions.md). Read the documentation on those features to see how to enable the proxy.

The proxy directs requests via the application, so an allow list is used to make sure only domains you want to proxy are proxied.

!!! warning
    Proxying requests can reduce performance and may even be blocked by the service provider. If in doubt, check with the service provider.

## Relevant tables

| Table Name                        | Description                          |
| --------------------------------- | ------------------------------------ |
| ProxyAllowedHosts                 | Contains a list of allowed hosts that can use the proxy capabilities. Anything not in this list will be rejected by the proxy |

### ProxyAllowedHosts

This table contains a simple list of all allowed 'hosts'. The host portion includes the domain and any sub-domains, but not the protocol or anything after the domain name.

!!! example
    :white_check_mark: Good

    - environment.data.gov.uk
    - map.bgs.ac.uk

    :warning: Invalid

    - https://mapservice.example.com
    - mapservice.example.com/services/wms



