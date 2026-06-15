# ADR 0001: Apply the Engineering AI Foundation to Itself

## Status

accepted

## Context

The Engineering AI Foundation defines a standard operating structure for AI systems working in engineering repositories. The foundation repo itself had no `.ai/` directory, no `AGENTS.md`, and no context files — meaning AI systems opening this repo had no contract to follow, contradicting the purpose of the project.

## Decision

Bootstrap the foundation repo using its own spec and bootstrap workflow (`bootstrap/create-new-project.md` adapted for `repo_type: migrated`). This creates the full `.ai/` structure, `AGENTS.md`, `.aiignore`, manifests, context files, and agent definitions within this repository.

Five of the seven registered agents are activated: `architect`, `implementer`, `reviewer`, `docs`, and `release`. `planner` is omitted because this repo rarely has enough parallel work to warrant formal task decomposition. `qa` is omitted because validation here is running `audit-project.md` inline — reviewer and implementer handle that without a dedicated agent.

## Consequences

- AI systems opening this repo now load `AGENTS.md` first and follow the same contract they would in any foundation-bootstrapped repo
- Future spec changes to this repo must follow the same workflow as any other foundation repo (task → ADR if architectural → implement → review → release)
- The foundation version recorded in `.ai/manifests/foundation.yaml` must be updated when the spec version changes
