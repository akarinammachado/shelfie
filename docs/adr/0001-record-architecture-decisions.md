# 0001. Record architecture decisions

- **Status:** Accepted
- **Date:** 2026-10-28

## Context

The project is built to mimic separate teams working on separate repositories. Decisions that affect both sides are easily lost in chat threads, and later contributors (including future us) need to know why things are the way they are.

## Decision

Significant decisions are recorded as ADRs in `shelfie/docs/adr`, one decision per file, numbered sequentially. Decisions affecting only one repo may be recorded in that repo's `docs/adr` using the same format.

## Alternatives considered

- **Wiki pages:** live outside code review and drift.
- **Nothing:** the reasoning disappears.

## Consequences

- Every significant decision needs a short write-up and a review.
- Accepted ADRs are immutable; changes require a superseding ADR.
