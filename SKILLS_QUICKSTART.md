# 📘 Skills 快速使用指南

## ✅ 配置状态

Skills 已在三个位置可用：

1. ✅ **主项目**: `/mnt/d/work/n8n_agent/.claude/skills/`
2. ✅ **n8n-workflow-agent**: `.claude/skills/` → 符号链接
3. ✅ **n8n-skills**: `.claude/skills/` → 符号链接

## 🚀 立即开始使用

### 方式 1: 让 Claude 自动使用（推荐）

在任何目录打开 Claude Code，直接描述问题：

```
📍 在 /mnt/d/work/n8n_agent/n8n-workflow-agent/

你: "我的 Python 脚本调用 n8n API 失败了"
Claude: [自动调用相关 skills]
        提供解决方案
```

### 方式 2: 询问可用 Skills

```
你: "有哪些 n8n skills 可用？"
Claude: [调用 n8n-skills-catalog]
        展示所有 7 个 skills
```

### 方式 3: 针对性提问

```
你: "n8n Code 节点有什么语法限制？"
Claude: [调用 n8n-best-practices]
        "必须使用 ES5，不能用箭头函数、模板字符串..."
```

## 📚 7 个可用 Skills

| Skill | 何时使用 |
|-------|---------|
| **n8n-best-practices** | ANY n8n 问题 - 错误、语法、调试 |
| **n8n-skills-catalog** | 寻找合适的技能或浏览所有能力 |
| **anti-scraping** | 网页抓取、Cloudflare 绕过 |
| **ai-integration** | LLM 集成、结构化输出解析 |
| **notion-operations** | Notion 数据库操作 |
| **oauth-automation** | OAuth 令牌自动刷新 |
| **video-processing** | YouTube 视频处理 |

## 💡 使用示例

### 在 n8n-workflow-agent 开发

```bash
cd /mnt/d/work/n8n_agent/n8n-workflow-agent

# 使用 Claude Code
```

**问题示例**:
- "如何用 Python 创建 n8n 工作流？"
- "n8n API 的最佳实践是什么？"
- "如何处理工作流 JSON 中的 Code 节点？"

### 在 n8n-skills 开发

```bash
cd /mnt/d/work/n8n_agent/n8n-skills

# 使用 Claude Code
```

**问题示例**:
- "这个技能模块的代码需要 ES5 兼容吗？"
- "如何测试 AI 集成代码？"
- "Notion API 调用的错误处理怎么写？"

## 🔍 验证 Skills 可用

```bash
# 检查符号链接
ls -la .claude/skills/

# 查看可用 skills
ls .claude/skills/

# 输出示例：
# README.md
# ai-integration/
# anti-scraping/
# n8n-best-practices/
# n8n-skills-catalog/
# notion-operations/
# oauth-automation/
# video-processing/
```

## 📖 详细文档

- **完整使用指南**: `/mnt/d/work/n8n_agent/SKILLS_USAGE.md`
- **Skills 目录**: `/mnt/d/work/n8n_agent/.claude/skills/`
- **仓库指南**: `/mnt/d/work/n8n_agent/CLAUDE.md`

## 🎯 推荐工作流程

### 开发 n8n-workflow-agent

```bash
cd /mnt/d/work/n8n_agent/n8n-workflow-agent

# 1. 开发 Python 代码
vim tools/n8n_workflow_manager.py

# 2. 遇到问题直接问 Claude
# "这个 n8n API 调用正确吗？"

# 3. Claude 自动使用 skills 提供答案
```

### 开发 n8n-skills

```bash
cd /mnt/d/work/n8n_agent/n8n-skills

# 1. 开发新技能模块
vim new-skill/code.js

# 2. 检查语法要求
# "这段代码在 n8n Code 节点能运行吗？"

# 3. Claude 检查 ES5 兼容性
```

## ⚡ 关键要点

1. ✅ **自动调用**: 无需手动指定，描述问题即可
2. ✅ **三处可用**: 主项目和两个子项目都能用
3. ✅ **自动同步**: 符号链接确保始终最新
4. ✅ **即时帮助**: 遇到 n8n 问题立即获得答案

---

**现在就开始使用！** 在 Claude Code 中直接描述你的 n8n 开发问题即可。
