---
last_updated: 2026-06-16
---

# Tribal Knowledge

## Summary

Conventions and context that are not obvious from reading the spec or files alone.

## Key Facts

- Bootstrap workflows must be run from inside the **target repository**, not from this foundation repo. Reference foundation files by absolute path in your AI session.
- The foundation repo is the reference for "how things should be done". Target repos do not need to duplicate guidance that lives here — they only need the structure and what's specific to them.
- `spec/` files must not be modified during bootstrap of another repo. They are read-only inputs to the bootstrap process.

## References

- `bootstrap/create-new-project.md`
- `README.md`
