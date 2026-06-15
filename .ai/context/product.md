# Product

## Purpose

Engineering AI Foundation is a deterministic, AI-agnostic operating system for engineering repositories. It defines how AI systems should structure, interpret, and modify software engineering codebases, giving all AI tools a shared contract rather than allowing each to invent its own conventions.

## Users

- AI systems operating inside target repositories (Claude, Cursor, Copilot, ChatGPT, Gemini, etc.)
- Engineering teams adopting the foundation to standardize AI behaviour across their repos
- Repository owners bootstrapping new projects or migrating existing ones

## Core Features

- `spec/` — machine-readable contracts (schemas, agent registry, structure rules) that AI systems must follow
- `templates/` — files copied verbatim into target repos during bootstrap
- `bootstrap/` — step-by-step workflows for creating, upgrading, and auditing repos
- `standards/` — language-agnostic engineering constraints (coding, testing, security)
- `examples/` — reference implementations showing the foundation applied to real project types
- `migration-guides/` — upgrade logic for bringing legacy repos into the foundation

## Non Goals

- This is not a framework for building applications
- This is not a CI/CD system or deployment pipeline
- This repo does not contain runnable production code
- The foundation does not enforce rules at commit time — it relies on AI systems reading and following the spec

## Dependencies

- No runtime dependencies
- `package.json` exists for tooling only (linting, validation scripts)

## Success Metrics

- AI systems operating in a foundation-bootstrapped repo produce structurally consistent outputs across sessions and tools
- Bootstrap audit passes with zero errors on all example repos
- Spec files parse without errors
- Migration guides successfully upgrade repos from prior foundation versions
