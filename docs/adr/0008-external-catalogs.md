# 0008. External catalogs instead of an in-house catalog

- **Status:** Accepted
- **Date:** 2026-10-28

## Context

Maintaining metadata for millions of titles is impossible for a small team. Good public sources exist for most media; coverage for webtoons is poor.

## Decision

Pull catalog metadata from external sources and cache it locally, keyed by `external_ids`:

- Anime and manga: AniList, MyAnimeList
- Movies and series: TMDB, Trakt
- Books: Open Library, Google Books, Hardcover
- Comics: Comic Vine
- Music and podcasts: Spotify

Users can create their own Works for anything missing.

## Alternatives considered

- **Own catalog:** unmaintainable.
- **Live lookups without caching:** slow, rate-limited, fragile.

## Consequences

- Each provider's terms must be checked for caching and commercial use.
- Imports need matching; ambiguous matches go to a user review queue rather than being guessed.
- Background refresh keeps cached metadata current.
