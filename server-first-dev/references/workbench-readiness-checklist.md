# Workbench Readiness Checklist

One workbench page combining **user to-dos** and **AI-managed production readiness**.

## User To-Dos

Users can add tasks for later (for themselves or the AI):

- Fields: title, notes, status, priority, createdAt, updatedAt
- Not the same as readiness items—free-form backlog

## Readiness Checklist

AI updates items as bootstrap progresses. Display makes the **next step** obvious (unchecked items first, optional grouping).

### Default Items

Seed or mirror these; edit per project:

1. App built
2. Production app reachable
3. Development app reachable
4. Domain connected
5. HTTPS working
6. Production database running
7. Development database running
8. MinIO / uploads working (if app uses uploads)
9. GitHub repository connected **or explicitly deferred**
10. Local backups running
11. Local restore instructions written
12. Hetzner Storage Box backups configured **or explicitly deferred**
13. Backup restore tested or documented
14. Secrets configured (production + development)
15. Admin authentication configured
16. Basic security checks completed
17. Future-agent docs written (`AGENTS.md` + `docs/agent/*`)

### AI Responsibilities

- Check items only when verified (HTTP check, backup file exists, etc.).
- Add custom items when the app needs them (e.g. payment provider, email DNS).
- Record deferrals with reason in notes (e.g. "GitHub deferred—user will add next week").

### Sync

Keep `docs/agent/READINESS.md` aligned with workbench state for agents that do not open the UI.
