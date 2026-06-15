# Bootstrap: Generate Context

Deterministic workflow for extracting and populating `.ai/context/` from an existing repository.

---

## Input

```
repo_path: string
domain: string  # e.g. "product", "architecture", "data-model"
```

---

## Process

### Step 1 — Load schemas

Load `spec/file-schemas.yaml`.
Identify the schema for the requested domain (e.g. `product_md`, `architecture_md`).

If no schema exists for the requested domain, halt:

> "Not permitted. Domain schema not defined in spec/file-schemas.yaml. Requires spec update."

---

### Step 2 — Check for existing file

Check if the target context file already exists (per schema `path` field).

- If exists: load current content. Treat as base to update, not replace.
- If missing: proceed to generate from scratch.

---

### Step 3 — Extract domain knowledge from repository

Read the following in order, skipping paths matched by `.aiignore`:

1. `README.md`
2. Existing `.ai/context/` files
3. Relevant source code and configuration files for the declared domain

Extraction rules:

- Extract only facts observable in the repository
- Do not infer intent not supported by evidence
- Do not copy raw code blocks unless the schema requires them
- Do not include personally identifiable information

---

### Step 4 — Populate context file

Write the context file using exactly the sections defined in the schema.

- Do not rename sections
- Do not add sections not in the schema
- Do not omit required sections (leave as `TBD` if information is unavailable, do not skip)

---

### Step 5 — Update context manifest

Add or update the entry for this file in `.ai/manifests/context.yaml`:

```yaml
contexts:
  - path: .ai/context/{domain}.md
    description: { one-line description of what this file contains }
    tags: [{ domain }]
```

If the file is already listed, update `description` if it has changed. Do not duplicate entries.

---

### Step 6 — Validate

Run schema validation for the generated file (as per `bootstrap/audit-project.md` Step 5).

If validation fails, correct the file and re-validate before completing.

---

## Output

```
Context file generated.
path: .ai/context/{domain}.md
sections_populated: N
manifest_updated: true
validation: passed
```

---

## Prohibited Actions

- Do not invent facts not present in the repository
- Do not generate context for domains without a schema
- Do not modify `.ai/memory/` or `.ai/journal/` during this workflow
- Do not modify `spec/` files
