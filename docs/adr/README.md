# Architecture decision records

An ADR captures one significant decision: the context, what was decided, and what follows from it. They explain *why* the system looks the way it does, so nobody has to reverse-engineer it from code.

| # | Decision | Status |
| --- | --- | --- |
| [0001](0001-record-architecture-decisions.md) | Record architecture decisions | Accepted |
| [0002](0002-separate-repositories.md) | Separate frontend, backend and platform repositories | Accepted |
| [0003](0003-graphql-for-client-api.md) | GraphQL for the client API, REST for plumbing | Accepted |
| [0004](0004-backend-stack.md) | TypeScript backend with Hono, GraphQL Yoga and Pothos | Accepted |
| [0005](0005-postgresql-and-drizzle.md) | PostgreSQL with Drizzle ORM | Accepted |
| [0006](0006-self-hosted-auth-with-better-auth.md) | Self-hosted authentication with Better Auth | Accepted |
| [0007](0007-media-taxonomy-as-data.md) | Media taxonomy as data | Accepted |
| [0008](0008-external-catalogs.md) | External catalogs instead of an in-house catalog | Accepted |
| [0009](0009-background-jobs-with-pg-boss.md) | Background jobs with pg-boss | Accepted |
| [0010](0010-schema-registry-with-hive.md) | GraphQL Hive as schema registry | Accepted |
| [0011](0011-nextjs-app-router.md) | Next.js with the App Router for the frontend | Accepted |
| [0012](0012-docs-as-code.md) | Docs as code, aggregated into one site | Accepted |

## Writing a new ADR

1. Copy [`template.md`](template.md) to the next number, e.g. `0013-short-title.md`.
2. Open a pull request; discussion happens in review.
3. Merge as **Accepted**. Never rewrite an accepted ADR: to change a decision, write a new ADR and mark the old one **Superseded by 00NN**.
