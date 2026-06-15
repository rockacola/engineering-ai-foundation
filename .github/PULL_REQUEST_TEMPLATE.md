## Summary

<!-- What does this change and why? -->

## Spec Impact Checklist

- [ ] Does this change any schema in `spec/`? If yes, does it require a major, minor, or patch version bump? (See `spec/versioning.yaml`)
- [ ] If this is a breaking change (major bump), is a migration guide added to `migration-guides/`?
- [ ] If this adds a required field or folder, does the `templates/` directory reflect the change?
- [ ] If this modifies `spec/file-schemas.yaml`, are example files in `examples/` still valid?
- [ ] If this adds a new bootstrap workflow, is it referenced from `README.md`?
- [ ] Is `CHANGELOG.md` updated?

## Testing

- [ ] `npx prettier --check "**/*.{md,yaml}"` passes
- [ ] All spec YAML files parse without error
- [ ] Ran `bootstrap/audit-project.md` mentally (or actually) against at least one example
