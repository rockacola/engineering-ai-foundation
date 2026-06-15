# AI Bootstrap

This file is the mandatory entry point for all AI systems operating in this repository.
Load this file first before any other context.

## Load Order

1. Standards — `.ai/standards/`
2. Context — `.ai/context/` (follow sequence in `.ai/manifests/context.yaml`)
3. Memory — `.ai/memory/`
4. Tasks — `.ai/tasks/active/` (active and blocked tasks; completed tasks are archived in `.ai/tasks/completed/`)

## Rules

- Follow spec strictly. No structural invention.
- Do not create files not defined in `spec/file-schemas.yaml`.
- Do not activate agents not listed in `.ai/manifests/agents.yaml`.
- Use `.ai/manifests/context.yaml` to determine which context files to load and in what order.
- Record all decisions in `.ai/journal/{YYYY}/{today}.md`.
- All architectural decisions require an ADR in `docs/adr/`.
- Do not modify `.ai/manifests/foundation.yaml` after initial setup.

## Active Agents

See `.ai/manifests/agents.yaml`.

## Ownership

See `.ai/manifests/ownership.yaml`.

## Foundation Version

See `.ai/manifests/foundation.yaml`. Rules in this file follow the spec version recorded there. On upgrade, replace this file with the version from the new foundation release.

## Project-Specific Rules

- This is a CLI tool — there is no web server, no persistent process, and no frontend.
- All commands must exit with a non-zero code on any failure. Callers depend on exit codes.
- Destructive operations (credential rotation, migrations) must prompt for confirmation unless `--yes` is passed.
- Active agents are limited to `implementer` and `reviewer`. See `.ai/manifests/agents.yaml`. Do not invoke disabled agents.

## Git

- **Never commit without explicit instruction from the operator.** Stage changes, show a `git diff --stat` summary, and wait for confirmation before creating a commit.
- Commit message format: single-line conventional commits, no body.
- Permitted types: `feat`, `fix`, `docs`, `refactor`, `chore`, `test`
- Example: `feat: add dry-run flag to migrate command`
- Never add `Co-Authored-By` to commit messages.
- When changing code, update relevant documentation in the same commit. Do not leave docs out of sync with the implementation.
