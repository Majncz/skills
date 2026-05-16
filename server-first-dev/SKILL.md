---
name: server-first-dev
description: One-time bootstrap for a production app on a fresh Hetzner server. Use when the user first connects an AI agent to a new server and gives the initial application prompt—cafe site, e-shop, internal admin, presentation web, or similar. Sets up Docker Compose, Caddy, PostgreSQL, MinIO, prod/dev environments, server workbench, local backups, secrets, and future-agent docs (AGENTS.md). Also use when reviewing an existing server-first setup or continuing bootstrap before readiness is complete. Do not use for routine feature work after bootstrap—future agents should read AGENTS.md instead.
---

# Server-First Development

Bootstrap a real production application on a single server. This skill runs once at the start; afterward the project should be self-explanatory to any AI agent via `AGENTS.md` and the server workbench.

## When To Use

- First SSH session on a fresh server with the user's first serious app prompt.
- User explicitly wants the "server-first" / article workflow setup.
- Reviewing or finishing an incomplete bootstrap (readiness checklist not done).

## When Not To Use

- Routine bug fixes or features on an already-bootstrapped project (read `AGENTS.md` first).
- Local-only development without server deployment unless user only wants stack scaffolding.

## Core Outcomes

By the end of bootstrap, deliver:

1. Monorepo app (Express + Vite React + Prisma + PostgreSQL).
2. Production and development environments (separate hostnames, DBs, secrets).
3. Docker Compose + Caddy + MinIO.
4. Server workbench (read-mostly ops UI).
5. Level 1 local backups visible in workbench (no external backup service required initially).
6. `AGENTS.md` + `docs/agent/*` for future agents.
7. Workbench readiness checklist reflecting real state.

## Workflow

Read references only when needed. Prefer outcomes over rigid commands—the server and app shape can vary.

### 1. Understand

- Confirm domains: production (`example.com` / `www`) and development (`dev.example.com` or user choice).
- Clarify app type: presentation site, e-shop, internal admin, or mix.
- Note payment provider only if user asks (out of scope by default).

### 2. Inspect Server

- OS, disk, RAM, Docker availability, Node/npm availability, open ports.
- Assume the server may be completely clean. Install missing prerequisites yourself (for example `curl`, `git`, `ca-certificates`, Node.js/npm, Docker/Compose, and any build tools needed by the generated app).
- Record findings in `docs/agent/DEVLOG.md` as you go.

### 3. Scaffold Project

- Monorepo with TypeScript strict mode, npm, latest stable LTS Node.
- Stack defaults: see [references/technology-decisions.md](references/technology-decisions.md).
- REST API, Zod validation, meaningful admin errors, server-local logs (no Sentry by default).

### 4. Infrastructure

- Docker Compose for services (exact service names: your choice at runtime).
- Caddy: HTTPS, serve built frontend, proxy API.
- PostgreSQL (prod + dev), MinIO for uploads.
- See [references/deployment.md](references/deployment.md) and [references/development-environment.md](references/development-environment.md).

### 5. Application

- Build user's requested features.
- **Public/customer pages:** [references/frontend-design.md](references/frontend-design.md).
- **Admin + workbench:** [references/admin-design.md](references/admin-design.md).
- Socket.IO where live data matters (admin dashboards, order status)—not on static marketing pages. See technology-decisions.

### 6. Server Workbench

- Same stack as main app; mostly read-only.
- Stats, service health, secrets, to-dos, readiness, backup status, dev log visibility.
- See [references/server-workbench.md](references/server-workbench.md) and [references/workbench-readiness-checklist.md](references/workbench-readiness-checklist.md).

### 7. Secrets

- Workbench is central secret UI; dev/prod separation; last-four display for comparison.
- See [references/secrets.md](references/secrets.md).

### 8. GitHub (Readiness Step)

- Before off-server backups, offer GitHub connection.
- Guide account/repo/SSH if needed; allow explicit deferral.
- Record in readiness checklist.

### 9. Backups And Rollback

- **Level 1 (required for first ship):** local scheduled backups, visible in workbench. Hourly for 24h, then one per day.
- **Level 2 (recommended later):** Hetzner Storage Box off-server copies.
- User can ask AI to roll back; document how in `docs/agent/ROLLBACK.md`.
- See [references/backups-and-rollback.md](references/backups-and-rollback.md).

### 10. Future-Agent Docs

- Create from templates in `assets/` if missing.
- See [references/future-agent-docs.md](references/future-agent-docs.md).
- Update `DEVLOG.md` and readiness after each major step.

### 11. Handoff

- Tell user what is live (prod/dev URLs), what readiness items remain, and that future work can continue without this skill via `AGENTS.md`.

## Reference Index

| Topic | File |
|-------|------|
| Stack defaults | [references/technology-decisions.md](references/technology-decisions.md) |
| Deploy / Caddy / Compose | [references/deployment.md](references/deployment.md) |
| Prod vs dev | [references/development-environment.md](references/development-environment.md) |
| Workbench | [references/server-workbench.md](references/server-workbench.md) |
| Readiness checklist | [references/workbench-readiness-checklist.md](references/workbench-readiness-checklist.md) |
| Secrets | [references/secrets.md](references/secrets.md) |
| Backups / rollback | [references/backups-and-rollback.md](references/backups-and-rollback.md) |
| Public UI design | [references/frontend-design.md](references/frontend-design.md) |
| Admin / workbench UI | [references/admin-design.md](references/admin-design.md) |
| AGENTS.md convention | [references/future-agent-docs.md](references/future-agent-docs.md) |

## Non-Negotiables

- HTTPS only; HTTP-only secure cookies for JWT auth (90-day); bcrypt for passwords.
- Never commit secrets; no server secrets in frontend bundles.
- First backup setup must not require external services.
- Workbench: no destructive/restart controls by default—AI performs mutations with logging.
- Meaningful errors for users; enough server logs for AI debugging.

## Assets

Templates for generated projects live in `assets/`—copy and fill when bootstrapping.
