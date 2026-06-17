# TM Marketing Claude Code Marketplace

**Marketplace Name**: `tm-marketing-marketplace`
**Repository**: `https://git.tmaws.io/andrew.wragg/claude-plugin-marketing-central`

Ticketmaster Marketing's shared catalog of Claude Code plugins for B2C and B2B marketing teams.

## Quick Start

```bash
# Add the marketplace (one-time setup)
claude plugin marketplace add git@git.tmaws.io:andrew.wragg/claude-plugin-marketing-central.git

# Install plugins
claude plugin install tm-marketing-core@tm-marketing-marketplace

# Verify installation
claude plugin list

# Update plugins
claude plugin update
```

## Available Plugins

### Central Marketing Team

| Plugin | Version | Skills | Who It's For |
|--------|---------|--------|-------------|
| `tm-marketing-core` | 1.0.0 | copywriting, translation, campaign-planning | B2C and B2B marketing teams |

### Registered Team Prefixes

| Team | Prefix | Directory |
|------|--------|-----------|
| Central Marketing | `tm-marketing` | `plugins/tm-marketing/` |

## Repository Structure

```
claude-plugin-marketing-central/
├── .claude-plugin/marketplace.json     # Marketplace manifest (all plugins)
├── .gitlab/
│   ├── CODEOWNERS                      # Automatic reviewer assignment
│   └── merge_request_templates/        # MR templates (new-plugin, new-skill)
├── plugins/
│   └── tm-marketing/
│       └── tm-marketing-core/          # Central marketing plugin
│           ├── .claude/plugin.json     # Plugin identity
│           ├── .mcp.json               # LN Confluence MCP connector
│           ├── CLAUDE.md               # Skill triggers
│           └── skills/
│               ├── copywriting/SKILL.md
│               ├── translation/SKILL.md
│               └── campaign-planning/SKILL.md
├── docs/                               # Specs, plans, architecture docs
├── CLAUDE.md                           # Contributor guidelines
└── README.md
```

## Confluence Authentication

When you first use a skill that searches Confluence, Claude may prompt for a Confluence API token:

1. Generate a token at https://id.atlassian.com/manage-profile/security/api-tokens
2. Provide your email and API token when prompted

Contact marketing-tech@ticketmaster.com for support.

## Contributing

See [CLAUDE.md](CLAUDE.md) for contributor guidelines, versioning rules, and how to add new plugins and skills. Use the MR templates in `.gitlab/merge_request_templates/` when raising changes.
