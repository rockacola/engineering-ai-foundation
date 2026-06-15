# 0001 — Auth Strategy

## Status

accepted

## Context

The application requires user authentication with workspace-level access control. Three options were evaluated:

1. **Custom JWT** — full control, high implementation cost, no session management out of the box
2. **NextAuth.js** — open-source, integrates natively with Next.js, supports database sessions
3. **Clerk** — managed auth service, fast to implement, per-seat cost at scale

The team is small, scale is unknown, and minimising third-party dependencies was preferred where cost is a factor.

## Decision

Use NextAuth.js with a credentials provider backed by the PostgreSQL user table. Sessions stored as database sessions (not stateless JWTs) to enable server-side revocation.

## Consequences

- Session validation runs a database read on every protected request — acceptable at current scale
- Password reset and email verification flows must be implemented in-house
- No per-seat vendor cost
- Migrating to a managed auth provider later is possible — NextAuth adapters are swappable
