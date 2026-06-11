# Teradata Trial Data Loading — Agent Skill

An [Agent Skill](https://docs.claude.com/en/docs/agents-and-tools/agent-skills) that guides
an AI agent through discovering and loading demo/sample datasets into a **Teradata Trial**
(formerly **ClearScape Analytics Experience**) environment using the `demo_user.get_data()`
stored procedure.

The skill works with any MCP server that can execute SQL against Teradata.

## What's in this repo

This skill is provided in two equivalent formats:

| Path | Format | Use it with |
|------|--------|-------------|
| [`teradata-trial-data-loading/`](teradata-trial-data-loading/) | Unpacked folder (generic Agent Skill) | Claude Code, the Claude Agent SDK, or any tool that reads the open Agent Skills format |
| [`teradata-trial-data-loading.skill`](teradata-trial-data-loading.skill) | Packaged `.skill` (ZIP) | Claude Desktop / claude.ai — upload directly in the Skills UI |

Both contain the same content:

```
teradata-trial-data-loading/
├── SKILL.md                          # skill instructions + frontmatter
└── references/
    ├── dataset-catalog.md            # full categorized catalog of ~180 datasets
    └── prompt-runbook.md             # ready-to-paste prompts and domain variants
```

## Installing the generic skill (Claude Code)

Copy the unpacked folder into your skills directory:

```bash
# Project-level
cp -r teradata-trial-data-loading .claude/skills/

# or user-level (available across all projects)
cp -r teradata-trial-data-loading ~/.claude/skills/
```

## Installing the Claude Desktop skill

In Claude Desktop or claude.ai, open **Settings → Capabilities → Skills** and upload
`teradata-trial-data-loading.skill`.

## Keeping the two formats in sync

The `.skill` file is just a ZIP of the unpacked folder. If you edit the folder, repackage it:

```bash
rm -f teradata-trial-data-loading.skill
( cd . && zip -r teradata-trial-data-loading.skill teradata-trial-data-loading -x '*.DS_Store' )
```

## Requirements

- A Teradata Trial / ClearScape Analytics Experience environment
  (get one free at [teradata.com/getting-started](https://www.teradata.com/getting-started))
- An MCP server connected that can execute SQL against Teradata
  (e.g. `tdsql-dev`, `teradata-ce`, or any Teradata SQL-execution MCP)
