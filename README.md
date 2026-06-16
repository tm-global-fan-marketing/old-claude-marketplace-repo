# tm-marketing-core Claude Plugin

Marketing skills and tools for Ticketmaster's central marketing org.

## What This Plugin Provides

**Skills:**
- `copywriting` — Write and edit B2C and B2B marketing copy with brand voice
- `translation` — Translate and localise marketing content (including regional/market adaptations)
- `campaign-planning` — Plan structured marketing campaigns using Confluence context

**Connector:**
- LN Confluence — Automatically connected on install. Skills use it for brand guidelines, existing campaigns, and publishing outputs.

Skills trigger automatically from natural language — no slash commands needed.

---

## For Staff

The plugin is managed centrally and should already appear under **Customize → Plugins → Your organisation** in Claude Desktop. No action needed.

If it is not appearing, contact your admin or follow the manual install steps below.

### Manual Install (testers / early access)

```bash
claude plugin marketplace add git@git.tmaws.io:andrew.wragg/claude-plugin-tm-marketing-core.git
claude plugin install tm-marketing-core@tm-marketing-core-marketplace
```

### Confluence Authentication

When you first use a skill that searches Confluence, Claude may prompt for a Confluence API token. To set this up:

1. Generate a Confluence API token at https://id.atlassian.com/manage-profile/security/api-tokens
2. When Claude prompts for credentials, provide your email and API token

If you cannot access Confluence or receive an authentication error, contact marketing-tech@ticketmaster.com.

---

## For Admins

### Enterprise Admin Setup (one-time)

1. In the claude.ai admin console, add the marketplace URL:
   `git@git.tmaws.io:andrew.wragg/claude-plugin-tm-marketing-core.git`
2. Enable the `tm-marketing-core` plugin for all users
3. Staff will see the plugin under **Customize → Plugins → Your organisation**

### Adding New Skills

1. Create `skills/[skill-name]/SKILL.md`
2. Add a trigger row to `CLAUDE.md`
3. Bump `version` in `.claude/plugin.json` and `.claude-plugin/marketplace.json`
4. Commit and push — staff pick up the update automatically

---

## Support

Contact the marketing technology team at marketing-tech@ticketmaster.com.
