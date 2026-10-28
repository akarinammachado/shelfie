# 0012. Docs as code, aggregated into one site

- **Status:** Accepted
- **Date:** 2026-10-28

## Context

Documentation spans three repositories. Docs kept apart from code drift; readers still want one place to browse everything.

## Decision

- Each repo documents itself in `README.md` and `docs/`, updated in the same pull request as the code.
- Cross-cutting docs and ADRs live in `shelfie`.
- A docs site (Starlight or Docusaurus) in `shelfie` fetches the other repos' `docs/` folders at build time. The other repos trigger a rebuild via `repository_dispatch` when their docs change on `main`.
- The GraphQL reference is generated from schema descriptions, never hand-written.

## Alternatives considered

- **Git submodules:** pinned commits go stale; confusing clones.
- **All docs in the platform repo:** drift from code.
- **GitHub wiki:** outside code review.

## Consequences

- Docs are reviewed with code.
- Cross-repo CI needs a token permitted to dispatch events to `shelfie`.
