---
title: "Azurite Hosting"
linkTitle: "Hosting"
weight: 30
---

Hosting your own Azurite API is very simple. The process depends on how you want to install and deploy your API: Docker container, native package, or manually.

## Choosing the right method

## Docker

Deploying Azurite via Docker is probably the easiest method available, and certainly the easiest to get started with. First, pull the image to your machine with the following command:

```bash
docker pull quay.io/azurite/azurite:stable
```

Next, run the container, binding your chosen port to port 80 in the container:

```bash
docker run -p 8080:80 quay.io/azurite/azurite:stable
```

You can then access your API at `localhost:8080`. You can test this by calling/browing `http://localhost:8080/version/` to get the raw Azurite version back.

### Building an index

At the moment your API will fail, unless you allow passthrough in your configuration, as there is no index for the API to read data from. You have two options here:

1. **Build the index in-container**: if you have the time and are not planning on restarting/recreating the container often, you can invoke an index rebuild inside the container using the container ID (check `docker ps`).

```bash
docker exec <CONTAINER_ID> curl -d -XPOST localhost/api/v1/index
```

2. **Pre-build an index and mount it**: If you already have a `ships.db` built using a previous instance, or using the CLI, you can include that file in the container and Azurite will load it:

```bash
docker run -p 8080:80 -v /path/to/prebuilt/ships.db:/app/ships.db quay.io/azurite/azurite:stable
```

> You can use a `ships.db` file from the Azurite CLI to power the Azurite API! They're the same format!

## Run Manually

First, you will need to download the matching `.zip` file for your chosen platform and extract it to a local folder.

Run the binary for your platform (`azurite.exe` for Windows, `azurite` for Linux/macOS) and the server should be listening at `http://localhost:5000`. Configuration should be done in the `appsettings.json` file in the directory you extracted to. You will also need to build an index (by calling `http://localhost:5000/api/v1/index`) or copy a pre-built `ships.db` file to the extract directory.