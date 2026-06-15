# Example: Internal Tool

Reference implementation of Engineering AI Foundation compliance for a small internal CLI tool with a single owner and a minimal agent setup.

The scenario is a database maintenance CLI used exclusively by a platform team.

## What this example demonstrates

- Minimal compliant `.ai/` structure appropriate for a small, single-owner tool
- A simplified agent manifest — only `implementer` and `reviewer` active, the rest explicitly disabled
- Single-domain ownership with an email address as the owner
- Context files scoped tightly to operational knowledge
- An ADR documenting a deliberate design choice (CLI over web UI)

## Structure

```
internal-tool/
├── AGENTS.md
├── .ai/
│   ├── manifests/
│   │   ├── foundation.yaml
│   │   ├── context.yaml
│   │   ├── ownership.yaml
│   │   └── agents.yaml
│   ├── context/
│   │   ├── product.md
│   │   └── architecture.md
│   └── tasks/
│       └── task-001.yaml
└── docs/
    └── adr/
        └── 0001-cli-over-web-ui.md
```

## Notes

This is a reference scaffold, not a runnable application. The key thing to notice here is what is _absent_: no per-agent config files, no language-specific standards, only two active agents. Compliance does not mean using everything — it means using the right subset.
