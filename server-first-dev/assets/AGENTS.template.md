# AGENTS.md

**Read this file before making any change to this project.**

## Project

- **Name:** {{PROJECT_NAME}}
- **Production:** https://{{PROD_HOST}}
- **Development:** https://{{DEV_HOST}}
- **Summary:** {{ONE_LINE_DESCRIPTION}}

## Read Next (in order)

1. [docs/agent/ARCHITECTURE.md](docs/agent/ARCHITECTURE.md)
2. [docs/agent/ENVIRONMENTS.md](docs/agent/ENVIRONMENTS.md)
3. [docs/agent/OPERATIONS.md](docs/agent/OPERATIONS.md)
4. [docs/agent/BACKUPS.md](docs/agent/BACKUPS.md)
5. [docs/agent/ROLLBACK.md](docs/agent/ROLLBACK.md)
6. [docs/agent/READINESS.md](docs/agent/READINESS.md)
7. [docs/agent/DEVLOG.md](docs/agent/DEVLOG.md)

## Rules

- Assume the user is non-technical by default. Do as much as is safe yourself, explain only necessary choices, and switch to technical detail only when the user asks or clearly has the context.
- Never commit secrets. Use the server workbench secrets UI or env files documented in ENVIRONMENTS.md.
- Read DEVLOG.md before deploys; append after meaningful changes.
- Prefer reversible changes: backup DB before migrations; commit before risky edits.
- Meaningful errors for users; log enough detail on the server for debugging.
- Do not add Sentry or heavy external ops tools unless the user asks.

## Quick Operations

See [docs/agent/OPERATIONS.md](docs/agent/OPERATIONS.md) for build, deploy, logs, and Docker Compose commands for **this** server.

## Bootstrap

This project was set up with the `server-first-dev` skill. Routine work does not require that skill—this file is the source of truth.
