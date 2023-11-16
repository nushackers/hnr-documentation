---
layout: default
title: Database
permalink: /developer-guide/database/
parent: Developer Guide
nav_order: 3
---

Hack&Roll uses PostgreSQL for the database. Install it first and then set it up via:

1. Create new database locally with `<name>`
2. Install .NET dependency for Entity Framework

    ```plain
    dotnet tool install --global dotnet-ef
    ```

3. Migrate the database to create tables

    ```plain
    DATABASE_URL=postgres://postgres:root@localhost:5432/<name> dotnet ef database update
    ```
