---
name: skill-creator
description: Guide for creating effective skills that extend Claude's capabilities with specialized knowledge, workflows, or tool integrations. Use when users need to create, structure, or package new skills for the RuleSync skill system.
---

# Skill Creator

This skill guides users in creating effective skills that extend Claude's capabilities with specialized knowledge, workflows, or tool integrations.

## Overview

Skills are modular, self-contained packages that add capabilities to Claude. They follow a specific structure with metadata, documentation, and optional bundled resources.

## Key Principles

**Context Window as Public Good**: Skills add information to Claude's context window. Only include information Claude doesn't already have. Match specificity to task fragility:
- High freedom (text-based guidance) for flexible tasks
- Low freedom (specific scripts/tools) for fragile operations

**Progressive Disclosure**: Structure skills to load information progressively:
- Metadata (name/description) - always in context
- Body (SKILL.md content) - loaded when skill is triggered
- References - loaded as needed via `Read`

## Anatomy of a Skill

Every skill requires:
- **SKILL.md**: Core documentation with YAML frontmatter (name + description) and Markdown body

Optional bundled resources:
- **scripts/**: Executable code (Python, Bash, etc.)
- **references/**: Documentation loaded into context as needed
- **assets/**: Files used in output (templates, fonts, images)

## Creation Process

### 1. Understand the Skill

Start with concrete examples:
- What specific user requests would trigger this skill?
- What would the ideal response look like?
- What knowledge or tools are needed?

### 2. Plan Reusable Contents

Identify what should be bundled:
- **Scripts**: Executable utilities (use Python for portability)
- **References**: Documentation too detailed for SKILL.md
- **Assets**: Files users need in output

### 3. Initialize the Skill

Use the init_skill.py script to create the structure:

```bash
python .rulesync/skills/skill-creator/scripts/init_skill.py <skill-name> --path <path>
```

### 4. Edit SKILL.md

Complete the TODO items and customize the structure. Keep SKILL.md under 500 lines.

### 5. Package the Skill

Create a distributable .skill file:

```bash
python .rulesync/skills/skill-creator/scripts/package_skill.py <path/to/skill>
```

### 6. Iterate

Test with real usage and refine based on what works.

## Reference Patterns

See references/ directory for detailed patterns:
- `output-patterns.md`: Templates and examples for consistent output
- `workflows.md`: Sequential and conditional workflow patterns

## Scripts

- **init_skill.py**: Creates a new skill directory with template files
- **package_skill.py**: Packages a skill into a distributable .skill file
- **quick_validate.py**: Validates skill structure before packaging
