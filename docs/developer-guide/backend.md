---
layout: default
title: Backend
permalink: /developer-guide/backend/
parent: Developer Guide
nav_order: 3
---

# Backend

When running the project, you must use the terminal command `dotnet run` to start the project
instead of running it through Rider or any other IDE as the environment variables may not be
loaded correctly.
 {: .warning }

## Backend components

### Stack

- C# + dotnet core
- Entity framework as ORM
- PostgreSQL as database

### Platform

- Using Dokku + DigitalOcean
- Must provide more documentation on deployment for this year's iteration

### Notable files

- `ApiModels/*` stores the DTOs used for request/response (used by Swagger + orval to replicate models on FE)
- `Controllers/*` stores the core endpoint logic (controller layer); set endpoint URL + RBAC/ABAC here
- `Models/*` stores entity framework models mapped from database (data layer)
- `Logic/*` stores  API logic (service layer)
- `Database/HnrApiDbContext.cs` is the database config
- `Middleware/*` contains middleware that trigger before controllers are called
- `Migrations/*` is the DB migrations, add new one for future migrations and use dotnet ef commands to migrate/update/rollback

## Environment Variables

C# sections its environment variable handling in the following ways:

1. Using `appsettings.json` - production
2. Using `launchSettings.json` - local
3. Direct passing before command - both

For the backend, we recommend creating a `.env` file and loading that using
`export $(cat .env | xargs)` before running the backend.

```bash
# To get started running the backend locally, you must provide the following URLs at the very least
# Project name when setting up Firebase
FIREBASE_PROJECT_ID=

# PostgreSQL URL for database
DATABASE_URL=

DISCORD_CLIENT_ID=
DISCORD_BOT_TOKEN=
DISCORD_JOINLOG_WEBHOOK=
DISCORD_GUILD_ID=
DISCORD_PARTICIPANTS_ROLE_ID=
REWARDS_PER_SPONSOR=
REWARDS_PER_USER=
BOT_TOKEN=
LAX_CORS=
GIT_REV=
```
