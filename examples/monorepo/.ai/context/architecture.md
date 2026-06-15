# Architecture Context

## System Overview

pnpm workspace monorepo with three packages: `api`, `web`, and `shared`. The `shared` package contains TypeScript types and validation schemas consumed by both `api` and `web`. Packages are independently deployable.

## Components

- `packages/api/` — Fastify REST API, handles auth and all data operations
- `packages/web/` — React + Vite dashboard, communicates with `api` over HTTP
- `packages/shared/` — Shared TypeScript types and Zod schemas; no runtime dependencies

## Data Flow

1. Web dashboard sends HTTP requests to the API
2. API authenticates the request via JWT (issued at login)
3. Validated request runs a query against PostgreSQL
4. Response returned as JSON; shared types ensure web and API stay in sync
5. Deployment events are polled by the dashboard every 5 seconds (no WebSocket in v1)

## External Services

- **PostgreSQL** — primary data store, managed on AWS RDS
- **GitHub Actions** — CI/CD; triggers deployment jobs on merge to `main`

## Deployment Model

- `packages/api/` — deployed as a Docker container on AWS ECS (Fargate)
- `packages/web/` — deployed as a static site to AWS S3 + CloudFront
- Deployments are independent per package; a change to `web` does not redeploy `api`
- `packages/shared/` — not deployed; consumed at build time by api and web

## Constraints

- `packages/shared/` must have zero runtime dependencies
- `packages/web/` must not import directly from `packages/api/` source — use the HTTP API only
- All cross-package type sharing must go through `packages/shared/`
- Breaking changes to `packages/shared/` types require updating both consumers before merging
