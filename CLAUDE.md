# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 🔥 Claude Code Skills Available

This repository includes **7 integrated Claude Code skills** for n8n automation. Claude will automatically invoke these skills when relevant to your task.

**Quick Access**:
- **n8n-best-practices** - Use for ANY n8n issue (errors, syntax, debugging)
- **n8n-skills-catalog** - Browse all available skills and patterns
- **anti-scraping** - Web scraping with Cloudflare bypass
- **ai-integration** - LLM integration patterns
- **notion-operations** - Notion database operations
- **oauth-automation** - OAuth token management
- **video-processing** - YouTube & video analysis

**How to use**: Just describe your n8n task, and Claude will automatically invoke the relevant skill if needed. Skills provide instant access to battle-tested patterns and solutions.

## Repository Overview

This is a **monorepo** containing two complementary n8n automation projects:

1. **n8n-workflow-agent/** - Python-based AI agent for programmatic workflow creation and management
2. **n8n-skills/** - Reusable n8n workflow code modules and patterns library
3. **.claude/skills/** - Claude Code skills (integrated access to n8n-skills)

### Project Relationship

```
┌─────────────────────────────────────────────────────┐
│  n8n-workflow-agent (Python)                        │
│  - Workflow lifecycle management via n8n API        │
│  - Programmatic node construction                   │
│  - Automated testing and analysis                   │
│  - Natural language → workflow generation (future)  │
└─────────────────────────────────────────────────────┘
                        ↓ Uses
┌─────────────────────────────────────────────────────┐
│  n8n-skills (JavaScript/Documentation)              │
│  - 14+ production-ready code modules                │
│  - Anti-scraping, AI integration, OAuth, etc.       │
│  - n8n best practices and patterns                  │
│  - Copy-paste ready Code node implementations       │
└─────────────────────────────────────────────────────┘
```

**Key Insight**: n8n workflows cannot be directly shared across instances (due to credential IDs), so we maintain:
- **n8n-skills** for environment-agnostic code logic (uses `$env` variables)
- **n8n-workflow-agent** for generating workflow JSON programmatically

## Essential Commands

### n8n-workflow-agent (Python Agent)

#### Environment Setup
```bash
cd n8n-workflow-agent

# Quick setup (recommended)
bash scripts/quick_start.sh

# Manual setup
cp config/.env.example config/.env
# Edit config/.env to set N8N_BASE_URL and N8N_API_KEY
pip install -r requirements.txt

# Test connection
python tools/n8n_workflow_manager.py test
```

#### Workflow Management
```bash
# List all workflows
python tools/n8n_workflow_manager.py list

# Create workflow from JSON config
python tools/n8n_workflow_manager.py create workflow_config.json --activate

# Update existing workflow
python tools/n8n_workflow_manager.py update WORKFLOW_ID changes.json

# Backup workflow
python tools/n8n_workflow_manager.py backup WORKFLOW_ID

# Import workflow
python tools/n8n_workflow_manager.py import workflow.json
```

#### Node Building (Programmatic)
```python
from tools.node_builder import NodeBuilder

builder = NodeBuilder()
webhook = builder.build_webhook_node('/api/webhook')
code = builder.build_code_node('// JavaScript code here')
builder.chain_nodes([webhook['id'], code['id']])
workflow = builder.build_workflow('My Workflow')
```

#### Workflow Analysis
```bash
# Analyze workflow for issues and optimization
python tools/workflow_analyzer.py workflow.json --output report.md

# Includes: complexity, performance, security, optimization suggestions
```

#### Testing
```bash
# Run test suite
python tools/test_runner.py test_scenarios.json

# Parallel testing
python tools/test_runner.py test_scenarios.json --parallel

# HTML report
python tools/test_runner.py test_scenarios.json --format html --output report.html
```

### n8n-skills (Skills Library)

#### Finding Skills
```bash
cd n8n-skills

# View all available skills
ls -la

# Read main skill catalog
cat README.md

# Search for specific functionality
grep -r "oauth" */README.md
grep -r "cloudflare" */README.md
```

#### Using Skills
Skills are JavaScript code modules designed to be copied into n8n Code nodes:

1. Navigate to skill directory (e.g., `cd ai-integration`)
2. Read `README.md` for usage instructions
3. Copy code from `.js` files into n8n Code nodes
4. Configure environment variables as documented
5. Test in n8n workflow

#### Key Skills by Category

**Web Scraping:**
- `anti-scraping/` - Cloudflare bypass with Playwright
- `pagination/` - Multi-page scraping patterns
- `html-parsing/` - Cheerio-based HTML extraction

**AI Integration:**
- `ai-integration/` - LLM integration patterns (OpenAI, Qwen, Claude)
- `video-processing/` - YouTube subtitle/video analysis
- `idea-generation/` - AI-powered content clustering

**Platform Integration:**
- `notion-operations/` - Notion database CRUD operations
- `notion-link-analysis/` - URL → AI analysis → Notion automation
- `feishu-integration/` - Feishu/Lark messaging
- `n8n-oauth-automation/` - OAuth token auto-refresh

**Utilities:**
- `error-handling/` - Retry logic with exponential backoff
- `data-processing/` - Deduplication and aggregation
- `data-export/` - CSV export with proper escaping
- `debugging/` - Data inspection and validation

**Documentation:**
- `n8n-best-practices/` - **READ THIS FIRST** for n8n development patterns

## Architecture

### n8n-workflow-agent Architecture

**Analysis Modules** (`docs/ANALYSIS_*.md`):
- Mandatory sequential processing for workflow creation
- `ANALYSIS_REQUIREMENTS.md` - Parse user requirements
- `ANALYSIS_NODES.md` - Design node configuration
- `ANALYSIS_DATAFLOW.md` - Plan data transformations
- `ANALYSIS_TESTING.md` - Generate test scenarios

**Python Tools** (`tools/`):
- `n8n_workflow_manager.py` (596 lines) - Workflow lifecycle via n8n API
- `node_builder.py` (569 lines) - Programmatic node construction
- `workflow_analyzer.py` (667 lines) - Performance and security analysis
- `test_runner.py` (552 lines) - Automated testing framework

**Configuration** (`config/`):
- `.env.example` - Environment variable template
- `agent_config.yaml` - Agent behavior configuration

**Templates** (`templates/`):
- `workflow_config.json` - Base workflow structure
- `node_mappings.json` - Node type definitions
- `test_scenarios.json` - Test case templates

### n8n-skills Architecture

**14 Skill Modules** - Each contains:
- `README.md` - Detailed documentation and usage guide
- `*.js` files - Copy-paste ready JavaScript code
- Examples and configuration templates (some modules)

**Key Documentation:**
- `README.md` - Complete skill catalog with search guide
- `QUICK_START.md` - Getting started guide
- `SKILLS_RETRIEVAL_GUIDE.md` - When and how to use skills
- `n8n-best-practices/README.md` - **Critical reference** for n8n patterns

## Critical Workflow Patterns

### Workflow Creation Pattern (Python Agent)

```python
# 1. Read analysis modules (mandatory sequence)
Read docs/ANALYSIS_REQUIREMENTS.md
Read docs/ANALYSIS_NODES.md
Read docs/ANALYSIS_DATAFLOW.md
Read docs/ANALYSIS_TESTING.md

# 2. Generate workflow config manually
Write workflow_config.json  # Based on analysis

# 3. Execute creation
python tools/n8n_workflow_manager.py create workflow_config.json --activate

# 4. Run tests
python tools/test_runner.py test_scenarios.json
```

### n8n Best Practices (Skills Library)

**ALWAYS check n8n-best-practices FIRST when:**
- Encountering Code node errors
- HTTP requests failing
- Data flow issues
- Environment variables not working
- JSON parsing errors
- gzip compression problems

**Key Patterns:**
```javascript
// ✅ Correct HTTP request in Code node
const https = require('https');
const options = {
  hostname: 'api.example.com',
  path: '/endpoint',
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  }
};

// ❌ DO NOT use $http (not available in Code nodes)
// ❌ DO NOT use axios (not available)

// ✅ ES5 Syntax (Code nodes don't support ES6+)
var result = items.map(function(item) {
  return item.value;
});

// ❌ DO NOT use arrow functions
// ❌ DO NOT use template literals
// ❌ DO NOT use const/let (use var)

// ✅ Environment variables
const API_KEY = $env.OPENAI_API_KEY;

// ❌ DO NOT hardcode credentials
```

## Development Guidelines

### For Python Agent Development

1. **Analysis Phase is Mandatory**: Never skip reading the analysis modules when creating workflows
2. **Manual Configuration**: Always create config files manually using Write tool (never automate)
3. **Testing Required**: Every workflow must have test scenarios before deployment
4. **Always Backup**: Backup before modifying existing workflows
5. **Error Handling**: All workflows must include error handler nodes

### For n8n Skills Development

1. **Use Claude Code Skills**: Skills are automatically available - Claude will invoke them when relevant
2. **Check Skills First**: Before implementing any n8n functionality, use `n8n-skills-catalog` skill or search `n8n-skills/` directory
3. **Read Best Practices**: Always start with `n8n-best-practices` skill for any n8n issue
4. **Use Environment Variables**: Never hardcode credentials (use `$env.VARIABLE_NAME`)
5. **ES5 Compatibility**: n8n Code nodes require ES5 JavaScript (no arrow functions, template literals)
6. **Test in n8n**: All code must be tested in actual n8n environment before committing

**Skill Usage Pattern**:
- Any n8n error → Claude auto-invokes `n8n-best-practices`
- Need to find a skill → Claude auto-invokes `n8n-skills-catalog`
- Specific task → Claude auto-invokes relevant skill (anti-scraping, ai-integration, etc.)

### Security Requirements

- Never hardcode credentials - use `$env` variables
- Always validate input data with schema validation
- Implement rate limiting for webhook endpoints
- Use authentication for external API access
- Run security analysis with `workflow_analyzer.py`

## Common Skill Combinations

### Web Scraping Pipeline
```
anti-scraping → pagination → html-parsing →
data-processing → data-export
```

### YouTube Video Analysis
```
n8n-oauth-automation → video-processing →
ai-integration → notion-operations
```

### Link Collection & Analysis
```
Webhook Trigger → notion-link-analysis →
Notion Database
```

### AI Content Generation
```
Schedule Trigger → idea-generation →
Batch Accumulator → AI Clustering →
notion-operations
```

## Key Configuration Files

### n8n-workflow-agent
- `config/.env` - Main configuration (N8N_BASE_URL, N8N_API_KEY, AI keys)
- `requirements.txt` - Python dependencies
- `docs/ANALYSIS_*.md` - Workflow creation guides

### n8n-skills
- Each skill's `README.md` - Individual skill documentation
- `n8n-best-practices/README.md` - Essential n8n patterns
- `SKILLS_RETRIEVAL_GUIDE.md` - How to find and use skills

## Testing

### Python Agent Testing
```bash
# Test n8n connection
python tools/n8n_workflow_manager.py test

# Validate workflow JSON
python -m json.tool workflow_config.json

# Run analyzer diagnostics
python tools/workflow_analyzer.py workflow.json --verbose

# Run test suite
python tools/test_runner.py test_scenarios.json
```

### Skills Testing
All skills must be tested directly in n8n:
1. Copy skill code to n8n Code node
2. Configure environment variables
3. Execute workflow
4. Verify output matches documentation

## Troubleshooting

### Python Agent Issues
- **Connection Failed**: Verify `N8N_BASE_URL` and `N8N_API_KEY` in `config/.env`
- **Workflow Creation Failed**: Check node configuration and connection mappings
- **Test Timeout**: Increase `TEST_TIMEOUT` environment variable
- **Import Failed**: Validate JSON structure against workflow schema

### n8n Skills Issues
- **Code node errors**: Read `n8n-best-practices/README.md` first
- **HTTP requests fail**: Use `require('https')`, not `$http` or `axios`
- **Syntax errors**: Ensure ES5 compatibility (no arrow functions/template literals)
- **undefined variables**: Use `$env.VAR_NAME` for environment variables
- **gzip errors**: Don't send `Accept-Encoding` header

## Dependencies

### n8n-workflow-agent
```
Python 3.8+
requests, aiohttp, python-dotenv, pyyaml, click
networkx, matplotlib, numpy
pytest, pytest-asyncio, pytest-cov
pandas, jsonschema, jinja2
```

### n8n-skills
```
n8n instance with:
- NODE_FUNCTION_ALLOW_BUILTIN=* (for require() access)
- API access enabled
- Environment variables configured

External tools (varies by skill):
- yt-dlp, ffmpeg (video-processing)
- playwright (anti-scraping)
```

## Important Notes

1. **Monorepo Structure**: This repository contains two related but independent projects
2. **Claude Code Skills**: 7 skills are integrated - Claude will auto-invoke when relevant
3. **Read Documentation First**: Both projects have extensive documentation - always read before coding
4. **Skills Library is Gold**: The n8n-skills library contains battle-tested solutions - use it
5. **Analysis is Mandatory**: n8n-workflow-agent requires sequential analysis phase for workflow creation
6. **ES5 Only**: n8n Code nodes only support ES5 JavaScript syntax
7. **No Direct Sharing**: n8n workflows cannot be shared directly (credential IDs), hence this architecture

## Claude Code Skills Reference

All skills located in `.claude/skills/`:

1. **n8n-best-practices** - Critical n8n patterns, must-read for any n8n work
2. **n8n-skills-catalog** - Master index of all skills with quick finder
3. **anti-scraping** - Web scraping with Cloudflare bypass using Playwright
4. **ai-integration** - LLM integration (OpenAI, Qwen, Claude) with structured parsing
5. **notion-operations** - Complete Notion CRUD, all field types, sync patterns
6. **oauth-automation** - OAuth token auto-refresh for YouTube/Google APIs
7. **video-processing** - YouTube subtitle extraction, VTT parsing, video analysis

Each skill includes:
- Quick reference for common patterns
- Code examples (ES5 compatible)
- Troubleshooting guides
- Integration patterns with other skills
- Links to full documentation in n8n-skills/

**Pro Tip**: When starting any n8n task, Claude will automatically check relevant skills for proven solutions.
