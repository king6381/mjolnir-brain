---
name: mjolnir-brain
description: "AI Agent self-evolving memory system. 100% local core (pure Markdown+JSON). Network features are optional opt-in."
---

# Mjolnir Brain - AI Agent Self-Evolving Memory System

**Version**: v3.0.3
**Author**: king6381
**License**: MIT

---

## Security Model

| Feature | Network | Credentials | Default |
|---------|---------|-------------|---------|
| Core Memory | No | No | Enabled |
| Backup | Yes | Yes | Disabled |
| Node Comms | Yes | Yes | Disabled |

**Core Promise**: 100% local by default, network features require explicit opt-in

---

## Core Features (Local)

- Three-layer memory: daily logs + MEMORY.md + strategies.json
- Write-through protocol
- Strategy registry
- Session restoration

**No binaries or network required**

---

## Optional Features (Opt-In)

### 1. Network Backup

WEBDAV_URL, WEBDAV_USER, WEBDAV_PASS
SSH_HOST, SSH_PATH

### 2. Node Communication

MJOLNIR_USER

### 3. Automation Scripts

Requires: bash, git, grep

---

## Quick Install

Core (Recommended):
  cp -r templates/* $WORKSPACE/
  cp strategies.json $WORKSPACE/

Full (Optional):
  cp -r scripts/ $WORKSPACE/scripts/
  chmod +x $WORKSPACE/scripts/*.sh

---

## Security Recommendations

1. Review scripts before enabling
2. Use minimum required features
3. Test in isolated workspace
4. Use environment variables for credentials
5. Support DRY_RUN=1 for testing

---

## Docs

- docs/architecture.md
- docs/self-learning.md
- docs/best-practices.md
- docs/security.md
