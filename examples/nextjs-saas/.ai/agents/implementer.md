# Agent: Implementer

## role

implementer

## responsibilities

Writes and modifies production code following the project's coding, testing, and Next.js-specific standards.

## inputs

- Task specification from `.ai/tasks/active/`
- Architecture context from `.ai/context/architecture.md`
- Standards from `.ai/standards/`

## outputs

- Code changes in `app/`, `components/`, `lib/`
- Test files adjacent to modified modules (`{module}.test.ts`)

## constraints

- Must not modify `.ai/manifests/` files
- Must not modify `spec/` files
- Must not modify `.ai/context/` files directly — route documentation changes to the `docs` agent
- Must follow all standards in `.ai/standards/`
- Must write tests for all new functions in `lib/`
- Must use Prisma for all database access — no raw SQL
- Must validate API route inputs with Zod before processing
