# Standard: Next.js

## Rules

### Components

- Use Server Components by default; opt into Client Components only when browser APIs or interactivity are required
- Mark Client Components with `"use client"` at the top of the file — never bury it after imports
- TypeScript strict mode required (`"strict": true` in tsconfig)
- No implicit `any`; no `as any` casts without an inline justification comment
- Named exports only — no default exports

### Routing and Data Fetching

- App Router only — no Pages Router patterns in new code
- Fetch data in Server Components where possible; avoid client-side fetching for initial page load
- Use React Server Actions for mutations; do not write custom POST handlers for form submissions

### API Routes

- Validate all inputs with Zod before any business logic runs
- Return consistent error shape: `{ error: string, code: string }`
- Authenticate and authorise before accessing any data
- No business logic in route handlers — delegate to `lib/` service functions

### State

- No global client state libraries unless justified by an ADR
- Prefer URL state (search params) and Server Component re-renders over client state

## Rationale

Server Components reduce client bundle size and move sensitive logic off the client. Consistent API error shapes make error handling predictable across the frontend.

## Examples

See the `app/` and `lib/` directories in this example for compliant patterns.
