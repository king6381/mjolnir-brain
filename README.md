# 🧠 雷神之脑 Mjolnir Brain

**AI Agent 自进化记忆系统** — 让你的 AI 助手拥有持久记忆、自我学习和自动纠错能力。

> 雷神三件套: ⚒️ 雷神之锤 (Private) · 🛡️ [雷神之盾](https://github.com) · 🧠 **雷神之脑**

---

## ✨ 特性

- 🧠 **分层记忆架构** — 会话日志 → 长期记忆 → 规则文件，三层沉淀
- 🔄 **自我进化协议** — 犯过的错自动记录，不犯第二次
- 📝 **Write-Through** — 学到即写入，不丢失任何洞察
- 🎯 **策略注册表** — 问题→解法映射，带成功率追踪，越用越准
- 💓 **心跳系统** — 定期自检、知识提炼、空闲任务队列
- 🤖 **AI 真摘要** — 自动提炼日志精华，不是原文复制
- 📦 **双目标备份** — 支持 WebDAV + SSH 双通道容灾
- 🔍 **模糊搜索** — 多源记忆检索，支持归档搜索

## 📁 项目结构

```
mjolnir-brain/
├── README.md                    # 本文件
├── INSTALL.md                   # 安装指南
├── templates/                   # 📋 开箱即用的模板文件
│   ├── AGENTS.md                # 行为规则 + 自进化协议
│   ├── SOUL.md                  # 人格定义框架
│   ├── BOOTSTRAP.md             # 首次启动引导
│   ├── IDENTITY.md              # 身份模板
│   ├── USER.md                  # 用户档案模板
│   ├── MEMORY.md                # 长期记忆模板 (分章节结构)
│   ├── HEARTBEAT.md             # 心跳检查 + 空闲任务队列
│   └── memory/                  # 记忆目录模板
│       └── .gitkeep
├── scripts/                     # 🔧 自动化脚本
│   ├── memory_consolidate.sh    # 记忆提炼 (清理+标记+容量检查)
│   ├── memory_search.sh         # 模糊搜索工具
│   ├── strategy_lookup.sh       # 策略查询
│   ├── strategy_update.sh       # 策略成功率更新
│   ├── auto_commit.sh           # Git 自动提交
│   ├── workspace_backup.sh      # 双目标备份
│   └── daily_log_init.sh        # 日志模板初始化
├── strategies.json              # 🎯 策略注册表 (示例)
├── playbooks/                   # 📖 操作手册模板
│   └── README.md
├── docs/                        # 📚 详细文档
│   ├── architecture.md          # 架构设计
│   ├── self-learning.md         # 自学习机制详解
│   └── best-practices.md        # 最佳实践
└── skill/                       # 🦞 OpenClaw Skill 打包
    └── SKILL.md
```

## 🚀 快速开始

### 方式一: OpenClaw Skill 安装 (推荐)

```bash
clawdhub install mjolnir-brain
```

### 方式二: 手动安装

```bash
# 克隆仓库
git clone https://github.com/YOUR_USER/mjolnir-brain.git

# 复制模板到你的 OpenClaw workspace
cp -r mjolnir-brain/templates/* ~/.openclaw/workspace/
cp -r mjolnir-brain/scripts ~/.openclaw/workspace/
cp mjolnir-brain/strategies.json ~/.openclaw/workspace/

# 设置脚本权限
chmod +x ~/.openclaw/workspace/scripts/*.sh

# 配置 cron (可选)
crontab -e
# 添加:
# 0 * * * * ~/.openclaw/workspace/scripts/auto_commit.sh
# 0 4 * * * ~/.openclaw/workspace/scripts/memory_consolidate.sh
# 0 4 * * * ~/.openclaw/workspace/scripts/workspace_backup.sh
```

### 首次使用

1. 启动 OpenClaw 会话
2. Agent 会自动读取 `BOOTSTRAP.md`，引导你完成身份设定
3. 设定完成后 `BOOTSTRAP.md` 自动删除
4. 开始使用！记忆系统自动运行

## 🏗️ 架构

```
┌─────────────────────────────────────────────┐
│                  AI Agent                    │
│  ┌──────────┐  ┌──────────┐  ┌───────────┐ │
│  │ SOUL.md  │  │ AGENTS.md│  │ TOOLS.md  │ │
│  │ 人格     │  │ 行为规则 │  │ 工具配置  │ │
│  └────┬─────┘  └────┬─────┘  └─────┬─────┘ │
│       └──────────────┼──────────────┘       │
│              ┌───────▼───────┐              │
│              │  MEMORY.md    │ ≤20KB        │
│              │  长期记忆精华  │              │
│              └───────┬───────┘              │
│       ┌──────────────┼──────────────┐       │
│  ┌────▼─────┐  ┌─────▼────┐  ┌─────▼─────┐│
│  │Daily Logs│  │strategies│  │ playbooks ││
│  │日志原文  │  │策略注册表│  │ 操作手册  ││
│  └──────────┘  └──────────┘  └───────────┘│
│                                             │
│  ┌──────────────────────────────────────┐  │
│  │  Cron: 提炼 + 备份 + Git + 清理      │  │
│  └──────────────────────────────────────┘  │
└─────────────────────────────────────────────┘
```

### 记忆生命周期

```
会话交互 → 即时写入 daily log (Write-Through)
         → 每日 AI 提炼精华 → MEMORY.md
         → 错误/教训 → strategies.json / AGENTS.md
         → 高频操作 → playbooks/
         → 30天归档 → memory/archive/
```

## 📊 效果数据 (来自真实使用)

| 指标 | 数值 |
|------|------|
| 每次启动读取量 | ~10K tokens |
| 长期记忆容量 | ≤20KB (结构化精华) |
| 错误复犯率 | 0% (已记录的错误) |
| 策略自动解决率 | ~70% (已知问题) |
| 外部依赖 | 零 (纯 markdown + json + bash) |

## 🤝 雷神三件套

| 项目 | 定位 | 状态 |
|------|------|------|
| ⚒️ 雷神之锤 Mjolnir Hammer | 量化分析系统 | Private |
| 🛡️ 雷神之盾 Mjolnir Shield | 加密安全系统 | [GitHub](https://github.com) |
| 🧠 **雷神之脑 Mjolnir Brain** | **AI 记忆智能** | **本项目** |

## 📄 License

MIT License

## ⭐ Star History

如果这个项目对你有帮助，请给一个 Star！
