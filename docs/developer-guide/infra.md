---
layout: default
title: Database
permalink: /developer-guide/infra/
parent: Developer Guide
nav_order: 6
---

![](./assets/infra_overview.png)

## Getting Started

* Create a new DO instance (whatever size, need to load test this)
* Setup ssh keys for the instance
* Clone https://github.com/nushackers/hnr-infra
* Run the `./deploy-up.sh` to start all the services, and `./deploy-down.sh` to stop everything

## Droplet Components

* Traefik + Let's Encrypt
    * This is the main proxy where all the traffic comes through and gets directed to different containers.

* Prometheus
    * Where all the logs are aggregated. This is connected to an external Grafana instance for monitoring

## Observability Tools

* Traefik Metrics
* Node Exporter

    