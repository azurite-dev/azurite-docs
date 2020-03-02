---
title: "Azurite API Configuration"
linkTitle: "API Configuration"
weight: 80
description: >
  Configuring and tuning your Azurite service
---

{{% pageinfo %}}
This information is only valuable if you are running your own Azurite service. The Hosted API cannot be configured.
{{% /pageinfo %}}

## Azurite

The default configuration of the Azurite API can be controlled using an `azurite.json` file in the app root directory.

The currently available configuration (with default values) looks like this:

```json
{ 
    "Azurite": {
        "RebuildWhitelist": ["127.0.0.1", "0.0.0.1"],
        "AllowPassthrough": false
    }
}
```

### Configuration Options

#### `RebuildWhiteList`

This setting is an array of IPv4 addresses that are allowed to initiate index rebuilds. In practice, only requests from these IPs will be able to hit the `/api/v1/index` endpoint to trigger a complete index build. By default, only `localhost` is allowed to do this, to prevent abuse.

#### `AllowPassthrough`

This setting is provided only for specific use cases and we recommend you leave it disabled (by default). Allowing passthrough will enable requests to be fulfilled even if a valid index isn't found. In practice, while this setting is enabled, requests that arrive without a valid index being present will still be completed by directly polling the upstream source. This will be slow, and might increase load on the upstream so this is only recommended as a temporary solution while index rebuilding is running or similar.

While this setting is disabled, requests that cannot be returned from the index will return a HTTP 507 response.

## Rate Limiting

Rate limiting is controlled by a separate configuration key:

```json
{
    "Azurite": {...}, //snipped
    "RateLimiting": {
        "GeneralRules": [
            {
                "Endpoint": "*:/api/*",
                "Period": "10s",
                "Limit": 5
            }
        ]
    }
}
```

These rules can control the limits applied to incoming requests, even down to specific endpoints.

> Since we just use [AspNetCoreRateLimit](https://github.com/stefanprodan/AspNetCoreRateLimit) under the hood, any of its configuration will work here