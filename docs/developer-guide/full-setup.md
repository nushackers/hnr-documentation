---
layout: default
title: Full Setup
permalink: /developer-guide/full-setup/
parent: Developer Guide
nav_order: 1
---

# Full Setup

For more information about the details of each component, refer to each individual page:

- [Frontend](/developer-guide/frontend)
- [Backend](/developer-guide/backend)
- [Database](/developer-guide/database)

This guide only contains the preliminary steps to get the WebApp running locally. Further configuration like Discord support etc. are not covered here.
{: .note}

## Prerequisites

Ensure the following prerequisites are installed first:

- [PostgreSQL](https://www.postgresql.org/download/)

- [.NET](https://dotnet.microsoft.com/en-us/download)

- [Node.js](https://nodejs.org/en/download)

- Entity framework CLI

    ```bash
    dotnet tool install --global dotnet-ef
    ```

Additionally, setup Firebase as instructed in [the developer guide.](/developer-guide)

## Steps

First, we have to setup the database first.

1. Create a database locally with `<name>`
2. Clone the backend repository

    ```bash
    git clone https://github.com/nushackers/hnr-api.git
    ```

3. Change to project directory

    ```bash
    cd hnr-api/
    ```

4. Migrate the database to create all tables

    ```bash
    DATABASE_URL=postgres://postgres:root@localhost:5432/<name> dotnet ef database update
    ```

Then, setup the backend.

1. Create `.env` with the following **minimal** variables:

    ```bash
    DATABASE_URL=postgres://postgres:root@localhost:5432/<name>
    # Project name when setting up Firebase
    FIREBASE_PROJECT_ID=
    ```

2. Load `.env` to the terminal

    ```bash
    export $(cat .env | xargs)
    ```

3. Start the backend

    ```bash
    dotnet run
    ```

The backend will run on `http://localhost:5134` by default. To change this, modify the `launchSettings.json` file under the `applicationUrl` property.
{: .note}

Finally, setup the frontend.

1. Return to home directory

    ```bash
    cd ../
    ```

2. Clone the frontend repository

    ```bash
    git clone https://github.com/nushackers/hnr-frontend.git
    ```

3. Change to project directory

    ```bash
    cd hnr-frontend/
    ```

4. Install dependencies

    ```bash
    yarn install
    ```

5. Setup `.env` with relevant details, refer to [this section for the fields needed](/developer-guide/frontend#environment-variables)

    The key fields needed will be `NEXT_PUBLIC_FIREBASE_API_KEY`, `NEXT_PUBLIC_FIREBASE_PROJECT_ID`, and `NEXT_PUBLIC_FIREBASE_APP_ID`

    The values of `NEXT_PUBLIC_API_URL` and `NEXT_PUBLIC_FLAGS_URL` should both be blank as well.
    {: .note}

6. Start the development server

    ```bash
    yarn dev
    ```

    `yarn dev` must be used to set `NODE_ENV` to `development`. Otherwise, the frontend will try using production values instead.
    {: .warning}

Lastly, validate the setup by visiting `localhost:3000/register` and attempting to create a new account. If all goes well, you should be able to view the newly created account in Firebase and a new database entry should be found under the `"Users"` table of the database.