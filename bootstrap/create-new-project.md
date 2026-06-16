# Bootstrap: Create New Project

Deterministic workflow for scaffolding a new repository from the Engineering AI Foundation spec.

---

## Input

```
project_name: string
project_description: string
repo_type: new
```

---

## Process

### Step 1 — Load spec

Load in this exact order:

1. `spec/repo-structure.yaml`
2. `spec/file-schemas.yaml`
3. `spec/agent-registry.yaml`
4. `spec/manifest-schema.yaml`

Do not proceed if any spec file is missing or fails to parse.

---

### Step 2 — Create required folder structure

Create every folder listed in `spec/repo-structure.yaml` under `folders.required`.

Do not create any folder not listed in the spec.

---

### Step 3 — Copy templates

Copy the entire `templates/` directory into the target repository root.

File mapping:

- `templates/AGENTS.md` → `AGENTS.md`
- `templates/.aiignore` → `.aiignore`
- `templates/.ai/**` → `.ai/**`

Do not rename any file. Do not modify any file during copy.

---

### Step 4 — Populate foundation manifest

Read `foundation_version` from `package.json` at the foundation repo root.

Write `.ai/manifests/foundation.yaml`:

```yaml
foundation_version: '{foundation_version}'
applied_at: { iso8601_timestamp }
repo_type: new
```

---

### Step 5 — Initialise context manifest

Write `.ai/manifests/context.yaml` with empty contexts list.
Write `.ai/manifests/ownership.yaml` with empty domains list.

---

### Step 6 — Generate README.md

Create `README.md` at repo root.

Required sections:

- Project name
- One-sentence description
- How to use this repo

Do not add sections not listed above.

---

### Step 7 — Validate structure

Run the audit workflow (`bootstrap/audit-project.md`) against the newly created repo.

Expected result: zero errors.

If any errors are present, halt and report. Do not hand off to the user until audit passes.

---

## Output

```
Repo scaffold complete.
foundation_version: '{foundation_version}'
folders_created: [list]
files_created: [list]
audit_result: passed
```

---

## Prohibited Actions

- Do not create any file not defined in `spec/file-schemas.yaml`
- Do not populate context files with invented content
- Do not activate agents not in `spec/agent-registry.yaml`
- Do not modify `spec/` files
