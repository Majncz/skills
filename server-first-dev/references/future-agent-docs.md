# Future-Agent Documentation

After bootstrap, **future agents should not need this skill**. They read project docs first.

## Entrypoint: `AGENTS.md`

Short file at repo root. Required sections:

1. **Read first** — list `docs/agent/*` files in order.
2. **Project summary** — what the app does, prod/dev URLs.
3. **Rules** — never commit secrets; read DEVLOG before deploy; update DEVLOG after meaningful changes; check READINESS for incomplete bootstrap.
4. **Common commands** — pointers to OPERATIONS.md (not a full duplicate).

Use template: [assets/AGENTS.template.md](../assets/AGENTS.template.md).

## `docs/agent/` Files

| File | Purpose |
|------|---------|
| ARCHITECTURE.md | Services, repos, folders, data flow |
| OPERATIONS.md | Build, deploy, logs, debug, compose commands |
| ENVIRONMENTS.md | Hostnames, DB names, secret *names*, ports |
| BACKUPS.md | Local + Storage Box policy, paths, risks |
| ROLLBACK.md | How to revert code, DB, files |
| DEVLOG.md | Chronological decisions (newest first) |
| READINESS.md | Checklist mirror of workbench |

Templates in [assets/docs-agent/](../assets/docs-agent/).

## When To Update

- **DEVLOG:** every deploy, infra change, backup policy change, incident.
- **READINESS:** when checklist items change.
- **ARCHITECTURE / ENVIRONMENTS:** when services or hostnames change.
- **ROLLBACK / BACKUPS:** after first real restore test or policy change.

## Workbench Integration

Expose summaries: readiness status, last DEVLOG entries, backup age, service health—so humans see state without opening markdown.

## Writing Style

- Audience: AI agents first, humans second.
- Concise, explicit, honest about unknowns.
- Prefer actual hostnames, paths, and service names from *this* deployment—not placeholders left unfilled.

## Bootstrap Obligation

Before calling bootstrap complete, all files must exist and contain real project-specific values—not lorem ipsum.
