# 0003. GraphQL for the client API, REST for plumbing

- **Status:** Accepted
- **Date:** 2026-10-28

## Context

The app serves many media types sharing common fields with type-specific extras. Data is graph-shaped (users → entries → works → related works, later users → users). Different screens need very different slices of the same data.

## Decision

All client data access goes through one GraphQL endpoint. OAuth redirects and callbacks, file uploads and webhooks are plain REST routes on the same server.

## Alternatives considered

- **REST only:** works, but many endpoint variants for compact vs detailed views of heterogeneous media.
- **tRPC:** excellent with a single TypeScript client, weaker for future native clients or a public API.

## Consequences

- Interfaces and fragments model media types cleanly.
- Must guard against expensive queries: depth, alias and complexity limits; rate limiting.
- Must avoid N+1 queries with batching (DataLoader or the Pothos Drizzle plugin).
- Import progress is exposed as a GraphQL `ImportJob` type that clients poll.
