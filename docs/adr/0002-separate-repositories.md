# 0002. Separate frontend, backend and platform repositories

- **Status:** Accepted
- **Date:** 2026-10-28

## Context

The frontend and backend could live in one monorepo, which is simpler for a single developer: one pull request per feature and shared types. However, a goal of this project is to practise working like two teams, including the friction between them.

## Decision

Three repositories in one GitHub organization:

- `shelfie-api` — backend (itself a pnpm workspace: API, worker, db, integrations)
- `shelfie-web` — frontend
- `shelfie` — cross-cutting docs, ADRs, full-stack local setup

## Alternatives considered

- **Monorepo:** atomic cross-stack changes and shared code, but hides the contract problems this project wants to learn.
- **Wrapper repo with git submodules:** pinned commits go stale and confuse clones.

## Consequences

- The GraphQL schema becomes an explicit contract with its own tooling ([ADR 0010](0010-schema-registry-with-hive.md)).
- Cross-repo features need coordination: schema-first PRs, linked issues, API-first deploys.
- Some configuration (Biome, CI patterns) is duplicated across repos.
- Production cookies require both apps on one registrable domain.
