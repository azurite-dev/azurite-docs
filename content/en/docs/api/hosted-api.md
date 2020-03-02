---
title: "Azurite Hosted API"
linkTitle: "Hosted API"
weight: 20
description: >
  An introduction to the hosted Azurite service
---

To make getting started with Azurite easy, there's a running instance of the Azurite API available at `azurite.app`. To test it out, try opening `azurite.app/api/v1/ships` and you should see every ship in Azur Lane appear!

## Limitations

This service is running the current version of Azurite API and is available for anyone to use. That said, servers aren't free and I'm not good at running services, so there are some limitations to the hosted Azurite API:

- **Performance**: The service is running on cheap hosted hardware, so don't expect stellar performance at all times.
- **Rate Limiting**: To minimise the costs of running the service, `azurite.app/api` has some pretty heavy rate limiting. This should be fine for testing and *very small* use cases, but you might hit them after that.
- **Index Rebuilds**: I'll only rebuild the index on major updates so there may be a short delay on in-game changes being reflected from the API.

> During the testing and beta phases of the Azurite API, the limits will be dramatically more lenient. Any changes will be communicated in the [update notes](/blog/).

If any of this gets in the way of what you're building, you can always [host your own Azurite API](/docs/api/hosting).

### API Reference

Like all Azurite servers, you can browse the full API specification at [`/api/help`](https://azurite.app/api/help). This also allows you to experiment with the API easily, directly from the endpoint documentation.

### Rate Limits

When you make a request to Azurite, you'll actually get a bunch of headers in response. Among them will be a set of headers starting with `X-Rate-Limit-` that will give you information on how many requests you have remaining (`X-Rate-Limit-Remaining`) over what period of time (`X-Rate-Limit-Limit`) and when the limit will reset (`X-Rate-Limit-Reset`).