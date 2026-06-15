# packages/shared

Shared TypeScript types and Zod validation schemas consumed by both `packages/api` and `packages/web`.

## Rules

- Zero runtime dependencies — this package is consumed at build time only
- All cross-package type sharing must go through this package
- Breaking changes to exported types require updating both `api` and `web` consumers before merging
