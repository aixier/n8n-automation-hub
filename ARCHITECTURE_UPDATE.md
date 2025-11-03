# 📐 文档架构更新说明

**日期**: 2025-11-03
**更新**: 统一 CLAUDE.md 为单一入口点

## ✅ 完成的更改

### 1. 主项目 CLAUDE.md - 单一真实来源

**位置**: `/mnt/d/work/n8n_agent/CLAUDE.md`

**内容**:
- ⚠️ 标记为"单一真实来源"
- 🔥 7个Claude Code Skills说明
- 📦 完整的n8n-workflow-agent指南
  - 关键工作流模式
  - 所有命令
  - Python工具架构
  - 强制要求和安全规范
- 📚 完整的n8n-skills指南
  - 技能查找和使用
  - 所有14+技能模块
  - 集成模式

### 2. 子模块 CLAUDE.md - 重定向文件

**n8n-workflow-agent/CLAUDE.md**:
- ⚠️ 重定向到主项目
- 📍 清晰的路径指引: `../../CLAUDE.md`
- 🔗 快速导航命令
- 💡 使用模式说明

**n8n-skills/CLAUDE.md**:
- ⚠️ 重定向到主项目
- 📍 清晰的路径指引: `../../CLAUDE.md`
- 🔗 快速导航命令
- 💡 使用模式说明

### 3. Skills 符号链接配置

```
n8n-workflow-agent/.claude/skills/ → ../../.claude/skills/
n8n-skills/.claude/skills/ → ../../.claude/skills/
```

## 🎯 架构优势

### Before (分散)
```
主项目/CLAUDE.md             (437行)
└── 基本架构说明

n8n-workflow-agent/CLAUDE.md (353行)
└── 工作流管理详细指南

n8n-skills/
└── (没有CLAUDE.md)
```

**问题**:
- ❌ 内容重复
- ❌ 维护困难
- ❌ 可能不同步
- ❌ 不知道哪个是权威

### After (统一)
```
主项目/CLAUDE.md             (546行 - 统一入口)
├── Skills 说明
├── n8n-workflow-agent 完整指南
└── n8n-skills 完整指南

n8n-workflow-agent/CLAUDE.md (77行 - 重定向)
└── 指向 ../../CLAUDE.md

n8n-skills/CLAUDE.md         (90行 - 重定向)
└── 指向 ../../CLAUDE.md
```

**优势**:
- ✅ 单一真实来源
- ✅ 无重复内容
- ✅ 易于维护
- ✅ 始终同步
- ✅ 清晰层次

## 📖 使用方式

### 场景 1: 在主项目工作

```bash
cd /mnt/d/work/n8n_agent

# Claude Code 自动读取 CLAUDE.md
# 包含所有指导内容
```

### 场景 2: 在 n8n-workflow-agent 工作

```bash
cd /mnt/d/work/n8n_agent/n8n-workflow-agent

# Claude Code 读取本地 CLAUDE.md
# 发现是重定向文件
# 自动参考主项目的 CLAUDE.md
```

### 场景 3: 在 n8n-skills 工作

```bash
cd /mnt/d/work/n8n_agent/n8n-skills

# Claude Code 读取本地 CLAUDE.md
# 发现是重定向文件
# 自动参考主项目的 CLAUDE.md
```

## 🔄 工作流程

### 更新指导内容

**只需编辑一个文件**: `/mnt/d/work/n8n_agent/CLAUDE.md`

```bash
cd /mnt/d/work/n8n_agent

# 编辑主 CLAUDE.md
vim CLAUDE.md

# 提交
git add CLAUDE.md
git commit -m "docs: Update guidance"
git push

# 完成！所有项目自动获得更新
```

### 添加新的 workflow-agent 命令

在主 CLAUDE.md 中找到 `### n8n-workflow-agent (Python Agent)` 部分并更新。

### 添加新的技能说明

在主 CLAUDE.md 中找到 `### n8n-skills (Skills Library)` 部分并更新。

## 📊 文件统计

| 文件 | 行数 | 角色 |
|------|------|------|
| 主项目/CLAUDE.md | 546 | 权威文档 |
| n8n-workflow-agent/CLAUDE.md | 77 | 重定向 |
| n8n-skills/CLAUDE.md | 90 | 重定向 |
| **总计** | **713** | - |

**节省**: 不再重复 ~300 行内容

## 🔗 相关提交

### 主项目
```
4951db7 refactor: Centralize all guidance in main CLAUDE.md
ba452c4 feat: Update submodules with unified CLAUDE.md structure
```

### n8n-workflow-agent
```
1da3bd0 refactor: Replace CLAUDE.md with redirect to main project
```

### n8n-skills
```
5f04632 docs: Add CLAUDE.md redirect to main project
```

## 💡 最佳实践

### ✅ DO

1. **更新指导时**: 只编辑主项目的 CLAUDE.md
2. **查找内容时**: 总是参考主 CLAUDE.md
3. **添加新功能时**: 更新主 CLAUDE.md 相应部分
4. **维护子模块时**: 保持重定向文件不变

### ❌ DON'T

1. **不要**: 编辑子模块的 CLAUDE.md 添加内容
2. **不要**: 在子模块创建详细指导
3. **不要**: 让文档在多处重复
4. **不要**: 删除重定向文件

## 🎓 学习路径

### 新用户

1. 克隆主项目（包含 submodules）
   ```bash
   git clone --recursive https://github.com/aixier/n8n-automation-hub.git
   ```

2. 阅读主 CLAUDE.md
   ```bash
   cd n8n-automation-hub
   cat CLAUDE.md
   ```

3. 根据需要进入子项目工作
   - Claude Code 自动参考主 CLAUDE.md
   - Skills 通过符号链接可用

### 维护者

1. 所有文档更新在主 CLAUDE.md
2. 子模块的重定向文件保持不变
3. 定期同步 Skills 到子项目

## 📞 问题排查

### Q: Claude Code 找不到指导？

A: 检查当前目录的 CLAUDE.md：
```bash
cat CLAUDE.md
# 应该看到重定向信息或完整内容
```

### Q: 子模块的 CLAUDE.md 太简单？

A: 这是设计如此！重定向到主项目获取完整指导：
```bash
cat ../../CLAUDE.md
```

### Q: 如何更新子项目的指导？

A: 更新主项目的 CLAUDE.md，然后：
```bash
cd /mnt/d/work/n8n_agent
git add CLAUDE.md
git commit -m "docs: Update guidance"
git push

# 子模块自动获得更新（通过重定向）
```

## 🎉 总结

**单一真实来源架构已完成！**

- ✅ 主 CLAUDE.md 统一所有指导
- ✅ 子模块通过重定向引用
- ✅ Skills 通过符号链接共享
- ✅ 所有更改已推送到 GitHub

**GitHub 仓库**: https://github.com/aixier/n8n-automation-hub

---

**架构更新完成！** 所有文档现在统一、清晰、易于维护。
