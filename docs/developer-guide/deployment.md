---
layout: default
title: Deployment
permalink: /developer-guide/deployment/
parent: Developer Guide
nav_order: 5
---

## Overview
Currently both staging and production API are in the same droplet, and
both use the same managed database provided by DigitalOcean.

How it works is that we have a `docker-compose.yml` in `~/services/api` which runs
both containers.

## Deploying and Destroying the Containers

We have scripts in the `~/services/scripts` repo that we can use for booting up or shutting down the repo.
Simply just run `deploy-up.sh` or `deploy-down.sh` to start all services. Note that you need to be root/superuser/docker group
to do this.

## Zero Downtime Deployment

In the event that the deployment is live (either staging or production) and we want to update with zero downtime,
all we need to do is to run the `prod-deploy.sh` script. Ideally we still want to do this sometime where traffic
is low, but it should run with basically zero downtime.

What the script does is it removes any cached builds, rebuilds the API containers but under a separate temporary project. It then
downs the current APIs, and uses the cached builds of the temporary project to instantly up it. In the meantime, the temporary
container handles all traffic (we won't have any stats or analytics during that period).

To update any of the prod/staging, go to their respective directories, ~/hnr-api and ~/staging respectively,
and update them to the branch/commit you want to deploy. Then, just go into the scripts folder and run `prod-deploy.sh`

## Database Migration

For database migration, there's probably a better way to do this, but basically we just want to run these commands:

Start a docker container with dotnet:
```bash
docker run -it -w /app -v ~/hnr-api:/app mcr.microsoft.com/dotnet/sdk:6.0 /bin/bash
```

> Note: If you want to update it via whatever commit is in staging, switch ~/hnr-api with ~/staging instead

Install dotnet-ef (the appropriate version):
```bash
dotnet tool install --global dotnet-ef --version 6.*
```

Update the PATH:
```bash
export PATH="$PATH:/root/.dotnet/tools"
```

And then run the migration command:
```bash
postgres://something:something dotnet ef database update
```

> Note: If you are copying the connection string from DO, remember it is `postgres://` not `postgresql://`, you need to 
> change it

## Monitoring for errors

Because we don't really have any unit tests or anything, we want to be careful about errors. We have a proper 
monitoring and logging system for this.

To check status codes (to monitor and major outages):
* Go to `grafana.nushackers.org`, creds in bitwarden.
* Go to Dashboards > Traefik Official Standalone Dashboard
* Change the time range on the top right to the desired time range
* Change the `service` variable to check between staging and production
* Use this dashboard to check for status codes in general

To check for controller level traffic and errors:
* Go to `grafana.nushackers.org`, creds in bitwarden.
* Go to Dashboards > ASP.NET Core - controller summary (Prometheus)
* Change the time range on the top right to the desired time range
* You should be able to see requests and errors for each individual controller

To check for docker logs manually
* SSH into the instance, using the webshell or ssh keys set up
* Our APIs are under the compose project named `api`, so to check, we just do:

```bash
docker compose -p api logs | less
```