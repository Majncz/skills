# Secrets

## Rules

- Never commit secrets to Git.
- Never expose server secrets in frontend bundles (only `VITE_*` or public keys belong client-side).
- Generate strong random values for JWT secret, session keys, DB passwords, MinIO credentials.

## Workbench Secrets UI

Central place to manage secrets for both environments.

### Adding A Secret

- Target: development, production, or **both** (default: both).
- Store encrypted or in a protected server-side store—implementation is your choice; document recovery in `docs/agent/BACKUPS.md`.

### Display

- Show only the **last four characters** by default (for comparing whether two entries match).
- Toggle can reveal last-four if hidden; never show full secret in UI after creation.

### Actions

- Create, delete, transfer/copy between development and production.

## Documentation

List required secret names (not values) in `docs/agent/ENVIRONMENTS.md`:

- Database URLs per env
- JWT secret
- MinIO keys
- SMTP credentials
- Any third-party API keys

## Rotation

Support rotating JWT/session secrets; document steps in DEVLOG when rotated.
