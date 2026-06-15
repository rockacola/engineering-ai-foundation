---
last_updated: 2026-06-16
---

# Lessons Learned

## Summary

Accumulated lessons from working with and evolving the Engineering AI Foundation.

## Key Facts

- The foundation repo itself should be bootstrapped with its own spec (dogfooding). Without it, AI systems operating in this repo have no contract to follow.
- Not all agents from `spec/agent-registry.yaml` are appropriate for every repo. The active agent list should reflect what the project actually needs.
- Rules in `AGENTS.md` are the primary contract for AI behaviour in a repo. Claude's own memory is a fallback, not a substitute.

## References

- `docs/adr/0001-apply-foundation-to-itself.md`
- `.ai/journal/2026/2026-06-16.md`
