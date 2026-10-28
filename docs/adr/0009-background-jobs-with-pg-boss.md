# 0009. Background jobs with pg-boss

- **Status:** Accepted
- **Date:** 2026-10-28

## Context

Imports can take minutes, hit rate limits and fail partway. They must not run inside API requests.

## Decision

pg-boss, a job queue stored in PostgreSQL, consumed by a separate worker process. Imports are idempotent (upsert by external ID) and retried with backoff.

## Alternatives considered

- **BullMQ with Redis:** mature and fast, but adds Redis to operate before it's needed.
- **In-process jobs:** lost on restart; compete with API traffic.

## Consequences

- No extra infrastructure.
- Revisit if job volume outgrows PostgreSQL.
