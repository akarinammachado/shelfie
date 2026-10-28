# 0005. PostgreSQL with Drizzle ORM

- **Status:** Accepted
- **Date:** 2026-10-28

## Context

The data is relational: users, entries, works and relations between works, with constraints that must hold (one entry per user per work, one work per external ID) and writes that must be atomic (an entry and its activity event). Media-specific metadata varies by type.

## Decision

PostgreSQL 18 as the only datastore, with Drizzle ORM and drizzle-kit migrations. Medium-specific metadata goes in jsonb columns. Search starts with Postgres full-text search.

## Alternatives considered

- **MongoDB:** flexible documents, but the data is cross-referenced and needs relational constraints and joins; jsonb covers the flexibility.
- **MySQL:** viable, weaker JSON and full-text support.
- **SQLite / Turso:** less comfortable with a concurrent background worker.
- **Prisma:** good, but Drizzle stays closer to SQL and its migrations are readable SQL.

## Consequences

- Constraints in the database make imports idempotent.
- One datastore to operate; the job queue lives here too ([ADR 0009](0009-background-jobs-with-pg-boss.md)).
- A dedicated search engine may be needed once the catalog grows.
