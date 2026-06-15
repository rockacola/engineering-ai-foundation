# Example: Next.js SaaS

Reference implementation of Engineering AI Foundation compliance for a Next.js SaaS application.

The scenario is a task management SaaS with team workspaces, Stripe billing, and Resend email.

## What this example demonstrates

- Full `.ai/` folder structure for a SaaS product
- `product.md` and `architecture.md` context files following spec schemas
- Agent manifest with all seven agents active
- Per-domain ownership across frontend, backend, and data
- Language-specific standard for Next.js App Router patterns
- A per-agent configuration file for the `implementer` role
- An example task and an ADR for the auth strategy decision

## Structure

```
nextjs-saas/
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
│   ├── agents/
│   │   └── implementer.md
│   ├── standards/
│   │   └── nextjs.md
│   └── tasks/
│       └── task-001.yaml
└── docs/
    └── adr/
        └── 0001-auth-strategy.md
```

## Notes

This is a reference scaffold, not a runnable application. Use it to understand the expected level of detail in context files, manifests, and ADRs — then adapt to your own project.
