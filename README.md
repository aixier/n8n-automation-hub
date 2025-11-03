# n8n Automation Hub

**Monorepo for n8n workflow automation with Claude Code integration**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Code](https://img.shields.io/badge/Claude-Code-purple.svg)](https://claude.com/claude-code)
[![n8n](https://img.shields.io/badge/n8n-compatible-orange.svg)](https://n8n.io/)

## 🌟 Overview

This monorepo combines three powerful components for n8n automation:

1. **Claude Code Skills** - 7 integrated skills for instant n8n knowledge access
2. **n8n-skills** - Reusable workflow code modules (14+ battle-tested patterns)
3. **n8n-workflow-agent** - Python tool for programmatic workflow management

## 🚀 Quick Start

### Clone with Submodules

```bash
git clone --recursive https://github.com/YOUR_USERNAME/n8n-automation-hub.git
cd n8n-automation-hub
```

If you already cloned without `--recursive`:
```bash
git submodule update --init --recursive
```

### Use Claude Code Skills

The integrated skills are automatically available when using Claude Code in this repository:

- **n8n-best-practices** - Critical patterns and debugging (use for ANY n8n issue)
- **n8n-skills-catalog** - Browse all available skills
- **anti-scraping** - Web scraping with Cloudflare bypass
- **ai-integration** - LLM integration patterns
- **notion-operations** - Notion database operations
- **oauth-automation** - OAuth token management
- **video-processing** - YouTube & video analysis

Just describe your n8n task, and Claude will automatically invoke relevant skills.

### Explore n8n Skills

```bash
cd n8n-skills
cat README.md  # Full skill catalog
ls -la         # Browse 14+ skill modules
```

### Use Workflow Agent

```bash
cd n8n-workflow-agent
pip install -r requirements.txt
python tools/n8n_workflow_manager.py --help
```

## 📚 Documentation

- **[CLAUDE.md](./CLAUDE.md)** - Complete repository guide for Claude Code
- **[.claude/skills/](./.claude/skills/)** - Claude Code skills (7 skills, ~53KB)
- **[n8n-skills/](./n8n-skills/)** - Full skills library (14+ modules, 8500+ lines)
- **[n8n-workflow-agent/](./n8n-workflow-agent/)** - Python agent documentation

## 🏗️ Architecture

```
n8n-automation-hub/
├── .claude/skills/          # Claude Code skills (automatic access)
│   ├── n8n-best-practices/
│   ├── n8n-skills-catalog/
│   ├── anti-scraping/
│   ├── ai-integration/
│   ├── notion-operations/
│   ├── oauth-automation/
│   └── video-processing/
│
├── n8n-skills/             # Submodule: Code library
│   ├── anti-scraping/
│   ├── ai-integration/
│   ├── notion-operations/
│   ├── video-processing/
│   └── ... (14+ modules)
│
└── n8n-workflow-agent/     # Submodule: Python tool
    ├── tools/
    ├── templates/
    └── docs/
```

## 💡 Why This Architecture?

**n8n workflows can't be directly shared** (due to credential IDs), so we maintain:

1. **Environment-agnostic code** (n8n-skills) - Uses `$env` variables, works anywhere
2. **Workflow generation tool** (n8n-workflow-agent) - Creates workflow JSON programmatically
3. **Claude Code integration** - Instant access to proven patterns

## 🎯 Common Use Cases

### Web Scraping Pipeline
```
anti-scraping → html-parsing → data-processing → data-export
```

### AI Content Analysis
```
input → ai-integration → notion-operations
```

### YouTube Video Intelligence
```
oauth-automation → video-processing → ai-integration → notion-operations
```

### Database Synchronization
```
schedule → notion-database-sync → target database
```

## 🛠️ Key Features

- ✅ **7 Claude Code Skills** - Automatic invocation when relevant
- ✅ **14+ Production Skills** - Battle-tested code modules
- ✅ **ES5 Compatible** - All code works in n8n Code nodes
- ✅ **Complete Documentation** - 8500+ lines of guides
- ✅ **Python Automation** - Programmatic workflow management
- ✅ **Submodule Architecture** - Clean separation, easy updates

## 📖 Learn More

### For Claude Code Users
1. Read [CLAUDE.md](./CLAUDE.md)
2. Browse `.claude/skills/` for quick references
3. Explore `n8n-skills/` for complete implementations

### For n8n Developers
1. Start with `n8n-skills/n8n-best-practices/` (critical!)
2. Browse `n8n-skills/README.md` for skill catalog
3. Copy code from skill modules into n8n Code nodes

### For Automation Engineers
1. Set up `n8n-workflow-agent/`
2. Use Python tools for workflow management
3. Combine with skills for rapid development

## 🤝 Contributing

Each submodule has its own contribution guidelines:

- **n8n-skills**: [n8n-skills/CONTRIBUTING.md](./n8n-skills/CONTRIBUTING.md)
- **n8n-workflow-agent**: [n8n-workflow-agent/CONTRIBUTING.md](./n8n-workflow-agent/CONTRIBUTING.md)

## 📄 License

MIT License - see [LICENSE](./LICENSE) for details

## 🔗 Submodule Repositories

- **n8n-skills**: https://github.com/aixier/n8n-skills
- **n8n-workflow-agent**: https://github.com/aixier/n8n-workflow-agent

## 🙏 Acknowledgments

- [n8n](https://n8n.io/) - The workflow automation platform
- [Claude Code](https://claude.com/claude-code) - AI-powered coding assistant
- [Anthropic](https://anthropic.com/) - Advanced language understanding

---

**Built with ❤️ using Claude Code**

⭐ Star this repo if you find it useful!
