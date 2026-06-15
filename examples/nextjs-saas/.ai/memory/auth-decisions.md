---
last_updated: 2024-01-15
---

# Memory: Auth Decisions

## Summary

Key constraints and learned facts about the authentication setup in this project. Supplements ADR 0001 with operational detail discovered during implementation.

## Key Facts

- NextAuth.js is configured with a credentials provider backed by the `users` PostgreSQL table.
- Sessions are stored as database sessions (not stateless JWTs) to support server-side revocation.
- Session validation runs a database read on every protected request — acceptable at current scale, revisit if latency becomes an issue.
- Password reset and email verification flows are implemented in-house (no third-party magic link service).
- The NextAuth adapter is swappable — migrating to Clerk or Auth0 later is structurally possible.

## References

- ADR 0001: `docs/adr/0001-auth-strategy.md`
- Architecture context: `.ai/context/architecture.md` (Authentication section)
