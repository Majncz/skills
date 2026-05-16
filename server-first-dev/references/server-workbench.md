# Server Workbench

A **read-mostly** operations portal generated during bootstrap. Same stack as the main app (Express, Vite React, Prisma, etc.). Styled per [admin-design.md](admin-design.md).

## Purpose

Help the user and future AI agents **see** server truth—not replace the AI as operator. Mutations (deploy, restore, restart) happen through the AI with logging, not fragile workbench buttons.

## Pages

### Overview / Stats

- Disk free / total
- CPU and RAM (current + simple history charts if practical)

### Service Health

- Production hostname reachable
- Development hostname reachable
- App processes up
- PostgreSQL (prod + dev)
- MinIO
- Caddy / TLS status

### Secrets

See [secrets.md](secrets.md).

### To-Dos And Readiness

See [workbench-readiness-checklist.md](workbench-readiness-checklist.md).

### Backups

- Last backup time, type (hourly/daily), size if easy
- List of local restore points (filename, timestamp)
- Warning if production backup older than policy threshold
- Note if Level 2 Storage Box not configured (with risk reminder)

### Dev Log / Recent Changes

Surface recent entries from `docs/agent/DEVLOG.md` or a DB mirror—what changed, when, why.

### Logs Viewer

Tail or paginate relevant Compose logs (read-only). Enough for user sanity checks; AI uses SSH/compose directly for deep debugging.

## Explicitly Omit By Default

- Service restart buttons
- One-click restore / destructive actions
- Generic server control panels (Cockpit, Webmin, Coolify, etc.)

## Auth

Protect entire workbench like admin: JWT cookie, same auth approach as app admin unless split account is requested.

## Data Model

Agent chooses schema for checklist items, to-dos, dev-log mirrors, backup metadata. Keep it simple and documented in `ARCHITECTURE.md`.
