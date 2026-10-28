# 0004. TypeScript backend with Hono, GraphQL Yoga and Pothos

- **Status:** Accepted
- **Date:** 2026-10-28

## Context

A small team needs a productive, well-documented backend stack, preferably in the same language as the frontend.

## Decision

- Node.js 24 LTS, TypeScript in strict mode
- pnpm workspaces for the backend repo
- Hono as HTTP server, hosting GraphQL, auth and REST routes side by side
- GraphQL Yoga as GraphQL server
- Pothos for a code-first, fully typed schema (Relay, Drizzle and scope-auth plugins)
- Zod for validating env, inputs and external payloads
- Biome for linting and formatting; Vitest and Testcontainers for tests

## Alternatives considered

- **npm workspaces:** works, but looser dependency resolution allows undeclared imports.
- **Fastify:** equally good; Hono chosen for Web Standards APIs, which Yoga and Better Auth plug into directly, and runtime portability.
- **Express:** older design, weaker typing. **NestJS:** heavy for this project.
- **Apollo Server:** strong, but its advantages (GraphOS, Federation) aren't needed; Yoga is lighter with a flexible plugin system.
- **ESLint + Prettier:** larger plugin ecosystem and deeper type-aware rules; Biome chosen for speed and one config. Revisit if a missing rule hurts.

## Consequences

- One language across the system.
- Pothos types flow from database to schema without server-side codegen.
- Biome may lack some type-aware lint rules.
