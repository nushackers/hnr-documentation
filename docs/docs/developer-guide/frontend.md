---
layout: default
title: Frontend
permalink: /developer-guide/frontend/
parent: Developer Guide
nav_order: 1
---

Steps apply for locally run setup, for deployment configuration changes, refer to [deployment section](/deployment).

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

5. Set `useFlags.tsx`, `stgFlags.stage` to `open`

6. Start the development server. Must use `yarn dev` as that allows all the URLs to point to
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