# Skills 使用指南

本文档说明如何在不同场景下使用 Claude Code Skills。

## 📚 Skills 概览

项目提供 **7 个 Claude Code Skills**：
- `n8n-best-practices` - n8n 核心模式和调试
- `n8n-skills-catalog` - 技能索引和快速查找
- `anti-scraping` - 网页抓取和 Cloudflare 绕过
- `ai-integration` - LLM 集成模式
- `notion-operations` - Notion 数据库操作
- `oauth-automation` - OAuth 令牌管理
- `video-processing` - YouTube 视频处理

## 🎯 使用场景

### 场景 1: 在主项目中工作（推荐）

**目录**: `/mnt/d/work/n8n_agent/`

**Skills 位置**: `.claude/skills/`

**使用方式**: ✅ **自动可用**

当你在主项目目录使用 Claude Code 时，所有 skills 会自动加载和调用。

```bash
# 在主项目目录工作
cd /mnt/d/work/n8n_agent

# 使用 Claude Code
# Skills 自动可用，无需额外配置
```

**示例**:
```
你: "我的 n8n Code 节点报错了"
Claude: [自动调用 n8n-best-practices skill]
        提供 ES5 语法修复方案
```

### 场景 2: 在 n8n-workflow-agent 子项目独立工作

**目录**: `/mnt/d/work/n8n_agent/n8n-workflow-agent/`

**问题**: 子项目没有 .claude/skills 目录

**解决方案**: 创建符号链接

#### 方案 A: 符号链接（推荐）

```bash
cd /mnt/d/work/n8n_agent/n8n-workflow-agent

# 创建 .claude 目录（如果不存在）
mkdir -p .claude

# 创建符号链接指向主项目的 skills
ln -s ../../.claude/skills .claude/skills

# 验证
ls -la .claude/skills
```

**优点**:
- ✅ Skills 始终保持最新
- ✅ 不占用额外空间
- ✅ 修改自动同步

**注意**:
- Windows WSL 下需要使用绝对路径
- 符号链接不会被 git 跟踪（已在 .gitignore 中）

#### 方案 B: 工作在主项目，访问子模块

```bash
# 推荐方式：始终在主项目目录工作
cd /mnt/d/work/n8n_agent

# 访问 n8n-workflow-agent 的文件
code n8n-workflow-agent/tools/n8n_workflow_manager.py

# Skills 自动可用
```

### 场景 3: 在 n8n-skills 子项目独立工作

**目录**: `/mnt/d/work/n8n_agent/n8n-skills/`

**使用方式**: 同样创建符号链接

```bash
cd /mnt/d/work/n8n_agent/n8n-skills

# 创建 .claude 目录
mkdir -p .claude

# 创建符号链接
ln -s ../../.claude/skills .claude/skills
```

## 🛠️ 配置步骤（一次性）

### 为两个子项目配置 Skills

```bash
# 进入主项目
cd /mnt/d/work/n8n_agent

# 为 n8n-workflow-agent 配置
cd n8n-workflow-agent
mkdir -p .claude
ln -s ../../.claude/skills .claude/skills
cd ..

# 为 n8n-skills 配置
cd n8n-skills
mkdir -p .claude
ln -s ../../.claude/skills .claude/skills
cd ..

# 验证配置
echo "=== n8n-workflow-agent ==="
ls -la n8n-workflow-agent/.claude/skills/ | head -5

echo "=== n8n-skills ==="
ls -la n8n-skills/.claude/skills/ | head -5
```

### 更新 .gitignore（子项目）

在子项目的 `.gitignore` 中添加：

```bash
# n8n-workflow-agent/.gitignore
.claude/skills/  # 符号链接，不提交

# n8n-skills/.gitignore
.claude/skills/  # 符号链接，不提交
```

## 📖 Skills 自动调用机制

### Claude Code 如何使用 Skills

Claude Code 会根据任务描述**自动调用**相关 skills：

```yaml
# n8n-best-practices/SKILL.md
---
name: n8n-best-practices
description: Use when encountering n8n workflow issues, Code node errors,
  HTTP requests failing, data flow problems, environment variables not working
---
```

当你的问题匹配 `description` 时，Claude 自动调用该 skill。

### 示例对话

**场景 1: 代码错误**
```
你: "我的代码用了箭头函数，n8n 报错了"
Claude: [检测到 "n8n" + "报错"]
        [自动调用 n8n-best-practices]
        "n8n Code 节点只支持 ES5。这里是修复方案..."
```

**场景 2: 寻找工具**
```
你: "我需要抓取一个有 Cloudflare 保护的网站"
Claude: [检测到 "抓取" + "Cloudflare"]
        [自动调用 n8n-skills-catalog 找到 anti-scraping]
        [调用 anti-scraping 提供方案]
        "使用 Playwright 绕过 Cloudflare..."
```

**场景 3: 复杂工作流**
```
你: "我要做一个工作流：抓取网站 → AI 分析 → 保存到 Notion"
Claude: [检测到多个关键词]
        [调用 anti-scraping]
        [调用 ai-integration]
        [调用 notion-operations]
        "这个工作流需要组合三个技能..."
```

## 🔍 手动查阅 Skills

虽然 Claude 会自动调用，但你也可以直接查看：

```bash
# 查看所有 skills
ls -la .claude/skills/

# 查看特定 skill
cat .claude/skills/n8n-best-practices/SKILL.md

# 查看 skills 索引
cat .claude/skills/n8n-skills-catalog/SKILL.md

# 搜索关键词
grep -r "OAuth" .claude/skills/*/SKILL.md
grep -r "Cloudflare" .claude/skills/*/SKILL.md
```

## 🎓 最佳实践

### ✅ 推荐做法

1. **始终在主项目工作**
   ```bash
   cd /mnt/d/work/n8n_agent  # 在这里工作
   code n8n-workflow-agent/  # 访问子项目文件
   ```

2. **让 Claude 自动调用 Skills**
   - 描述你的问题
   - Claude 会自动使用相关 skills
   - 无需手动指定

3. **遇到 n8n 问题先问 Claude**
   ```
   "我的 Code 节点报错: XXX"
   "如何处理 OAuth token 过期？"
   "需要抓取有反爬虫的网站"
   ```

### ❌ 避免做法

1. **不要直接复制 skills 到子项目**
   - 会导致同步问题
   - 浪费空间
   - 使用符号链接代替

2. **不要修改 skill 文件**
   - Skills 是只读参考
   - 需要修改时，在你的代码中实现
   - 或提交 PR 到主项目

## 🔄 更新 Skills

### 主项目更新 Skills

```bash
cd /mnt/d/work/n8n_agent

# 编辑 skill
vim .claude/skills/n8n-best-practices/SKILL.md

# 提交更改
git add .claude/skills/
git commit -m "docs: Update n8n-best-practices skill"
git push
```

### 子项目自动同步

使用符号链接时，子项目会**自动同步**主项目的更改：

```bash
cd n8n-workflow-agent
ls -la .claude/skills/  # 显示主项目的最新版本
```

## 📊 Skills 位置总结

```
/mnt/d/work/n8n_agent/
├── .claude/skills/                    # ✅ 主 Skills 目录
│   ├── n8n-best-practices/
│   ├── n8n-skills-catalog/
│   └── ...
│
├── n8n-workflow-agent/
│   └── .claude/skills/ → ../../.claude/skills/  # 符号链接
│
└── n8n-skills/
    └── .claude/skills/ → ../../.claude/skills/  # 符号链接
```

## 🚀 快速开始

### 新用户设置（3 步）

```bash
# 1. 克隆主项目（包含 submodules）
git clone --recursive https://github.com/aixier/n8n-automation-hub.git
cd n8n-automation-hub

# 2. 为子项目创建符号链接（可选，推荐在主项目工作）
cd n8n-workflow-agent && mkdir -p .claude && ln -s ../../.claude/skills .claude/skills && cd ..
cd n8n-skills && mkdir -p .claude && ln -s ../../.claude/skills .claude/skills && cd ..

# 3. 开始使用 Claude Code
# Skills 自动可用！
```

### 验证 Skills 可用

在 Claude Code 中测试：

```
你: "有哪些 n8n skills 可用？"
Claude: [调用 n8n-skills-catalog]
        显示所有可用 skills 列表
```

## 💡 常见问题

### Q: 符号链接在 Windows 上能用吗？

A: 在 WSL 中可以。如果在 Windows 原生环境，建议：
- 使用 WSL
- 或在主项目目录工作

### Q: 子项目独立克隆后如何使用 skills？

A: 有两种方式：
1. 同时克隆主项目，创建符号链接
2. 将 `.claude/skills/` 复制到子项目（需手动同步）

### Q: Skills 会自动更新吗？

A:
- 主项目中：通过 git pull 更新
- 符号链接：自动同步主项目
- 复制的：需手动重新复制

### Q: 如何知道 Claude 使用了哪个 skill？

A: Claude 的回答通常会包含相关信息，或者你可以问：
```
你: "你刚才用了哪个 skill？"
```

## 🔗 相关文档

- **主项目**: `/mnt/d/work/n8n_agent/CLAUDE.md`
- **Skills 目录**: `/mnt/d/work/n8n_agent/.claude/skills/`
- **n8n-skills 库**: `/mnt/d/work/n8n_agent/n8n-skills/`
- **Workflow Agent**: `/mnt/d/work/n8n_agent/n8n-workflow-agent/`

---

**总结**: 推荐在主项目目录工作，Skills 会自动可用。如需在子项目独立工作，使用符号链接。
