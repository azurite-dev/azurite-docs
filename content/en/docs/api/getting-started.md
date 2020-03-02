---
title: "Getting Started"
linkTitle: "Getting Started"
weight: 10
description: >
  Getting started with the Azurite HTTP API
---

The Azurite HTTP API makes Azur Lane ship data available to any client that supports HTTP. Using a REST-like API, you can request information about available ships, specific ship details and even search by criteria not available in-game.

The first thing you'll need to get started with the HTTP API is an Azurite server. Fortunately, if you don't have your own, you can always use the [Hosted API](/docs/api/hosted-api) we provide. If you're [running your own](/docs/api/hosting), use your server address for the below examples.

> As always, the full list of API endpoints and their request/response formats is available in the [API Reference](/docs/reference)

For example, you can get a summary list of all available ships using the following `curl` command:

```bash
# swap out azurite.app with your own address for self-hosted server
curl https://azurite.app/api/v1/ships
```

This will give you a (very long) JSON summary output of all the ships currently available. You can then use that data to pull a specific ship's details by ID:

```bash
curl https://azurite.app/api/v1/ships/3119
```

or just look for all the Super Rare Eagle Union Ships:

```bash
curl https://localhost:5001/api/v1/ships?rarity=SuperRare&Faction=Eagle%20Union
```

> In general, it's best to retrieve ship summaries from `/api/v1/ships` and use the IDs returned from that call to get specific ship details. This should skip a request and validation won't be an issue.

## Choosing the right server

More information about using the hosted API vs running your own is available in the documentation for [the Hosted API](/docs/api/hosted-api) and [Self-Hosting](/docs/api/hosting).
