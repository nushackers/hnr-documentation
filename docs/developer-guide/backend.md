---
layout: default
title: Backend
permalink: /developer-guide/backend/
parent: Developer Guide
nav_order: 2
---

Steps apply for locally run setup, for deployment configuration changes, refer to
[deployment section](/deployment). For database setup, refer to [database section](/database).

1. Clone repository

    ```plain
    git clone https://github.com/nushackers/hnr-api.git
    ```

2. Change to directory

    ```plain
    cd hnr-api
    ```

3. Open project in Rider to automatically setup the project
4. Setup `.env`, see [launch settings section](#environment-variables)
5. Start the development server

    ```plain
    dotnet run
    ```

### Backend components

#### Stack

- C# + dotnet core
- Entity framework as ORM
- PostgreSQL as database

#### Platform

- Using Dokku + DigitalOcean
- Must provide more documentation on deployment for this year's iteration

#### Notable files

- `ApiModels/*` stores the DTOs used for request/response (used by Swagger + orval to replicate models on FE)
- `Controllers/*` stores the core endpoint logic (controller layer); set endpoint URL + RBAC/ABAC here
- `Models/*` stores entity framework models mapped from database (data layer)
- `Logic/*` stores  API logic (service layer)
- `Database/HnrApiDbContext.cs` is the database config
- `Middleware/*` contains middleware that trigger before controllers are called
- `Migrations/*` is the DB migrations, add new one for future migrations and use dotnet ef commands to migrate/update/rollback

### Launch settings

C# sections its environment variable handling in the following ways:

1. Using `appsettings.json` - production
2. Using `launchSettings.json` - local
3. Direct passing before command - both

For the backend, we recommend creating a `.env` file and loading that using
`export $(cat .env | xargs)` before running the backend.

- `DATABASE_URL`
- `DISCORD_CLIENT_ID`
- `DISCORD_BOT_TOKEN`
- `DISCORD_JOINLOG_WEBHOOK`
- `DISCORD_GUILD_ID`
- `DISCORD_PARTICIPANTS_ROLE_ID`
- `REWARDS_PER_SPONSOR`
- `REWARDS_PER_USER`
- `BOT_TOKEN`
- `FIREBASE_URL`
- `SqlConnectionString` - overwritten by `DATABASE_URL`
- `FIREBASE_PROJECT_ID`
- `LAX_CORS` - important
- `GIT_REV`