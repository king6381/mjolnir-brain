# Mjolnir Brain — OpenClaw Skill

AI Agent 自进化记忆系统。分层记忆架构 + 自我学习 + 策略注册表 + 自动提炼。

## Installation

```bash
clawdhub install mjolnir-brain
```

## What It Does

Gives your OpenClaw agent persistent memory and self-learning capabilities:

- **Layered memory**: session logs → daily files → curated long-term memory
- **Self-improvement**: errors auto-recorded, never repeated
- **Strategy registry**: problem→solution mappings with success rate tracking
- **Auto consolidation**: AI summarizes daily logs into distilled knowledge
- **Backup**: dual-target automated backups (WebDAV + SSH)

## Setup

After installation, start a new OpenClaw session. The agent will:
1. Read `BOOTSTRAP.md` and guide you through identity setup
2. Configure memory files based on your preferences
3. Start learning immediately

## Files

| File | Purpose |
|------|---------|
| `AGENTS.md` | Behavioral rules + self-improvement protocol |
| `SOUL.md` | Personality definition |
| `MEMORY.md` | Long-term curated memory (≤20KB) |
| `HEARTBEAT.md` | Periodic check configuration |
| `strategies.json` | Problem→solution registry |
| `scripts/*.sh` | Automation (consolidation, search, backup) |
| `playbooks/` | Parameterized operation guides |

## Key Commands

```bash
# Search memory
scripts/memory_search.sh "keyword"        # exact
scripts/memory_search.sh -f "keyword"     # fuzzy

# Strategy lookup
scripts/strategy_lookup.sh "error message"

# Update strategy success rate
scripts/strategy_update.sh pip_install_fail 0 success

# Run memory maintenance
scripts/memory_consolidate.sh
```

## Requirements

- OpenClaw (any version)
- bash, python3, git
- curl (optional, for WebDAV backup)

## Links

- [GitHub](https://github.com/YOUR_USER/mjolnir-brain)
- [Architecture Docs](docs/architecture.md)
- [Self-Learning Explained](docs/self-learning.md)
