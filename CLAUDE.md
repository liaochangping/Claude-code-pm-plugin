# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Claude Code PM Plugin** - a plain-text, markdown-based plugin that provides Product Management agents and commands for Claude Code. It requires no build step, runtime, or SDK - just pure markdown files that Claude reads and executes.

### Plugin Architecture

```
.claude-plugin/
├── marketplace.json          # Plugin manifest for Claude Code marketplace
├── agents/                   # PM agent specifications (Markdown)
│   ├── pm_discovery.agent.md
│   ├── pm_prd.agent.md
│   ├── pm_review.agent.md
│   ├── pm_priority.agent.md
│   └── pm_tech_bridge.agent.md
└── commands/                 # CLI command definitions (Markdown)
    ├── discover.md
    ├── prd.md
    ├── review.md
    ├── roadmap.md
    └── backlog.md
```

**Key Design Principle**: All agents and commands are plain markdown files. When users invoke a command or agent, Claude reads the corresponding markdown file and follows the instructions within it.

## Marketplace Configuration

The plugin is published to Claude Code's marketplace via `.claude-plugin/marketplace.json`:

- **name**: `claude-code-pm-plugin`
- **source**: Points to `./` (plugin root)
- **homepage**: https://github.com/liaochangping/Claude-code-pm-plugin
- **repository**: https://github.com/liaochangping/Claude-code-pm-plugin
- **license**: MIT
- **category**: workflow
- **keywords**: pm, product-management, prd, backlog, agile, agents, commands, project-discovery, review

**Important**: When updating marketplace.json, ensure:
1. `owner` field matches GitHub username
2. `plugins[0].source` is `"./"` (relative to marketplace.json)
3. All metadata fields are present
4. Version changes require git commits

## Agent System

Agents are specialized PM personas invoked via the Task tool. Each agent is defined in a markdown file with:

### Available Agents

1. **pm_discovery** (`agents/pm_discovery.agent.md`)
   - Purpose: Requirement discovery and validation
   - Persona: Senior, restrained, rational PM
   - Key behaviors: Separates problem from solution, challenges fake requirements, exposes hidden assumptions
   - Language: Chinese (designed for Chinese-speaking PMs)

2. **pm_prd** (`agents/pm_prd.agent.md`)
   - Purpose: Engineering-ready PRD generation
   - Persona: PM who collaborates with engineering teams
   - Key behaviors: Implementation-focused, explicit boundaries, edge cases, acceptance criteria
   - Language: Chinese

3. **pm_review** (`agents/pm_review.agent.md`)
   - Purpose: Ruthless PRD/solution review
   - Persona: Demanding tech lead
   - Key behaviors: Finds ambiguities, missing edge cases, high-risk assumptions
   - Language: Chinese

4. **pm_priority** (`agents/pm_priority.agent.md`)
   - Purpose: Priority & roadmap planning
   - Persona: Resource-sensitive product owner
   - Methods: RICE scoring, MoSCoW prioritization
   - Language: Chinese

5. **pm_tech_bridge** (`agents/pm_tech_bridge.agent.md`)
   - Purpose: PM ↔ Engineering translation
   - Persona: Translator between PM and engineering mindsets
   - Key behaviors: Bridges language gaps, reveals implicit information, facilitates consensus
   - Language: Chinese

### Invoking Agents

Use the Task tool with `subagent_type`:
```bash
# Launch discovery agent
Task("subagent_type": "claude-code-pm-plugin:pm_discovery.agent", ...)

# Launch PRD agent
Task("subagent_type": "claude-code-pm-plugin:pm_prd.agent", ...)
```

**Note**: All agent content is in Chinese. When using these agents, expect Chinese output.

## Command System

Commands are user-invocable slash commands that load corresponding markdown instruction files.

### Available Commands

1. **/discover** (`commands/discover.md`)
   - Triggers: pm_discovery agent behavior
   - Input: Requirement description
   - Output: Clarified requirements, identified assumptions, validation needs

2. **/prd** (`commands/prd.md`)
   - Triggers: PRD generation based on pm_prd.agent.md
   - Input: Clear requirements, background, target users
   - Output: Engineering-ready PRD with 8 sections (background, users, scope, flows, interactions, data/tracking, acceptance criteria, risks)

3. **/review-prd** (`commands/review.md`)
   - Triggers: PRD review based on pm_review.agent.md
   - Input: PRD content
   - Output: Critical review with severity ratings, clarifications needed, risks, optimization suggestions

4. **/roadmap** (`commands/roadmap.md`)
   - Triggers: Priority planning based on pm_priority.agent.md
   - Input: List of requirements, constraints (time, resources, goals)
   - Output: Prioritized requirements, MVP phasing, roadmap visualization, "not doing" list

5. **/backlog** (`commands/backlog.md`)
   - Triggers: Backlog decomposition
   - Input: PRD content or requirement list
   - Output: Epic → Story → Task hierarchy with estimates and dependencies

### Command Invocation Pattern

Commands are invoked by users in Claude Code. Each command file follows this structure:

```markdown
你现在调用的是【Command Name】命令。

请基于下面输入，[command-specific instructions].

## 工作模式
[Mode description]

## 输出格式
[Output structure]

## 输入格式
[Expected input format]
```

## Recommended Workflow

The plugin follows this sequential PM workflow:

```
/discover    →  Clarify requirements, challenge assumptions
     ↓
/prd         →  Generate engineering-ready PRD
     ↓
/review-prd  →  Ruthless technical review
     ↓
/roadmap     →  Prioritize and plan phases
     ↓
/backlog     →  Decompose into executable tasks
     ↓
Engineering execution
```

## Development Workflow

### Adding a New Agent

1. Create new markdown file in `agents/` with naming: `[name]_agent.md`
2. Define agent persona, rules, output structure
3. Add agent reference to this CLAUDE.md under "Available Agents"
4. Test via Task tool invocation

### Adding a New Command

1. Create new markdown file in `commands/` with naming: `[command].md`
2. Follow command structure (mode, output format, input format)
3. Add command reference to this CLAUDE.md under "Available Commands"
4. Update README.md if it's a user-facing command
5. Test via `/command-name` invocation

### Updating marketplace.json

1. Edit `.claude-plugin/marketplace.json`
2. Ensure JSON is valid
3. Increment version if needed
4. Commit changes

### Localization

**Current State**: All agents and commands are in Chinese. This is intentional - the plugin targets Chinese-speaking technical PMs.

**Adding English Support**: To add English versions:
1. Create parallel agent files (e.g., `pm_discovery_en.agent.md`)
2. Create parallel command files (e.g., `discover_en.md`)
3. Update marketplace.json keywords to include both languages

## File Organization Principles

- **Plain text only**: No build process, no dependencies
- **Markdown-first**: All logic and instructions in markdown
- **200-400 lines per agent**: Focused, single-purpose agents
- **High cohesion, low coupling**: Each agent/command is independent
- **Chinese language**: Designed for Chinese PM workflows

## Common Operations

### Testing Agent Changes

After modifying an agent file:
1. Use Claude Code to invoke the agent via Task tool
2. Verify agent follows updated instructions
3. Check output format matches expected structure
4. No build/test commands needed - just reload the agent

### Testing Command Changes

After modifying a command file:
1. Use Claude Code to invoke the command (e.g., `/discover`)
2. Verify command loads and follows instructions
3. Check prompt and output format
4. No build/test commands needed

### Publishing Plugin Updates

1. Commit changes to git
2. Push to GitHub repository
3. Claude Code marketplace reads from `repository` URL in marketplace.json
4. No manual publishing step needed

## Important Constraints

- **No runtime**: This is not a Node.js/Python/etc. plugin
- **No SDK**: Does not use Claude Code SDK
- **No build**: Pure markdown, no compilation
- **No dependencies**: Zero npm/pip/cargo dependencies
- **Agent language**: All agents output in Chinese
- **Command language**: All command prompts in Chinese

## Troubleshooting

### Agent not found
- Verify agent file exists in `agents/`
- Check subagent_type matches filename pattern: `claude-code-pm-plugin:pm_[name].agent`

### Command not working
- Verify command file exists in `commands/`
- Check command file has valid markdown structure
- Ensure command is referenced in marketplace.json if user-facing

### Marketplace not updating
- Verify marketplace.json has valid JSON syntax
- Check `repository` URL is correct and public
- Ensure git commit has been pushed to GitHub

## Philosophy

> A good PM plugin should help you:
> - Ask harder questions
> - Write less bullshit
> - Ship fewer but better things

This plugin is **opinionated by design** - it challenges vague requirements, demands technical rigor, and forces explicit trade-offs. It is designed for technical PMs, indie hackers, and engineering-led teams who value clarity over politeness.
