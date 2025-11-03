# Claude Code Skills for n8n Automation

This directory contains 7 integrated Claude Code skills that provide instant access to the n8n-skills library.

## 📦 Available Skills

| Skill | Size | Purpose |
|-------|------|---------|
| **n8n-best-practices** | 5.8KB | Critical patterns, debugging, ES5 syntax guide |
| **n8n-skills-catalog** | 9.0KB | Master index and skill finder |
| **anti-scraping** | 4.2KB | Cloudflare bypass, web scraping |
| **ai-integration** | 7.1KB | LLM integration patterns |
| **notion-operations** | 8.5KB | Notion database CRUD |
| **oauth-automation** | 8.1KB | OAuth token management |
| **video-processing** | 9.8KB | YouTube & video analysis |

**Total**: ~53KB of concentrated n8n knowledge

## 🚀 How Skills Work

### Automatic Invocation

Claude Code automatically invokes skills based on your task description. You don't need to manually call them.

**Examples**:
- "I'm getting a Code node error" → `n8n-best-practices` auto-invoked
- "How do I scrape this website?" → `anti-scraping` auto-invoked
- "Need to work with Notion" → `notion-operations` auto-invoked

### Skill Descriptions

Each skill has a description that tells Claude when to use it:

```yaml
name: n8n-best-practices
description: Use when encountering n8n workflow issues, Code node errors,
  HTTP requests failing, data flow problems, environment variables not working,
  JSON parsing errors, or need n8n development patterns
```

## 📚 Skill Contents

Each `SKILL.md` includes:

1. **When to use** - Clear use case description
2. **Quick patterns** - Copy-paste code examples
3. **Best practices** - Dos and don'ts
4. **Troubleshooting** - Common issues and solutions
5. **Integration patterns** - How skills work together
6. **Full documentation links** - Path to complete guides in n8n-skills/

## 🎯 Start Here

### New to n8n?
1. Start with `n8n-best-practices` - Critical knowledge
2. Browse `n8n-skills-catalog` - Discover capabilities
3. Pick specific skills as needed

### Experienced with n8n?
- Claude will auto-invoke skills when relevant
- Use catalog for quick lookup: "What skills are available for X?"
- Check best practices when errors occur

### Building a Workflow?
1. Describe your goal
2. Claude checks catalog for relevant skills
3. Skills provide proven patterns
4. Combine multiple skills as needed

## 🔗 Relationship to n8n-skills/

**Skills (.claude/skills/)** → Quick reference for Claude Code
- Optimized for AI consumption
- Fast lookup during development
- Essential patterns only

**Full Library (n8n-skills/)** → Complete documentation
- Detailed guides
- Full code implementations
- Examples and templates
- 8500+ lines of documentation

**Flow**:
```
Claude encounters task
    ↓
Checks skill descriptions
    ↓
Invokes relevant skill
    ↓
Provides patterns from SKILL.md
    ↓
Links to full documentation if needed
```

## 💡 Usage Examples

### Example 1: Code Node Error
```
User: "My Code node is throwing 'arrow function not supported'"
Claude: [Auto-invokes n8n-best-practices]
        "n8n Code nodes only support ES5. Here's the fix..."
```

### Example 2: Finding the Right Tool
```
User: "I need to process YouTube videos"
Claude: [Auto-invokes n8n-skills-catalog]
        "Use video-processing skill for YouTube..."
        [Then invokes video-processing]
```

### Example 3: Complex Workflow
```
User: "Scrape a site with Cloudflare, analyze with AI, save to Notion"
Claude: [Invokes multiple skills]
        - anti-scraping: Cloudflare bypass pattern
        - ai-integration: Structured output parsing
        - notion-operations: Database creation pattern
```

## 🛠️ Maintenance

### Adding New Skills

1. Create directory: `.claude/skills/new-skill/`
2. Create `SKILL.md` with frontmatter:
```yaml
---
name: new-skill
description: Use when [clear use case description]
---
```
3. Add content: Quick patterns, examples, links
4. Update this README

### Updating Skills

1. Edit relevant `SKILL.md`
2. Keep focused on essential patterns
3. Link to full documentation for details
4. Test with Claude Code

### Syncing with n8n-skills/

When n8n-skills/ is updated:
1. Review changes in relevant modules
2. Update corresponding SKILL.md if needed
3. Keep skills concise - link to full docs

## 📊 Skill Statistics

- **Total Skills**: 7
- **Total Size**: ~53KB
- **Coverage**: 14+ n8n-skills modules
- **Code Examples**: ES5 compatible
- **Documentation Links**: Direct paths to n8n-skills/

## 🎓 Learning Path

**Beginner**:
1. n8n-best-practices (must-read)
2. n8n-skills-catalog (overview)
3. Start with simple skills (data-export, debugging)

**Intermediate**:
1. anti-scraping (web scraping)
2. ai-integration (AI workflows)
3. notion-operations (Notion automation)

**Advanced**:
1. oauth-automation (complex auth)
2. video-processing (media handling)
3. Combine multiple skills

## 🔍 Quick Reference

**When you see these errors** → Use this skill:
- Arrow function error → `n8n-best-practices`
- Template literal error → `n8n-best-practices`
- $http not defined → `n8n-best-practices`
- Cloudflare blocking → `anti-scraping`
- AI output parsing fails → `ai-integration`
- Notion field error → `notion-operations`
- OAuth token expired → `oauth-automation`
- VTT parsing issues → `video-processing`

**When you want to** → Use this skill:
- Fix any n8n issue → `n8n-best-practices`
- Find the right skill → `n8n-skills-catalog`
- Scrape websites → `anti-scraping`
- Integrate LLMs → `ai-integration`
- Work with Notion → `notion-operations`
- Handle OAuth → `oauth-automation`
- Process videos → `video-processing`

## 📞 Support

**Claude Code automatically uses these skills** when relevant. You can also:
- Ask: "What skills are available?"
- Request: "Use the n8n-best-practices skill"
- Browse: Read SKILL.md files directly

## 🔗 Links

- **Full Skills Library**: `/mnt/d/work/n8n_agent/n8n-skills/`
- **Repository Guide**: `/mnt/d/work/n8n_agent/CLAUDE.md`
- **Workflow Agent**: `/mnt/d/work/n8n_agent/n8n-workflow-agent/`

---

**Last Updated**: 2025-11-03
**Maintained By**: Claude Code integration
**Source Library**: n8n-skills v3.1
