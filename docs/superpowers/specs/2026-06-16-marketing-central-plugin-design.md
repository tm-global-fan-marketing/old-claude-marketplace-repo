# marketing-central Plugin Design

**Date:** 2026-06-16
**Status:** Draft

---

## Overview

A Superpowers-style Claude plugin for Live Nation's central marketing organisation, serving both B2C and B2B teams. The plugin packages marketing-specific skills and the LN Confluence connector into a single installable unit that works in Claude Desktop (all surfaces) and Claude Code.

---

## Goals

- Give internal marketing staff access to AI-assisted workflows without manual configuration
- Provide a consistent, branded experience for copywriting, translation, campaign planning, and more
- Start with 2–3 skills and scale to 8–9 within 2 months
- Require no authentication or login to install

---

## Out of Scope (Initial Release)

- Sub-agents (noted as a future capability — pattern is `skills/[skill]/agents/[agent].md`)
- Additional MCP connectors beyond LN Confluence
- External user access (internal staff only)

---

## Architecture

### Repository Structure

```
claude-plugin-marketing-central/
├── .claude-plugin/
│   └── plugin.json          ← plugin identity (name, description, author)
├── .mcp.json                ← registers LN Confluence MCP on install
├── skills/
│   ├── copywriting/
│   │   └── SKILL.md
│   ├── translation/
│   │   └── SKILL.md
│   └── campaign-planning/
│       └── SKILL.md
├── docs/
│   └── superpowers/
│       └── specs/           ← this file lives here
├── CLAUDE.md                ← skill trigger table + invocation rules
└── README.md                ← install instructions for staff
```

### Plugin Identity

`.claude-plugin/plugin.json`:

```json
{
  "name": "marketing-central",
  "description": "Marketing skills and tools for Live Nation's central marketing org — copywriting, translation, campaign planning, and more.",
  "author": {
    "name": "Live Nation Marketing",
    "email": "marketing-tech@livenation.com"
  }
}
```

### LN Confluence Connector

`.mcp.json` registers the LN Confluence MCP automatically on plugin install. No manual configuration required for staff.

```json
{
  "mcpServers": {
    "ln-confluence": {
      "url": "https://confluence.livenation.com/mcp"
    }
  }
}
```

Skills can use the `ln-confluence` MCP tools to read brand guidelines, search existing content, and publish outputs back to Confluence.

---

## Skills

### Initial Skills (v1)

| Skill | Trigger | Purpose |
|---|---|---|
| `marketing-central:copywriting` | User asks to write or edit marketing copy | B2C and B2B copy with brand voice |
| `marketing-central:translation` | User asks to translate content | Localisation with marketing-appropriate tone |
| `marketing-central:campaign-planning` | User asks to plan a campaign | Structured campaign planning using Confluence context |

Each skill is a `SKILL.md` file inside its own subdirectory under `skills/`. The file defines the skill's purpose, instructions, constraints, and output format for Claude to follow.

### Scaling to 8–9 Skills

Each new skill requires:
1. A new `skills/[skill-name]/SKILL.md` file
2. A new row in the `CLAUDE.md` trigger table

No structural changes to the repo are needed.

### Planned Future Skills (not yet specced)

- Report creation
- Content calendar
- Brief writing
- Social media
- Audience research

---

## CLAUDE.md — Skill Auto-Invocation

The `CLAUDE.md` in the repo root defines a trigger table so Claude invokes the correct skill automatically based on user intent, without requiring staff to type slash commands.

```markdown
| Skill                                  | Triggers When                                  |
|----------------------------------------|------------------------------------------------|
| `marketing-central:copywriting`        | User asks to write, edit, or review copy       |
| `marketing-central:translation`        | User asks to translate or localise content     |
| `marketing-central:campaign-planning`  | User asks to plan, brief, or structure a campaign |
```

The file also includes guidance on when to proactively use the LN Confluence connector (e.g. check brand guidelines before writing copy, search for existing campaigns before planning a new one).

---

## Distribution

### Approach: Enterprise Admin Console + GitHub Pages Marketplace

The plugin lives in a private GitHub repo. A `manifest.json` is published via GitHub Pages (public URL, no authentication required). An Enterprise admin registers this marketplace once in the claude.ai admin console and pushes the plugin to all staff — it appears under **Customize → Plugins → Your organisation** automatically. Staff do nothing.

The GitHub Pages marketplace is still needed as the plugin source, but staff never need to run any CLI commands.

**Why this approach:**
- Zero friction for staff — plugin appears automatically
- Managed centrally by one admin, not per-user
- No login or token required for the install source
- Plugin updates are picked up automatically
- Skills and connector changes roll out to all staff on next sync

### GitHub Pages Setup

The repo's `gh-pages` branch (or `/docs` folder) serves a `manifest.json` that describes the plugin and its source.

`manifest.json` (served at `https://your-org.github.io/claude-plugin-marketing-central/manifest.json`):

```json
{
  "name": "marketing-central-marketplace",
  "description": "Live Nation Marketing Central plugin marketplace",
  "plugins": [
    {
      "name": "marketing-central",
      "description": "Marketing skills and tools for Live Nation's central marketing org.",
      "version": "1.0.0",
      "source": "https://github.com/your-org/claude-plugin-marketing-central"
    }
  ]
}
```

### Enterprise Admin Setup (one-time)

1. Admin opens the claude.ai admin console
2. Adds the GitHub Pages URL as a known marketplace
3. Enables the `marketing-central` plugin for all users
4. Plugin appears under **Customize → Plugins → Your organisation** for all staff

### Self-Install (for early testers before org-wide rollout)

Developers and testers can install before the admin pushes it org-wide:

```bash
claude plugin marketplace add https://your-org.github.io/claude-plugin-marketing-central
claude plugin install marketing-central@marketing-central
```

---

## Testing & Rollout

- Install the plugin in a test Claude Desktop session and verify skills trigger correctly from natural language
- Verify LN Confluence MCP connects and tools are available
- Share install instructions via internal wiki
- Gather feedback from B2C and B2B teams and use it to prioritise the next skill additions

---

## Future Considerations

- **Sub-agents:** Campaign planning and report creation are good candidates for sub-agents that can search Confluence and produce structured outputs in parallel. Pattern: `skills/[skill]/agents/[agent].md`.
- **Additional connectors:** Add to `.mcp.json` as new tools become available (e.g. DAM, analytics, translation APIs).
- **Separate B2B/B2C skill variants:** If brand voice diverges significantly, skills can fork into `copywriting-b2b` and `copywriting-b2c` without changing the repo structure.
