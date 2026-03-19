---
name: mjolnir-brain
description: "AI Agent 自进化记忆系统 (Mjolnir Brain)。提供分层记忆架构、Write-Through 即时写入、策略注册表(问题→解法+成功率追踪)、心跳自检、AI 真摘要提炼、双目标备份。适用于需要持久记忆、自我学习和自动纠错能力的 AI Agent。当用户要求设置记忆系统、自进化能力、策略注册表或 Agent 持久化时使用。"
---

# Mjolnir Brain — AI Agent Self-Evolving Memory System

## Quick Setup

```bash
# Copy templates to workspace
cp -r templates/* $WORKSPACE/
cp -r scripts/ $WORKSPACE/scripts/
cp strategies.json $WORKSPACE/
cp -r playbooks/ $WORKSPACE/
chmod +x $WORKSPACE/scripts/*.sh
mkdir -p $WORKSPACE/memory
```

## Core Components

### 1. Three-Layer Memory
- **Layer 1**: `memory/YYYY-MM-DD.md` — daily session logs (ephemeral)
- **Layer 2**: `MEMORY.md` (≤20KB) + `strategies.json` + `playbooks/` — curated knowledge
- **Layer 3**: `SOUL.md` + `AGENTS.md` + `TOOLS.md` — identity & rules (stable)

### 2. Write-Through Protocol
Write immediately, never defer. Enforced in AGENTS.md:
- Learn something → write to file instantly
- Command fails → check `strategies.json` → update success rate
- Sub-task completes → write findings to `memory/learnings-queue.md`

### 3. Strategy Registry (`strategies.json`)
Problem→solution mapping with success rate tracking:
```bash
# Look up solutions
scripts/strategy_lookup.sh "pip install"
# Update after attempt
scripts/strategy_update.sh pip_install_fail 0 success
```

### 4. Automated Maintenance (cron)
```cron
0 * * * *  scripts/auto_commit.sh           # hourly git commit
0 4 * * *  scripts/memory_consolidate.sh     # clean + archive + mark pending
0 4 * * *  scripts/workspace_backup.sh       # dual-target backup
```

Plus an AI cron job at 04:05 for real summarization of pending daily logs.

### 5. Search
```bash
scripts/memory_search.sh "keyword"           # exact search
scripts/memory_search.sh -f "fuzzy term"     # fuzzy search
scripts/memory_search.sh -a "old topic"      # include archives
```

## Session Startup (MANDATORY)
Every session, before any reply:
1. Read `SOUL.md`
2. Read `USER.md`
3. Read `memory/YYYY-MM-DD.md` (today + yesterday)
4. Read `MEMORY.md` (main session only)

## File Reference
| File | Purpose | Load |
|------|---------|------|
| `SOUL.md` | Personality | Every session |
| `AGENTS.md` | Behavior rules + Write-Through | Every session |
| `USER.md` | User profile | Every session |
| `MEMORY.md` | Long-term curated memory (≤20KB) | Main session |
| `IDENTITY.md` | Name, vibe, emoji | On reference |
| `TOOLS.md` | Environment config | On reference |
| `HEARTBEAT.md` | Periodic checks + idle queue | On heartbeat |
| `BOOTSTRAP.md` | First-run setup (delete after) | First session only |
| `strategies.json` | Problem→solution registry | On error |
| `playbooks/` | Parameterized runbooks | On repeated operation |

## Docs
- `docs/architecture.md` — System design and data flow
- `docs/self-learning.md` — Four learning mechanisms explained
- `docs/best-practices.md` — Tips and common pitfalls
