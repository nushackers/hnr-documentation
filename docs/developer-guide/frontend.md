---
layout: default
title: Frontend
permalink: /developer-guide/frontend/
parent: Developer Guide
nav_order: 4
---

# Frontend

If the `NEXT_PUBLIC_FLAGS_URL` is set to a non-empty value in `.env`, you may notice that you will
always be redirected back to `/` even if you set the `stgFlags.stage` to `open`.
<br><br>
To resolve this, please remove the value for `NEXT_PUBLIC_FLAGS_URL` while on `localhost`.
{: .warning }

## Frontend components

### Stack

- React + Next.js
- Axios for API calls

### Platform

- Netlify

### Notable files

- `useFlags.tsx` is used to toggle flag state about different components of the website (separate
  flags repository to avoid redeployments)
- `backend/model/*` stores the DTOs used for each backend endpoint (auto generated using orval
  from the Swagger file)
- `data/*` has some hardcoded values of various elements of the website in JSON files
- `pages/*` is standard React pages
- `components/*` is standard React components

## Environment variables

```bash
# From Google console for Firebase project
NEXT_PUBLIC_FIREBASE_API_KEY=

# Project name when setting up Firebase
NEXT_PUBLIC_FIREBASE_PROJECT_ID=

# From Firebase project settings page (scroll to the bottom)
NEXT_PUBLIC_FIREBASE_APP_ID=

# From Discord bot in the Discord bot developer portal
NEXT_PUBLIC_DISCORD_CLIENT_ID=

# From Discord server (enable Developer Mode to copy link)
NEXT_PUBLIC_DISCORD_GUILD_ID=

# From Discord server (enable Developer Mode to copy link)
NEXT_PUBLIC_DISCORD_LFT_CHANNEL_ID=

# Staging/Prod API URL, uses NODE_ENV to
# toggle to this variable or to localhost:5134 (for local)
NEXT_PUBLIC_API_URL=

# Points to flag repository to read from
# If running locally, do not set this value, otherwise, the flags will be wrong
NEXT_PUBLIC_FLAGS_URL=

# Disables Firebase auth mode, to leave this alone
NEXT_PUBLIC_DISABLE_FIREBASE_AUTH=
```

## Important pointers for future iterations

- Must regenerate a new Firebase store
- Must update Discord guild ID, channel ID + (potentially new Discord bot token)