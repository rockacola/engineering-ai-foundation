# Architecture Context

## System Overview

Single-package Node.js CLI. Commands are invoked manually by platform engineers or via scheduled CI jobs. No web server, no persistent process.

## Components

- `src/commands/` — one file per CLI command (migrate, snapshot, rotate-credentials)
- `src/db/` — PostgreSQL client setup and query helpers
- `src/aws/` — S3 and Secrets Manager clients
- `src/config.ts` — environment variable loading and validation
- `scripts/` — shell wrappers for CI invocation

## Data Flow

1. Engineer runs `node src/index.js <command> --env <target>`
2. `config.ts` loads and validates environment variables for the target
3. Command module runs the operation (migration, snapshot, or rotation)
4. Result is logged to stdout; errors exit with a non-zero code

## External Services

- **PostgreSQL** — target database for all operations
- **AWS S3** — snapshot storage
- **AWS Secrets Manager** — credential storage and rotation target

## Deployment Model

- Not deployed as a service — run on demand from an engineer's machine or a CI runner
- Credentials sourced from environment variables or AWS instance role (in CI)
- No `.env` files in the repository — engineers use their own local `.env.local`

## Constraints

- Must exit non-zero on any failure — callers rely on exit codes
- Must not hardcode credentials or environment names
- All destructive operations (credential rotation) must prompt for confirmation unless `--yes` flag is passed
