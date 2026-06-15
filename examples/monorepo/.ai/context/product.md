# Product Context

## Purpose

An internal developer platform consisting of a REST API and a web dashboard, maintained as a monorepo. The platform provides engineering teams with self-service access to infrastructure provisioning and deployment status.

## Users

- **Engineers** — trigger deployments, view service health, manage environment variables via the API or dashboard
- **Team leads** — review deployment history and access logs for their team's services
- **Platform team** — maintain the API and dashboard, manage permissions, run infrastructure changes

## Core Features

- REST API for deployment triggers and status queries
- Web dashboard for deployment history and service health overview
- Role-based access control per service
- Shared type definitions consumed by both packages

## Non Goals

- External customer-facing features
- Mobile applications
- Real-time log streaming (v1)

## Dependencies

- Node.js + Fastify — API package
- React + Vite — web package
- PostgreSQL — shared data store
- pnpm workspaces — monorepo package management

## Success Metrics

- API availability: 99.9% uptime
- Dashboard initial load time: under 1 second on internal network
- Deployment trigger to status update latency: under 5 seconds
