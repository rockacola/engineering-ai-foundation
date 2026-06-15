# 0001 — Monorepo Tooling

## Status

accepted

## Context

The platform requires a `shared` package consumed by both `api` and `web`. Options for monorepo tooling were evaluated:

1. **npm workspaces** — built-in, no additional tooling, slower installs
2. **pnpm workspaces** — fast installs, strict dependency isolation by default, growing adoption
3. **Turborepo + pnpm** — adds task orchestration and caching on top of pnpm workspaces
4. **Nx** — full monorepo platform, high configuration overhead for three packages

The repo has three packages with low inter-dependency complexity.

## Decision

Use pnpm workspaces without Turborepo. The build graph is simple enough that task orchestration tooling adds overhead without clear benefit at this scale. Revisit when package count exceeds five or CI build times exceed 10 minutes.

## Consequences

- Fast, deterministic installs with pnpm's content-addressable store
- Strict hoisting prevents accidental cross-package dependency leakage
- No task caching — each CI run rebuilds from scratch
- Adding Turborepo later is additive and non-breaking
