# 0006. Self-hosted authentication with Better Auth

- **Status:** Accepted
- **Date:** 2026-10-28

## Context

Users sign in with OAuth providers. Separately, they connect import accounts (AniList, Trakt, Spotify) whose tokens the worker must use. Both relate to the same user record.

## Decision

Better Auth, self-hosted in the API, storing users, sessions and login identities in PostgreSQL. Login providers: Google and Discord at first; Apple before any iOS app. Connected import accounts are a separate table and flow.

## Alternatives considered

- **Auth0:** mature, hosted, nothing to maintain; costs scale with active users, data lives outside our database, migration away is hard, and it doesn't help with import accounts.
- **Clerk:** similar trade-offs to Auth0; the easiest swap if self-hosting becomes a burden.

## Consequences

We own auth security. Required measures:

- Strong, per-environment `BETTER_AUTH_SECRET`; exact `trustedOrigins`
- HttpOnly, Secure, SameSite=Lax session cookies; CSRF prevention on GraphQL; strict CORS
- Account linking only with providers that verify email
- Connected-account tokens encrypted at rest, never exposed via GraphQL, decrypted only in the worker
- Rate limiting with correct client IPs behind proxies
- Prompt Better Auth updates (Dependabot, release watching)
- Security event logging without secrets
- Data export and account deletion (GDPR)
