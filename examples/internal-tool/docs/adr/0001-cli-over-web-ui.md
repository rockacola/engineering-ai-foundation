# 0001 — CLI Over Web UI

## Status

accepted

## Context

The tool automates database maintenance tasks for the platform team. Two delivery options were considered:

1. **CLI** — low overhead, runs where engineers already work, no hosting required
2. **Web UI** — more accessible, requires hosting, auth, and ongoing maintenance

The tool is used exclusively by platform engineers (fewer than five people) who are comfortable with the terminal.

## Decision

Build as a CLI tool. The audience is small and technical; the operational cost of hosting a web service is not justified.

## Consequences

- No browser required; runs on engineer machines and CI runners
- No access control layer needed — access is controlled by who has the credentials
- Adding a web UI later would require a significant rewrite
- Discoverability depends on documentation rather than a UI
