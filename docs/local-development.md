# Local development

Each repository runs on its own; see its README. This page covers running the **whole stack** together, for integration and end-to-end testing.

## Prerequisites

- Node.js 24 LTS with Corepack enabled (`corepack enable`), which provides pnpm
- Docker with Docker Compose
- The three repositories cloned side by side:

```
projects/
├── shelfie-api/
├── shelfie-web/
└── shelfie/
```

## Running everything

The `docker-compose.yml` in this repo (to be added once both apps exist) starts PostgreSQL, the API, the worker and the web app, building from the sibling directories.

Until then, run each part from its own repo:

1. `shelfie-api`: `docker compose up -d` (PostgreSQL), then `pnpm install`, `pnpm db:migrate`, `pnpm db:seed`, `pnpm dev`. API on `http://localhost:3000`.
2. `shelfie-web`: `pnpm install`, copy `.env.example` to `.env.local` with `NEXT_PUBLIC_API_URL=http://localhost:3000`, then `pnpm dev`. App on `http://localhost:3001`.

## OAuth in development

Register separate **development** OAuth apps (Google, Discord, AniList...) with `localhost` redirect URIs. Never reuse production credentials locally.

## Environment variables

Each repo validates its environment at startup and documents every variable in `.env.example`. Secrets are never committed; generate local ones with `openssl rand -base64 32`.
