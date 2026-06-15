# Product Context

## Purpose

A CLI tool used by the platform team to automate routine database maintenance tasks: running migrations, generating snapshots, and rotating credentials across environments.

## Users

- **Platform engineers** — the only users; tool is not exposed to other teams

## Core Features

- Run pending database migrations against a target environment
- Generate a point-in-time schema snapshot and upload to S3
- Rotate database credentials and update secrets manager

## Non Goals

- Web UI or dashboard
- Use by non-platform engineers
- Support for non-PostgreSQL databases

## Dependencies

- Node.js — runtime
- `pg` — PostgreSQL client
- AWS SDK — S3 uploads and Secrets Manager access
- dotenv — environment variable loading for local use

## Success Metrics

- Migration run time: under 60 seconds for typical workloads
- Zero failed credential rotations in production (target: 100% success rate)
