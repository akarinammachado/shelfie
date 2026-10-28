# 0011. Next.js with the App Router for the frontend

- **Status:** Accepted
- **Date:** 2026-10-28

## Context

The frontend needs interactive logged-in screens now and fast, shareable public pages (profiles) later.

## Decision

Next.js with the App Router and TypeScript. Interactive screens are Client Components using Apollo Client (via `@apollo/client-integration-nextjs`); public pages later use Server Components. Supporting choices: GraphQL Codegen, Better Auth client, Tailwind CSS with shadcn/ui, React Hook Form with Zod, MSW, Vitest, Playwright, Biome.

## Alternatives considered

- **React + Vite SPA:** simpler, with a more explicit API boundary; no server rendering for public pages.

## Consequences

- The frontend has its own server. Server Components must forward the session cookie to the API.
- Mocking requests from Server Components is harder than in the browser.
- Production must use our own domain, not the host's default, for first-party cookies.
