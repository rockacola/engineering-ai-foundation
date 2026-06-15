# Bootstrap: Upgrade Existing Project

Deterministic workflow for migrating an existing repository into compliance with the Engineering AI Foundation spec.

---

## Input

```
repo_path: string
current_foundation_version: string | null
target_foundation_version: 1.0.0
```

---

## Process

### Step 1 — Load spec

Load `spec/repo-structure.yaml`, `spec/file-schemas.yaml`, `spec/manifest-schema.yaml`, `spec/migration-rules.yaml`.

All migration behaviour in subsequent steps is governed by the rules in `spec/migration-rules.yaml`. The blocking rules there take precedence over any local judgement call.

---

### Step 2 — Parse current repo structure

Recursively list all files and folders in the repo.
Exclude paths matched by `.aiignore` if present.

---

### Step 3 — Compare against spec

Produce a structured diff:

```yaml
missing_folders: []
missing_files: []
unknown_ai_files: []
schema_violations: []
```

---

### Step 4 — Generate mapping plan

For each existing file, determine one of:

- `move` — file belongs in a different location under the new structure
- `keep` — file is already in the correct location
- `archive` — file has no place in the new structure
- `pending` — AI cannot determine; requires human decision

Output the plan as:

```yaml
mapping_plan:
  - source: path/to/existing-file
    action: move | keep | archive | pending
    target: path/to/new-location # if action is move
    reason: string
```

---

### Step 5 — Human approval gate

**HALT. Do not proceed.**

Present the mapping plan to the human operator.
Wait for explicit written approval before continuing.

Required approval statement: `"Approved"` or equivalent explicit confirmation.

Do not infer approval from silence or partial responses.

---

### Step 6 — Execute migration

Apply the approved mapping plan:

1. For `move`: use `git mv {source} {target}` to preserve git history.
2. For `keep`: no action.
3. For `archive`: move to `.ai/archive/{original_path}_{timestamp}`.
4. For `pending`: leave untouched; record in migration report as unresolved.

---

### Step 7 — Create missing structure

Create any folders and files listed as missing in Step 3.
Populate templates for missing required files.

---

### Step 7a — Sync foundation standards

Copy `standards/coding.md`, `standards/testing.md`, and `standards/security.md` from the foundation repository into `.ai/standards/`.

- If a file does not exist in `.ai/standards/`: copy it.
- If a file already exists in `.ai/standards/`: **do not overwrite** — the project may have customised it. Record the existing file as `kept` in the migration report.

---

### Step 8 — Update foundation manifest

Write `.ai/manifests/foundation.yaml`:

```yaml
foundation_version: 1.0.0
applied_at: { iso8601_timestamp }
repo_type: migrated
```

---

### Step 9 — Generate migration report

Write `migration-report.md` at repo root:

Required sections:

- Summary
- Files Moved
- Files Archived
- Files Created
- Validation Results
- Pending Human Decisions

---

### Step 10 — Validate

Run `bootstrap/audit-project.md`.
Append audit results to migration report under `Validation Results`.

---

## Output

```
Migration complete.
files_moved: N
files_archived: N
files_created: N
pending_decisions: N
audit_result: passed | failed
report: migration-report.md
```

---

## Prohibited Actions

- Do not delete any file without archiving first
- Do not proceed past Step 5 without explicit human approval
- Do not invent content for migrated files
- Do not modify `spec/` files
