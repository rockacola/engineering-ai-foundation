# Architecture Context

## System Overview

Next.js application using the App Router. API routes handle all server-side logic. PostgreSQL accessed via Prisma ORM. Deployed to Vercel. Authentication via NextAuth with database sessions.

## Components

- `app/` — App Router pages, layouts, and Server Components
- `app/api/` — API route handlers (REST endpoints)
- `components/` — Reusable React components (client and server)
- `lib/` — Business logic, service clients, and shared utilities
- `lib/db/` — Prisma client instance and query helpers
- `prisma/` — Schema definition and migrations

## Data Flow

1. Request arrives at a Next.js page or API route
2. NextAuth middleware validates the session cookie
3. Authenticated request passes to a service function in `lib/`
4. Service function runs a Prisma query against PostgreSQL
5. Response returned to client as rendered HTML (pages) or JSON (API routes)

## External Services

- **Stripe** — subscription lifecycle, invoice management, and payment processing
- **Resend** — transactional email (invitations, task notifications, billing receipts)
- **Vercel** — hosting, edge middleware, preview deployments

## Deployment Model

- Production: Vercel, auto-deployed from `main` branch
- Preview: Vercel preview deployment per pull request
- Database: Managed PostgreSQL on Supabase (connection pooling via PgBouncer)
- Secrets: managed in Vercel environment variable settings, not committed to the repo

## Constraints

- All database access must go through Prisma — no raw SQL
- No sensitive data in Client Components or client-side code
- All API routes validate input with Zod before reaching business logic
- Session validation runs server-side on every protected route
