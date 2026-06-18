# Migration Guides

This directory contains step-by-step upgrade guides for moving a repository from one foundation version to another.

## Naming convention

```
{from-version}-to-{to-version}.md
```

Example: `1.0.0-to-2.0.0.md`

## When a guide is required

A migration guide is required whenever the foundation version bump is **major** (breaking change). See `spec/governance.yaml` for the definition of breaking vs. non-breaking changes.

Minor and patch upgrades do not require a guide — existing repos remain valid without migration.

## Guide structure

Each guide must include:

1. **Summary** — what changed and why
2. **Pre-migration checklist** — things to verify before starting
3. **Step-by-step migration** — references `bootstrap/upgrade-existing-project.md` and adds version-specific overrides
4. **Post-migration validation** — run `bootstrap/audit-project.md` and confirm zero errors
5. **Rollback instructions** — how to revert if the migration fails

## Current status

No migration guides exist yet. The foundation is at version `1.1.1`.

The first guide will be written when a breaking change is introduced.
