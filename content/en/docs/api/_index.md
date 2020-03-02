---
title: "Azurite HTTP API"
linkTitle: "HTTP API"
weight: 30
---

{{% pageinfo %}}
This documentation will go over the high-level design, deployment, configuration and hosting of the HTTP API. For details of specific endpoints and what to expect in return, check the [API reference](/docs/reference)
{{% /pageinfo %}}

The main purpose of the Azurite project is the HTTP API. This API provides access to ship data through convenient HTTP requests. Note that while the API is REST-like, it definitely won't pass careful scrutiny of it's RESTfulness.



In addition to the "mainline" API, this project includes a simple command-line to perform local-only basic operations. The CLI must have its index populated before use, but is then able to run completely offline and provides basic ship listing functionality.

Since it uses the excellent `Spectre.Cli`, you can always check the usage by running with `--help`.
