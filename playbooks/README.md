# Playbooks

Playbooks are parameterized runbooks for frequently repeated operations.

## Format

Each playbook follows this structure:

```markdown
# Title
## Parameters
- param1: description
## Pre-checks
- [ ] check item
## Steps
1. command
2. ...
## Rollback
- what to do if it fails
## History
- created: date
```

## Frequency Tracking

`frequency.json` tracks how often operations are performed. When an operation type exceeds 3 occurrences, consider creating a playbook for it.

## Adding a Playbook

1. Create `your-playbook.md` in this directory
2. Follow the format above
3. Update `frequency.json` if tracking the operation type

## Example Playbooks

- `deploy-to-server.md` — Deploy project to production
- `debug-service-crash.md` — Service crash troubleshooting flowchart
- `backup-data.md` — Data backup procedure
