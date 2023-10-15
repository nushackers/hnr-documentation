# Developer Guide

Quick guide to help navigate the codebase of both the frontend and backend components.

## Firebase Setup

1. Create Firebase project
2. Initialise Web application
3. Enable "Authentication" and allow
   1. Email
   2. Google
   3. Github

## Discord Setup

1. Create new Discord server for the year (use the template from 2022 server)
2. Create new Discord bot

## Frontend

Steps apply for locally run setup, for deployment configuration changes, refer to
[deployment section](#deployment).

1. Clone repository

    ```plain
    git clone https://github.com/nushackers/hnr-frontend.git
    ```

2. Change to directory

    ```plain
    cd hnr-frontend
    ```

3. Install dependencies

    ```plain
    yarn install
    ```

4. Setup `.env`, see [environment variables section](#environment-variables)

5. Start the development server. Must use `yarn dev` as that allows all the URLs to point to
   `localhost`

    ```plain
    yarn dev
    ```

### Frontend components

#### Stack

- React + Next.js
- Axios for API calls

#### Platform

- Netlify

#### Notable files

- `useFlags.tsx` is used to toggle flag state about different components of the website (separate
  flags repository to avoid redeployments)
- `backend/model/*` stores the DTOs used for each backend endpoint (auto generated using orval
  from the Swagger file)
- `data/*` has some hardcoded values of various elements of the website in JSON files
- `pages/*` is standard React pages
- `components/*` is standard React components

### Environment variables

- `NEXT_PUBLIC_FIREBASE_API_KEY` - from Google console for Firebase project
- `NEXT_PUBLIC_FIREBASE_PROJECT_ID` - project name when setting up Firebase
- `NEXT_PUBLIC_FIREBASE_APP_ID` - from Firebase project settings (scroll down)
- `NEXT_PUBLIC_DISCORD_CLIENT_ID` - from Discord bot
- `NEXT_PUBLIC_DISCORD_GUILD_ID` - from Discord server (must enable Developer Mode to copy
    link)
- `NEXT_PUBLIC_DISCORD_LFT_CHANNEL_ID` - from Discord server
- `NEXT_PUBLIC_API_URL` - refers to staging/prod URL, if running locally, ensure `NODE_ENV` is
    in `development`
- `NEXT_PUBLIC_FLAGS_URL` - used to load flags without needing to redeploy, must ask for
    access, if running locally, no issues
- `NEXT_PUBLIC_DISABLE_FIREBASE_AUTH`

### Important pointers for future iterations

- Must regenerate a new Firebase store
- Must update Discord guild ID, channel ID + (potentially new Discord bot token)

## Backend

Steps apply for locally run setup, for deployment configuration changes, refer to
[deployment section](#deployment). For database setup, refer to [database section](#database).

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

## Database

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

## Deployment
