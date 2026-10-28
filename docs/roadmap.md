# Roadmap

## Milestone 1 — first real user

Done when one person can sign in, import their AniList history, fix mismatches, and update progress on something they're watching.

### shelfie-api

- [ ] Workspace, tooling and Docker PostgreSQL running; `/health` responds
- [ ] CI green; secret scanning and push protection on
- [ ] Core schema migrated; media types seeded
- [ ] Google and Discord login; user handle required
- [ ] Ownership checks and shared visibility rule, with cross-user access tests
- [ ] `searchWorks`, `addToLibrary`, `updateLibraryEntry`, `myLibrary` with pagination
- [ ] Every library mutation writes an activity event
- [ ] CSRF prevention, CORS allowlist, rate limits and security headers
- [ ] Schema published to Hive on merge; breaking-change check on PRs
- [ ] AniList connect, import and review queue; tokens encrypted at rest
- [ ] Goodreads CSV import through the same matcher, with upload limits
- [ ] Before launch: security event logging, session management, data export, account deletion

### shelfie-web

- [ ] Next.js app, Biome, Vitest and CI
- [ ] Codegen from Hive; Apollo provider sending credentials
- [ ] Server-side cookie forwarding helper
- [ ] MSW mocks generated from the schema
- [ ] Sign-in, protected routes and handle form against the local API
- [ ] Search, library, entry editor, import and review queue screens
- [ ] Playwright end-to-end tests for the main flows

### shelfie

- [ ] Docs site aggregating all three repos' docs
- [ ] Full-stack `docker-compose.yml`
- [ ] Production domains chosen; cross-subdomain cookies verified on staging

## Later, in rough order

1. TMDB and Trakt for movies and series; Open Library for books
2. Personal stats from the activity log
3. Public profiles, rendered with Server Components
4. Following and activity feed
