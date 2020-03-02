---
title: "Introduction"
linkTitle: "Introduction"
weight: 1
description: >
  A basic primer on the Azurite API Project
---

Azurite is an **unofficial** API service that provides access to a range of ship data for ships in Azur Lane. This project is not affiliated with Yongshi, Manjuu or Yostar in any way, and is based entirely on community resources for the community.

## Status and Limitations

This is a new project that's been hacked together over a couple of weeks. As such, it still has some pretty big missing functionality:

- **No skins**: Still unsure whether this will be included in the API.
- **Talents**: Talents aren't available and *may not ever be*. Limitations in how we're retrieving data make it a fragile process to build.
- **Equipment**: Equipment slots are currently included in ship details, but this is currently in preview and **heavily** subject to change
- **Statistics** are implemented, but as they currently stand are also using a (sort of unwieldy) fixed schema. This might change in future versions.

> If there are specific features you would like to see implemented (within reason), open an issue and we can discuss the viability.

### Data Sources

At current, this project retrieves data from the [Azur Lane Wiki](https://azurlane.koumakan.jp/Azur_Lane_Wiki). Since an API that just returned a parsed wiki page per-request would be punishingly awful for the backend wiki, this project includes an "indexing" layer (called `Azurite.Index`) that serves as part-cache, part-database for ship data retrieved from the Wiki. This index does have to be fully populated at least once!

> There's also some light HTTP caching in the Wiki interface code, but `Index` is the superior solution.

#### Alternative Sources

All the ship data retrieved from the Wiki happens in a separate `Azurite.Wiki` project using the `IShipDataProvider` interface so it is reasonably easy to add a new/replacement data source by implementing that interface and returning the correct data.

### Clients and Apps

At present, the project supports just the two main components:

- **API**: the HTTP REST(ish) API for access to game data
- **CLI**: the Command-Line Interface app for accessing game data.

> While the CLI is completely independent of the API, they share a significant portion of logic and code.

### API Hosting

At this time, we do offer a live hosted instance of the API for public use, but this comes with caveats. The hosted API is only intended for development, testing and *very* light usage scenarios. You can read more about this in the [Hosted API docs](/docs/api/hosted-api).

If you want to use the API for anything other than very light usage, you should host your own! It's easy and it's possible to run the API itself in almost any app hosting environment. For more details on hosting your own API, check out [the self-hosting docs](/docs/api/hosting).