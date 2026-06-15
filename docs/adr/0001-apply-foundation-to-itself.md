# ADR 0001: Apply the Engineering AI Foundation to Itself

## Status

accepted

## Context

The Engineering AI Foundation defines a standard operating structure for AI systems working in engineering repositories. The foundation repo itself had no `.ai/` directory, no `AGENTS.md`, and no context files — meaning AI systems opening this repo had no contract to follow, contradicting the purpose of the project.

## Decision

Bootstrap the foundation repo using its own spec and bootstrap workflow (`bootstrap/create-new-project.md` adapted for `repo_type: migrated`). This creates the full `.ai/` structure, `AGENTS.md`, `.aiignore`, manifests, context files, and agent definitions within this repository.

All seven agents from `spec/agent-registry.yaml` are activated, since maintaining the foundation requires the full range: planning spec changes, making architectural decisions, implementing updates, reviewing changes, validating correctness, keeping docs current, and managing releases.

## Consequences

- AI systems opening this repo now load `AGENTS.md` first and follow the same contract they would in any foundation-bootstrapped repo
- Future spec changes to this repo must follow the same workflow as any other foundation repo (task → ADR if architectural → implement → review → release)
- The foundation version recorded in `.ai/manifests/foundation.yaml` must be updated when the spec version changes
