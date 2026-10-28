# API contract

The GraphQL schema is the agreement between `shelfie-api` and `shelfie-web`. The two deploy independently, so the frontend in production will sometimes be older or newer than the API. These rules keep that safe.

## Publishing the schema

- The schema registry is **GraphQL Hive**. It stores every schema version and records which fields the frontend actually queries.
- `shelfie-api` CI exports `schema.graphql`, commits it, and publishes it to Hive on every merge to `main`.
- On every API pull request, CI runs Hive's schema check against `main`. Breaking changes fail the check unless explicitly approved.
- `shelfie-web` generates types with GraphQL Codegen from the registry and reports its operations to Hive, so checks know which fields are in use.
- `shelfie-web` CI regenerates types and fails if they changed but weren't committed.

## Evolving the schema

- **Additive changes are always safe.** New types, new fields and new optional arguments never break clients.
- **Deprecate before removing.** Mark the field `@deprecated(reason: "Use progress.current")`. Remove it only after Hive shows no usage.
- **Rename with expand and contract.** Add the new field → move the frontend to it → remove the old field in a later release.
- **Never add a required argument** to an existing field; add an optional one with a default.
- **Deploy order:** when a feature spans both repos, the API deploys first.
- **Describe everything.** Every type and field has a description in the schema; it is the API reference.

## Conventions

- Relay global IDs and the `Node` interface; cursor pagination (`first` / `after`) for every list that can grow.
- Mutations take one `input` argument and return the changed object.
- Enums in `SCREAMING_SNAKE_CASE`, fields in `camelCase`, types in `PascalCase`.
- Errors a user can act on are returned as typed results; unexpected failures are GraphQL errors.

## Working in parallel

1. **Schema first.** A feature starts as an API pull request containing only schema changes, reviewed by the frontend side before any resolver is written.
2. **Mock.** Once merged, the frontend builds against MSW mocks generated from the schema.
3. **Implement.** The backend implements resolvers behind the agreed schema.
4. **Integrate.** Test end to end with the local full stack (see [local development](local-development.md)).
5. **Track.** Cross-repo features are linked issues on the organization's shared GitHub Projects board.

## Domains and cookies

- Production frontend and API share one registrable domain: `app.<domain>` and `api.<domain>`.
- Better Auth uses cross-subdomain cookies for that domain.
- The API allows the frontend's exact origin in CORS (with credentials) and in Better Auth's `trustedOrigins`, per environment. No wildcards.
- Requests from Next.js Server Components forward the session cookie explicitly; Client Components send it with `credentials: "include"`.
- Login working on `localhost` proves nothing about production cookies. Verify on a staging deployment before launch.
