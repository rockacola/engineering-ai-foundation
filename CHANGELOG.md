# Changelog

All notable changes to this project will be documented here.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/). Versions follow [Semantic Versioning](https://semver.org/).

---

## [1.1.0] — 2026-06-18

### Changed

- `bootstrap/upgrade-existing-project.md`: removed human approval gate at Step 5 -- plan is logged to migration report and execution continues automatically
- `bootstrap/upgrade-existing-project.md`: Step 7a now overwrites existing standards files with the foundation version (previously skipped them); git diff is the review mechanism
- `bootstrap/upgrade-existing-project.md`: Step 10 now spawns a sub-agent with clean context to run the audit, isolating it from accumulated migration context
- `AGENTS.md`: added `Critical Rules` section at the top of the file with explicit, high-priority behavioral rules (git commit, co-authored-by, writing style)

---

## [1.0.2] — 2026-06-16

### Changed

- Removed redundant `version:` header from all `spec/*.yaml` files — version is now sourced exclusively from `package.json`
- Replaced hardcoded version literals in `bootstrap/create-new-project.md` and `bootstrap/upgrade-existing-project.md` with `{foundation_version}` placeholders
- Updated `templates/.ai/manifests/foundation.yaml` to use `{foundation_version}` placeholder populated by bootstrap
- Updated `examples/*/foundation.yaml` to use mock version `1.2.3` with comment, so examples never drift with releases
- Added `# keep in sync with package.json` comment to `.ai/manifests/foundation.yaml`

---

## [1.0.1] — 2026-06-16

### Changed

- Merged `spec/versioning.yaml` and `spec/migration-rules.yaml` into `spec/governance.yaml` — same content, one fewer file to load
- Removed `templates/.ai/standards/coding.md`, `testing.md`, `security.md` — drifted copies; bootstrap step 7a copies from `standards/` directly
- Removed redundant `.gitkeep` files from `templates/.ai/skills/` and `templates/.ai/memory/` (directories have real content)
- Corrected `docs/adr/0001` to accurately reflect the five active agents (not seven)

---

## [1.0.0] — 2024-01-15

### Added

- `spec/repo-structure.yaml` — required folder and file layout
- `spec/file-schemas.yaml` — schemas for all `.ai/` file types
- `spec/manifest-schema.yaml` — schemas for all `.ai/manifests/` files
- `spec/agent-registry.yaml` — seven defined agent roles with inputs, outputs, and constraints
- `spec/governance.yaml` — semver versioning policy and migration execution rules
- `templates/` — ready-to-copy scaffold for new repositories
- `bootstrap/create-new-project.md` — workflow for scaffolding a new repo
- `bootstrap/audit-project.md` — read-only validation workflow
- `bootstrap/upgrade-existing-project.md` — migration workflow for existing repos
- `bootstrap/generate-context.md` — workflow for extracting `.ai/context/` from a repo
- `standards/coding.md`, `standards/testing.md`, `standards/security.md` — universal engineering standards
- `examples/nextjs-saas/` — Next.js SaaS reference structure
- `examples/internal-tool/` — Node.js CLI reference structure
- `examples/monorepo/` — pnpm workspace monorepo reference structure
