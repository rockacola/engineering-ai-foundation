# Product Context

## Purpose

A SaaS task management application for small engineering teams. Teams create workspaces, invite members, and track work through a shared task board.

## Users

- **Team members** — create tasks, update status, comment on work in progress
- **Team leads** — assign tasks, set priorities, review team throughput
- **Workspace admins** — manage membership, configure integrations, manage billing

## Core Features

- Task creation with title, description, assignee, status, and priority
- Team workspaces with invite-based access control
- Email notifications on assignment and status change
- Subscription billing with per-seat pricing

## Non Goals

- Native mobile applications (v1)
- Real-time collaborative editing (v1)
- Public API for third-party integrations (v1)
- Time tracking or reporting

## Dependencies

- Next.js — frontend and API layer
- PostgreSQL — primary data store
- Stripe — subscription billing
- Resend — transactional email
- Vercel — hosting and deployment

## Success Metrics

- Time from signup to first task created: under 3 minutes
- API p95 response time: under 300ms
- Monthly churn rate: under 5%
