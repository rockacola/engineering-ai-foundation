# Engineering AI Foundation

A deterministic, AI-agnostic operating system for engineering repositories.

This is not a project repository. It is a **specification + template system** that defines how AI systems should structure, interpret, and modify software engineering codebases.

---

## What it does

When you apply this foundation to a repository, AI systems (Claude, Cursor, Copilot, ChatGPT, Gemini, etc.) gain a shared contract for how to operate in that repo — what files exist, what agents are allowed to do, what standards to follow, and how to record decisions.

AI systems are not permitted to invent structure. All structural decisions must derive from `spec/`.

---

## Repository layout

| Folder              | Purpose                                                               |
| ------------------- | --------------------------------------------------------------------- |
| `spec/`             | Machine-readable contracts (schemas, agent registry, structure rules) |
| `templates/`        | Files copied verbatim into new repos                                  |
| `bootstrap/`        | Step-by-step workflows for creating, upgrading, and auditing repos    |
| `standards/`        | Engineering constraints (coding, testing, security)                   |
| `examples/`         | Reference implementations (Next.js SaaS, internal tool, monorepo)     |
| `migration-guides/` | Upgrade logic for bringing legacy repos into the foundation           |

---

## What gets added to your repo

Applying the foundation creates a `.ai/` directory with this structure:

```
.ai/
  manifests/     # foundation version, context load order, ownership
  agents/        # per-agent configuration
  context/       # architecture, decisions, domain knowledge
  standards/     # inherited engineering constraints
  skills/        # reusable AI workflows
  memory/        # persistent AI memory across sessions
  journal/       # daily decision log
  tasks/         # structured task definitions
docs/
  adr/           # architecture decision records
AGENTS.md        # AI entry point — loaded first by all AI systems
.aiignore        # files AI systems must not read or modify
```

---

## Getting started

> **How to run bootstrap workflows**
>
> All bootstrap workflows must be run from inside the **target repository** — that is, open your AI session in the repo you want to create, upgrade, or audit. The bootstrap files live here in the foundation repo, so reference them by their absolute path in your prompt.
>
> Replace `/path/to/engineering-ai-foundation` with the actual path where you cloned this repo.

### New repository

Open an AI session inside the new (empty) repo, then prompt:

```
Follow /path/to/engineering-ai-foundation/bootstrap/create-new-project.md to scaffold this repo.
```

The workflow loads the spec, creates the folder structure, copies templates, and runs an audit to confirm zero errors before handing off.

### Existing repository

Open an AI session inside the target repo, then prompt:

```
Follow /path/to/engineering-ai-foundation/bootstrap/upgrade-existing-project.md to apply the foundation to this repo.
```

The workflow will produce a mapping plan and pause for your approval before making any changes.

### Audit a repo

Open an AI session inside the repo you want to audit, then prompt:

```
Follow /path/to/engineering-ai-foundation/bootstrap/audit-project.md to audit this repo.
```

The audit is read-only and produces a structured report of passes, failures, and warnings.

---

## Defined agents

The foundation ships with seven agent roles. Each has declared inputs, outputs, and constraints:

| Agent         | Responsibility                           |
| ------------- | ---------------------------------------- |
| `planner`     | Decomposes goals into tasks              |
| `architect`   | Defines structure and records ADRs       |
| `implementer` | Writes and modifies code                 |
| `reviewer`    | Reviews diffs against standards          |
| `qa`          | Validates against acceptance criteria    |
| `docs`        | Generates and maintains documentation    |
| `release`     | Manages versioning and release artifacts |

Agents are registered in `spec/agent-registry.yaml`. AI systems may not activate agents not listed there.

---

## Design principles

- **Determinism over creativity** — structure comes from spec, not inference
- **Separation of concerns** — each layer has exactly one responsibility
- **AI vendor neutrality** — no vendor-specific assumptions anywhere in the spec
