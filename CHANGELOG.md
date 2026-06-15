# Changelog

All notable changes to this project will be documented here.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/). Versions follow [Semantic Versioning](https://semver.org/).

---

## [1.0.0] — 2024-01-15

### Added

- `spec/repo-structure.yaml` — required folder and file layout
- `spec/file-schemas.yaml` — schemas for all `.ai/` file types
- `spec/manifest-schema.yaml` — schemas for all `.ai/manifests/` files
- `spec/agent-registry.yaml` — seven defined agent roles with inputs, outputs, and constraints
- `spec/migration-rules.yaml` — blocking and recommended rules for repo migration
- `spec/versioning.yaml` — semver scheme with breaking/non-breaking/patch classification
- `templates/` — ready-to-copy scaffold for new repositories
- `bootstrap/create-new-project.md` — workflow for scaffolding a new repo
- `bootstrap/audit-project.md` — read-only validation workflow
- `bootstrap/upgrade-existing-project.md` — migration workflow for existing repos
- `bootstrap/generate-context.md` — workflow for extracting `.ai/context/` from a repo
- `standards/coding.md`, `standards/testing.md`, `standards/security.md` — universal engineering standards
- `examples/nextjs-saas/` — Next.js SaaS reference structure
- `examples/internal-tool/` — Node.js CLI reference structure
- `examples/monorepo/` — pnpm workspace monorepo reference structure
