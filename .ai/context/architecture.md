# Architecture

## System Overview

The Engineering AI Foundation is a specification-driven template system. It is not deployed as a service. AI systems consume it by reading the spec and applying bootstrap workflows to target repositories. The output is a `.ai/` directory inside those target repos.

## Components

| Component           | Path                | Role                                                                                                                       |
| ------------------- | ------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| Spec                | `spec/`             | Machine-readable contracts defining permitted structure, agent roles, manifest schemas, file schemas, and versioning rules |
| Templates           | `templates/`        | Files copied verbatim into target repos during bootstrap (AGENTS.md, .aiignore, initial .ai/ files)                        |
| Bootstrap workflows | `bootstrap/`        | Step-by-step instructions AI systems follow to create, upgrade, or audit a repo                                            |
| Standards           | `standards/`        | Language-agnostic engineering constraints inherited by all foundation repos                                                |
| Examples            | `examples/`         | Reference implementations showing the foundation applied to Next.js SaaS, internal tools, and monorepos                    |
| Migration guides    | `migration-guides/` | Rules for upgrading a repo from one foundation version to the next                                                         |

## Data Flow

1. Operator opens an AI session inside a **target repository**
2. AI reads `bootstrap/create-new-project.md` (or upgrade/audit equivalent) from this foundation repo by absolute path
3. AI loads `spec/` files in the order defined by the bootstrap workflow
4. AI stamps the `.ai/` directory structure into the target repo using `templates/` as source
5. AI populates manifests and context files with project-specific content
6. AI runs the audit workflow to validate the result

The foundation repo itself is never modified during bootstrap of another repo.

## External Services

None. The foundation is a local file-based system with no network dependencies at runtime.

## Deployment Model

Not deployed. Consumed as a reference by cloning or reading files via absolute path in an AI session.

## Constraints

- All structural decisions for target repos must derive from `spec/` — no invention permitted
- `spec/` files must not be modified during bootstrap of target repos
- Templates are copied verbatim — no modification during copy
- The foundation version in `.ai/manifests/foundation.yaml` must not be changed after initial setup; upgrades follow `migration-guides/`
