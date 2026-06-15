# Bootstrap: Audit Project

Deterministic, read-only workflow for validating a repository against the Engineering AI Foundation spec.

---

## Input

```
repo_path: string
```

---

## Process

### Step 1 — Load spec

Load in this exact order:

1. `spec/repo-structure.yaml`
2. `spec/file-schemas.yaml`
3. `spec/manifest-schema.yaml`

---

### Step 2 — Check required folders

For each folder in `spec/repo-structure.yaml` under `folders.required`:

- PASS if folder exists
- FAIL if folder is missing

---

### Step 3 — Check required files

For each file in `spec/repo-structure.yaml` under `required_files`:

- PASS if file exists at repo root
- FAIL if file is missing

---

### Step 4 — Validate manifest schemas

For each manifest defined in `spec/manifest-schema.yaml`:

- Check file exists at declared path
- Check all `required_fields` are present
- Check field values match declared types and enums
- PASS | FAIL per manifest

---

### Step 5 — Validate context file schemas

For each file found under `.ai/context/` and `.ai/agents/`:

- Match against schema in `spec/file-schemas.yaml`
- Check all required sections are present
- Check no required section has been renamed
- PASS | FAIL per file

---

### Step 6 — Check for unknown files in `.ai/`

List all files under `.ai/` that are not defined in `spec/file-schemas.yaml` and not in `spec/repo-structure.yaml`.
Flag each as WARN (unknown files do not block pass, per enforcement rules).

---

### Step 7 — Check for structural drift

Detect:

- Folders that exist but are not in spec (WARN)
- Files in `.ai/` with wrong extension (WARN)
- Manifest files referencing agents not in `spec/agent-registry.yaml` (WARN)

---

## Output

Produce a structured audit report:

```yaml
audit:
  repo: { repo_path }
  timestamp: { iso8601 }
  foundation_version: { from .ai/manifests/foundation.yaml or "missing" }
  result: passed | failed

  checks:
    required_folders:
      - path: string
        status: pass | fail

    required_files:
      - path: string
        status: pass | fail

    manifest_schemas:
      - manifest: string
        status: pass | fail
        violations: []

    context_schemas:
      - file: string
        status: pass | fail
        violations: []

    warnings:
      - type: unknown_file | structural_drift | unknown_agent
        path: string
        detail: string

  summary:
    errors: N
    warnings: N
```

---

## Rules

- Do not modify any file in the repository
- Do not create any file in the repository
- Only report findings
- result is `passed` only when errors = 0
- Warnings do not affect pass/fail
