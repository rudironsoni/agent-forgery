# File Formats

## `rulesync/rules/*.md`

Example:

```md
---
root: true # true that is less than or equal to one file for overview such as `AGENTS.md`, false for details such as `.agents/memories/*.md`
localRoot: false # (optional, default: false) true for project-specific local rules. Claude Code: generates CLAUDE.local.md; Others: appends to root file
targets: ["*"] # * = all, or specific tools
description: "Rulesync project overview and development guidelines for unified AI rules management CLI tool"
globs: ["**/*"] # file patterns to match (e.g., ["*.md", "*.txt"])
agentsmd: # agentsmd and codexcli specific parameters
  # Support for using nested AGENTS.md files for subprojects in a large monorepo.
  # This option is available only if root is false.
  # If subprojectPath is provided, the file is located in `${subprojectPath}/AGENTS.md`.
  # If subprojectPath is not provided and root is false, the file is located in `.agents/memories/*.md`.
  subprojectPath: "path/to/subproject"
cursor: # cursor specific parameters
  alwaysApply: true
  description: "Rulesync project overview and development guidelines for unified AI rules management CLI tool"
  globs: ["*"]
antigravity: # antigravity specific parameters
  trigger: "always_on" # always_on, glob, manual, or model_decision
  globs: ["**/*"] # (optional) file patterns to match when trigger is "glob"
  description: "When to apply this rule" # (optional) used with "model_decision" trigger
---

# Rulesync Project Overview

...
```

## `.rulesync/hooks.json`

Lifecycle hooks for various events.

```json
{
  "$schema": "https://github.com/dyoshikawa/rulesync/releases/latest/download/hooks-schema.json",
  "hooks": {
    "sessionStart": [
      {
        "command": "echo",
        "args": ["Session started!"]
      }
    ],
    "preToolUse": [
      {
        "command": "node",
        "args": ["scripts/pre-tool.js"]
      }
    ],
    "postToolUse": [
      {
        "command": "echo",
        "args": ["Tool used!"]
      }
    ]
  }
}
```

Supported hooks:
- `sessionStart` - Triggered when a new session starts
- `preToolUse` - Triggered before a tool is used
- `postToolUse` - Triggered after a tool is used

## `rulesync/commands/*.md`

Command definitions with descriptions and tool-specific settings.

```md
---
name: my-command
description: "Description of what this command does"
---

# my-command

Detailed documentation for this command...
```

## `rulesync/subagents/*.md`

Subagent configurations.

```md
---
name: my-subagent
description: "Description of this subagent's purpose"
model: claude-3-opus-4-6
tools: ["Read", "Write", "Edit"]
---

# my-subagent

Instructions for this subagent...
```

## `.rulesync/skills/*/SKILL.md`

Skill definitions with allowed tools and model settings.

```md
---
name: my-skill
description: "What this skill does"
allowed-tools: ["Read", "Write"]
model: claude-3-opus-4-6
---

# my-skill

Skill documentation...
```

## `.rulesync/mcp.json`

MCP server configurations.

```json
{
  "$schema": "https://github.com/dyoshikawa/rulesync/releases/latest/download/mcp-schema.json",
  "mcpServers": {
    "my-server": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem"],
      "env": {}
    }
  }
}
```

## `.rulesync/.aiignore`

Ignore patterns for rulesync.

```
# Comments are supported
node_modules/
*.log
dist/
```

This file uses standard gitignore patterns.
