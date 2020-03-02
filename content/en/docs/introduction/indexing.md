---
title: "Indexing and Load"
linkTitle: "Indexing and Load"
weight: 20
---

> This applies to the CLI as well as hosted APIs

Since we are pulling data from upstream sources (generally the Azur Lane Wiki), we want to be reasonable about the load we put on those sources. Retrieving and parsing the source pages on every request is by far the easiest answer, but would place a ton of extra load on the wiki that we don't want to do to a community resource. This is why the index layer exists, but it still needs data, so on first run (and whenever changes are made) it needs to be rebuilt.

## Ship Index

The ship data index (as of API v1) is a single file called `ships.db` that resides in the Azurite application directory. This data file contains a representation of all the data we extract from the data source (i.e. the Azur Lane Wiki) that our API uses. This way, the API and the CLI (they use the same format) can read from the local file and return it immediately without having to hit the upstream page every time you make a request.

This is a more complicated solution than just fetching the page on-demand, but gives us a few benefits:

1. **Less upstream load**. We don't want to overload the Azur Lane Wiki (or any other sources) if we can avoid it. Using the index, every page gets hit exactly once and then the apps can just pull directly from the index.

1. **More responsive**. Since we're not doing multiple HTTP round trips, requests for ship data only have to hit the index and immediately return, meaning requests can be dramatically faster.

1. **Offline capability**. After the index is built, Azurite apps don't need to hit the Internet again, so we can cover edge cases like the CLI working offline or hosting the API even with slow or expensive Internet connections.

There's one very big downside of the index though: building it. 

### Building the Index

Without extra configuration, Azurite is not designed to run without an index present so there's a one-time prerequisite of actually building the index. This is a pretty easy process that's built in to both the CLI and the API, but there's one gotcha: it's ***slow***.

The index build process involves almost 500 separate page loads to the upstream wiki. On top of that, to limit how badly we load the upstream site, the Azurite index build process deliberately adds delay between page loads. As such, the build process can take up to *an hour* by default. In general, you can keep using this index until there's changes you need (i.e. new ships, stat changes etc).

> It's possible to disable the delay entirely while building the index, but I recommend against it.