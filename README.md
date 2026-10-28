# Shelfie (working name) — Platform

Shelfie tracks everything a person has read, watched and listened to — manga, webtoons, books, anime, movies, series, podcasts, albums and more — in one library, with imports from the services they already use.

This repository is the **platform repo**. It holds what belongs to neither the frontend nor the backend alone: the system overview, the API contract rules, onboarding, and the architecture decisions that shape both sides. Docs about one codebase live in that codebase.

## Repositories

| Repository | Contents |
| --- | --- |
| `shelfie-api` | Backend: GraphQL API, import worker, database schema, integrations (pnpm workspace) |
| `shelfie-web` | Frontend: Next.js (App Router) web app |
| `shelfie` (this repo) | Cross-cutting docs, ADRs, local full-stack setup, docs site |

## Documentation

- [System overview](docs/overview.md) — what the pieces are and how they connect
- [API contract](docs/api-contract.md) — how the frontend and backend agree on and evolve the GraphQL schema
- [Local development](docs/local-development.md) — running the whole stack on one machine
- [Roadmap](docs/roadmap.md) — milestones across both repos
- [Architecture decision records](docs/adr/README.md) — why the system is built the way it is

## Where does a doc go?

- It describes code in one repo → that repo's `README.md` or `docs/` folder, changed in the same pull request as the code.
- It describes how the repos work together, or a decision affecting both → this repo.
- It describes the GraphQL API's types and fields → schema descriptions in `shelfie-api`; the reference is generated, never hand-written.
