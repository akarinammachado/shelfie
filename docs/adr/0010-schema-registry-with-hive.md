# 0010. GraphQL Hive as schema registry

- **Status:** Accepted
- **Date:** 2026-10-28

## Context

With separate repositories ([ADR 0002](0002-separate-repositories.md)), the frontend needs a reliable source for the schema, and the backend needs to know whether a change breaks the frontend.

## Decision

GraphQL Hive is the schema registry. The API publishes on merge to `main` and checks every pull request; the frontend generates types from it and reports its operations. Rules are in [the API contract](../api-contract.md).

## Alternatives considered

- **Introspection from a staging API:** requires a running deployment; no usage data.
- **Schema file in GitHub releases:** works, but no breaking-change checks against real usage.
- **GraphQL Inspector alone:** detects breaking changes, but without usage data.
- **Apollo GraphOS:** comparable, tied to the Apollo ecosystem.

## Consequences

- A third-party service in the delivery pipeline (free tier).
- Removals are safe only when Hive shows no usage.
