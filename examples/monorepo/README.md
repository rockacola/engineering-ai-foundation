# Example: Monorepo

Reference implementation of Engineering AI Foundation compliance for a monorepo with multiple independently deployable packages.

The scenario is an internal developer platform with a Fastify API (`packages/api`), a React dashboard (`packages/web`), and shared types (`packages/shared`).

## What this example demonstrates

- Ownership manifest split across packages and teams
- Architecture context that explains cross-package constraints
- An agent manifest with all seven agents active
- Example task involving a cross-package change
- An ADR documenting the monorepo tooling decision

## Structure

```
monorepo/
├── AGENTS.md
├── .ai/
│   ├── manifests/
│   │   ├── foundation.yaml
│   │   ├── context.yaml
│   │   ├── ownership.yaml
│   │   └── agents.yaml
│   ├── context/
│   │   ├── product.md
│   │   └── architecture.md
│   └── tasks/
│       └── task-001.yaml
├── docs/
│   └── adr/
│       └── 0001-monorepo-tooling.md
└── packages/
    ├── api/
    ├── web/
    └── shared/
```

## Notes

This is a reference scaffold, not a runnable application. Pay particular attention to how the `architecture.md` documents cross-package constraints — this is what stops an AI system from importing `packages/api` source directly into `packages/web`.
