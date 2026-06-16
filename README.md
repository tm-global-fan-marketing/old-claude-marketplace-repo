# marketing-central Claude Plugin

Marketing skills and tools for Live Nation's central marketing org.

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
claude plugin marketplace add https://your-org.github.io/claude-plugin-marketing-central
claude plugin install marketing-central@marketing-central
```

### Confluence Authentication

When you first use a skill that searches Confluence, Claude may prompt for a Confluence API token. To set this up:

1. Generate a Confluence API token at https://id.atlassian.com/manage-profile/security/api-tokens
2. When Claude prompts for credentials, provide your email and API token

If you cannot access Confluence or receive an authentication error, contact marketing-tech@livenation.com.

---

## For Admins

### One-Time Setup

1. Ensure the `manifest.json` is live at `https://your-org.github.io/claude-plugin-marketing-central/manifest.json`
2. In the claude.ai admin console, add the GitHub Pages URL as a known marketplace
3. Enable the `marketing-central` plugin for all users
4. Staff will see the plugin under **Customize → Plugins → Your organisation**

### GitHub Pages Configuration

In the repo settings:
- Go to **Settings → Pages**
- Set source to the `main` branch, `/docs` folder
- Click **Save** — GitHub Pages will publish within ~1 minute

Verify it is working:
```bash
curl https://your-org.github.io/claude-plugin-marketing-central/manifest.json
```

### Adding New Skills

1. Create `skills/[skill-name]/SKILL.md`
2. Add a trigger row to `CLAUDE.md`
3. Update `version` in `docs/manifest.json` and `.claude-plugin/plugin.json`
4. Commit and push — staff pick up the update automatically

---

## Support

Contact the marketing technology team at marketing-tech@livenation.com.
