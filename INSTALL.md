# 🧠 Mjolnir Brain — Installation Guide

## Prerequisites

- [OpenClaw](https://github.com/openclaw/openclaw) installed and running
- Bash 4+ (Linux/macOS)
- Python 3.8+ (for strategy scripts)
- Git (for auto-commit)

## Method 1: OpenClaw Skill (Recommended)

```bash
clawdhub install mjolnir-brain
```

This installs the skill and makes templates available. You still need to copy templates to your workspace:

```bash
# The skill will guide you through setup on first use
```

## Method 2: Manual Installation

### Step 1: Clone

```bash
git clone https://github.com/YOUR_USER/mjolnir-brain.git
cd mjolnir-brain
```

### Step 2: Copy Templates

```bash
WORKSPACE="${HOME}/.openclaw/workspace"

# Copy template files
cp templates/AGENTS.md "$WORKSPACE/"
cp templates/SOUL.md "$WORKSPACE/"
cp templates/BOOTSTRAP.md "$WORKSPACE/"
cp templates/IDENTITY.md "$WORKSPACE/"
cp templates/USER.md "$WORKSPACE/"
cp templates/MEMORY.md "$WORKSPACE/"
cp templates/HEARTBEAT.md "$WORKSPACE/"

# Copy scripts
cp -r scripts "$WORKSPACE/"
chmod +x "$WORKSPACE/scripts/"*.sh

# Copy strategy registry
cp strategies.json "$WORKSPACE/"

# Create memory directory
mkdir -p "$WORKSPACE/memory"

# Create playbooks directory
mkdir -p "$WORKSPACE/playbooks"
cp playbooks/README.md "$WORKSPACE/playbooks/"
cp playbooks/frequency.json "$WORKSPACE/playbooks/"
```

### Step 3: Initialize Git

```bash
cd "$WORKSPACE"
git init
git add -A
git commit -m "init: Mjolnir Brain memory system"
```

### Step 4: Set Up Cron Jobs (Optional but Recommended)

```bash
crontab -e
```

Add these lines:

```cron
# Memory consolidation — daily at 04:00
0 4 * * * ~/.openclaw/workspace/scripts/memory_consolidate.sh >> ~/.openclaw/workspace/memory/consolidate.log 2>&1

# Auto git commit — every hour
0 * * * * ~/.openclaw/workspace/scripts/auto_commit.sh

# Workspace backup — daily at 04:00 (configure targets in script first)
# 0 4 * * * ~/.openclaw/workspace/scripts/workspace_backup.sh >> ~/.openclaw/workspace/memory/backup.log 2>&1
```

### Step 5: Configure Backup (Optional)

Edit `scripts/workspace_backup.sh` and set your backup targets:

```bash
# WebDAV (e.g., Nextcloud)
WEBDAV_URL="http://your-nextcloud/remote.php/webdav/backup/"
WEBDAV_USER="your_user"
WEBDAV_PASS="your_pass"

# SSH remote
SSH_HOST="your-server"
SSH_PATH="/backups/workspace/"
```

### Step 6: Start Using

1. Start an OpenClaw session
2. The agent reads `BOOTSTRAP.md` and guides you through identity setup
3. After setup, `BOOTSTRAP.md` is deleted
4. The memory system runs automatically from here

## Verification

After installation, check that everything is in place:

```bash
cd ~/.openclaw/workspace

# Templates
ls -la AGENTS.md SOUL.md MEMORY.md HEARTBEAT.md BOOTSTRAP.md

# Scripts
ls -la scripts/*.sh

# Strategy registry
cat strategies.json | python3 -m json.tool | head -5

# Memory directory
ls -la memory/

# Cron jobs
crontab -l | grep openclaw
```

## Uninstall

```bash
# Remove scripts (keep your data!)
rm -rf ~/.openclaw/workspace/scripts/memory_consolidate.sh
rm -rf ~/.openclaw/workspace/scripts/memory_search.sh
rm -rf ~/.openclaw/workspace/scripts/strategy_*.sh
rm -rf ~/.openclaw/workspace/scripts/auto_commit.sh
rm -rf ~/.openclaw/workspace/scripts/workspace_backup.sh
rm -rf ~/.openclaw/workspace/scripts/daily_log_init.sh
rm -f ~/.openclaw/workspace/strategies.json

# Remove cron jobs
crontab -l | grep -v openclaw | crontab -

# Your MEMORY.md, AGENTS.md, SOUL.md etc. are YOUR data — keep them!
```
