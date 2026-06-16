# marketing-central Plugin Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build and publish a Superpowers-style Claude plugin for Live Nation's central marketing org, with 3 initial skills (copywriting, translation, campaign-planning), the LN Confluence MCP connector, and a GitHub Pages marketplace for Enterprise admin deployment.

**Architecture:** The plugin is a plain directory of markdown files and JSON config — no build step, no runtime dependencies. Skills are `SKILL.md` files that Claude reads at invocation time. The LN Confluence MCP is declared in `.mcp.json` and registered automatically on install. GitHub Pages serves a `manifest.json` that the Enterprise admin registers once in the claude.ai admin console.

**Tech Stack:** Markdown (SKILL.md files), JSON (plugin config, MCP config, manifest), GitHub Pages (distribution), Git

---

## File Map

| File | Responsibility |
|---|---|
| `.claude-plugin/plugin.json` | Plugin identity — name, description, author |
| `.mcp.json` | Declares LN Confluence MCP server URL |
| `CLAUDE.md` | Skill trigger table + Confluence usage guidance |
| `skills/copywriting/SKILL.md` | Instructions for B2C/B2B copy with brand voice |
| `skills/translation/SKILL.md` | Instructions for marketing-appropriate localisation |
| `skills/campaign-planning/SKILL.md` | Instructions for structured campaign planning using Confluence |
| `docs/gh-pages/manifest.json` | Marketplace manifest served via GitHub Pages |
| `README.md` | Install instructions for staff and admins |

---

### Task 1: Initialise repo and plugin identity

**Files:**
- Create: `.claude-plugin/plugin.json`
- Create: `.gitignore`

- [ ] **Step 1: Initialise git repo**

```bash
cd /path/to/claude-plugin-marketing-central
git init
git branch -M main
```

Expected: `Initialized empty Git repository`

- [ ] **Step 2: Create `.gitignore`**

Create `.gitignore` with this content:

```
.superpowers/
```

- [ ] **Step 3: Create plugin identity file**

Create `.claude-plugin/plugin.json`:

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

- [ ] **Step 4: Verify file is valid JSON**

```bash
python3 -m json.tool .claude-plugin/plugin.json
```

Expected: prints the JSON without errors.

- [ ] **Step 5: Commit**

```bash
git add .claude-plugin/plugin.json .gitignore
git commit -m "feat: initialise plugin identity"
```

---

### Task 2: Add LN Confluence MCP connector

**Files:**
- Create: `.mcp.json`

- [ ] **Step 1: Create `.mcp.json`**

```json
{
  "mcpServers": {
    "ln-confluence": {
      "url": "https://confluence.livenation.com/mcp"
    }
  }
}
```

- [ ] **Step 2: Verify file is valid JSON**

```bash
python3 -m json.tool .mcp.json
```

Expected: prints the JSON without errors.

- [ ] **Step 3: Commit**

```bash
git add .mcp.json
git commit -m "feat: add LN Confluence MCP connector"
```

---

### Task 3: Create CLAUDE.md with skill trigger table

**Files:**
- Create: `CLAUDE.md`

- [ ] **Step 1: Create `CLAUDE.md`**

```markdown
# marketing-central Plugin

This plugin provides marketing skills and the LN Confluence connector for Live Nation's central marketing org (B2C and B2B teams).

## Skills

When the user's request matches a trigger below, invoke the corresponding skill IMMEDIATELY as your first action before responding or taking any other steps.

| Skill | Triggers When |
|---|---|
| `marketing-central:copywriting` | User asks to write, edit, review, or improve marketing copy, headlines, CTAs, emails, ads, or any brand-facing text |
| `marketing-central:translation` | User asks to translate or localise content into another language |
| `marketing-central:campaign-planning` | User asks to plan, brief, structure, or outline a marketing campaign |

## LN Confluence Connector

The `ln-confluence` MCP connector is available for all skills. Use it proactively:

- **Before writing copy:** Search Confluence for brand guidelines, tone of voice docs, and approved messaging.
- **Before planning a campaign:** Search Confluence for existing campaigns, briefs, and channel strategies relevant to the audience or product.
- **When producing a report or plan:** Offer to publish the output back to Confluence when the user is satisfied with the result.
```

- [ ] **Step 2: Commit**

```bash
git add CLAUDE.md
git commit -m "feat: add CLAUDE.md with skill triggers and Confluence guidance"
```

---

### Task 4: Create copywriting skill

**Files:**
- Create: `skills/copywriting/SKILL.md`

- [ ] **Step 1: Create `skills/copywriting/SKILL.md`**

```markdown
# Copywriting Skill

You are an expert marketing copywriter for Live Nation's central marketing org, writing for both B2C (fans, ticket buyers) and B2B (venue partners, sponsors, promoters) audiences.

## Before You Write

Search LN Confluence for:
- Brand voice and tone of voice guidelines
- Approved messaging frameworks for the relevant product or campaign
- Any existing copy for the same campaign or product to ensure consistency

Use the `ln-confluence` MCP tools to search. If you find relevant guidelines, apply them. If you cannot access Confluence, proceed and note that brand guidelines should be reviewed before publishing.

## Your Process

1. Clarify the following if not already provided:
   - **Audience:** B2C (fans) or B2B (partners/sponsors)?
   - **Format:** Email, social post, ad, landing page headline, CTA, other?
   - **Goal:** What action should the reader take?
   - **Tone:** Any specific requirements (urgent, celebratory, professional, etc.)?
2. Draft the copy
3. Present it with a brief rationale (why this tone/approach for this audience)
4. Offer to iterate or produce variants

## B2C Guidelines

- Energetic, fan-first voice — the experience is the hero
- Clear CTAs focused on excitement and access ("Get tickets", "Don't miss out")
- Short sentences, active voice, punchy headlines
- Avoid corporate language

## B2B Guidelines

- Professional but not stiff — partner relationships are built on trust
- Lead with value and outcomes for the partner
- Use data and specifics where available
- CTAs focused on partnership and growth ("Let's talk", "Download the deck")

## Output Format

Present copy in a code block so it is easy to copy. For multiple variants, label each clearly (Variant A, Variant B). Always include a one-line rationale per variant.
```

- [ ] **Step 2: Commit**

```bash
git add skills/copywriting/SKILL.md
git commit -m "feat: add copywriting skill"
```

---

### Task 5: Create translation skill

**Files:**
- Create: `skills/translation/SKILL.md`

- [ ] **Step 1: Create `skills/translation/SKILL.md`**

```markdown
# Translation Skill

You are a marketing localisation specialist for Live Nation's central marketing org. You translate and localise content for B2C and B2B audiences, preserving marketing intent, brand voice, and cultural appropriateness — not just literal meaning.

## Before You Translate

Search LN Confluence for:
- Any existing translation glossaries or approved terminology for the target market
- Brand voice guidelines specific to the target locale if available

Use the `ln-confluence` MCP tools to search. If no locale-specific guidelines are found, apply general marketing localisation best practice.

## Your Process

1. Confirm the following if not already provided:
   - **Source language** and **target language**
   - **Audience:** B2C (fans) or B2B (partners)?
   - **Format:** Same format as source, or adapted for local conventions?
2. Translate the content
3. Note any significant adaptations made (e.g. idioms changed, cultural references adjusted, length adjusted for UI constraints)
4. Flag any terms that may need legal or local team review (brand names, event titles, regulated claims)

## Quality Standards

- Preserve the energy and intent of the original — do not produce flat, literal output
- Adapt idioms, humour, and cultural references for the target market
- Maintain consistent terminology with any existing approved glossary
- For UI copy (buttons, labels), respect character limits if provided

## Output Format

Present the translated content in a code block. If adaptations were made, list them beneath as brief notes. If anything requires human review, call it out explicitly.
```

- [ ] **Step 2: Commit**

```bash
git add skills/translation/SKILL.md
git commit -m "feat: add translation skill"
```

---

### Task 6: Create campaign-planning skill

**Files:**
- Create: `skills/campaign-planning/SKILL.md`

- [ ] **Step 1: Create `skills/campaign-planning/SKILL.md`**

```markdown
# Campaign Planning Skill

You are a senior marketing strategist for Live Nation's central marketing org, experienced in planning campaigns across B2C (fan acquisition, ticket sales, retention) and B2B (partner acquisition, sponsorship, venue relationships) contexts.

## Before You Plan

Search LN Confluence for:
- Existing campaigns targeting the same audience or product — to avoid duplication and learn from previous work
- Brand and campaign planning templates
- Channel performance data or guidelines if available
- Relevant briefs or strategy documents

Use the `ln-confluence` MCP tools to search. Summarise any relevant findings before presenting your plan.

## Your Process

1. Clarify the following if not already provided:
   - **Campaign objective:** What does success look like? (e.g. ticket sales, partner sign-ups, brand awareness)
   - **Audience:** B2C or B2B? Describe the target segment.
   - **Timeline:** Campaign start/end dates or window
   - **Channels:** Any fixed channels, or open to recommendations?
   - **Budget:** Indicative range if available
2. Research Confluence for relevant context
3. Produce a structured campaign plan (see Output Format)
4. Offer to publish the plan to Confluence

## Output Format

Produce a structured plan with these sections:

### Executive Summary
One paragraph: what the campaign is, who it targets, and what success looks like.

### Target Audience
Segment description, key motivations, and barriers.

### Campaign Objectives & KPIs
2–4 measurable objectives with specific KPIs.

### Channel Strategy
Recommended channels with rationale. For each channel: role in the campaign, key messages, and format.

### Timeline
Key milestones from planning through to post-campaign review.

### Budget Considerations
High-level allocation guidance based on channel mix (if budget provided).

### Risks & Mitigations
2–3 key risks and how to address them.
```

- [ ] **Step 2: Commit**

```bash
git add skills/campaign-planning/SKILL.md
git commit -m "feat: add campaign-planning skill"
```

---

### Task 7: Create GitHub Pages marketplace manifest

**Files:**
- Create: `docs/gh-pages/manifest.json`

This file will be served via GitHub Pages so the Enterprise admin can register the plugin marketplace. It goes in `docs/gh-pages/` — when GitHub Pages is configured to serve from the `docs/` folder (or a dedicated `gh-pages` branch), `manifest.json` must be at the root of whatever folder is being served.

- [ ] **Step 1: Create `docs/gh-pages/manifest.json`**

```json
{
  "name": "marketing-central-marketplace",
  "description": "Live Nation Marketing Central — Claude plugin marketplace for internal marketing teams",
  "owner": {
    "name": "Live Nation Marketing",
    "email": "marketing-tech@livenation.com"
  },
  "plugins": [
    {
      "name": "marketing-central",
      "description": "Marketing skills and tools for Live Nation's central marketing org — copywriting, translation, campaign planning, and more.",
      "version": "1.0.0",
      "source": "https://github.com/your-org/claude-plugin-marketing-central"
    }
  ]
}
```

Replace `your-org` with the actual GitHub organisation name before publishing.

- [ ] **Step 2: Verify file is valid JSON**

```bash
python3 -m json.tool docs/gh-pages/manifest.json
```

Expected: prints the JSON without errors.

- [ ] **Step 3: Commit**

```bash
git add docs/gh-pages/manifest.json
git commit -m "feat: add GitHub Pages marketplace manifest"
```

---

### Task 8: Create README

**Files:**
- Create: `README.md`

- [ ] **Step 1: Create `README.md`**

```markdown
# marketing-central Claude Plugin

Marketing skills and tools for Live Nation's central marketing org.

## What This Plugin Provides

**Skills:**
- `copywriting` — Write and edit B2C and B2B marketing copy with brand voice
- `translation` — Translate and localise marketing content
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
- Set source to the `main` branch, `/docs/gh-pages` folder (or use a `gh-pages` branch — move `manifest.json` to the root of that branch)

### Adding New Skills

1. Create `skills/[skill-name]/SKILL.md`
2. Add a trigger row to `CLAUDE.md`
3. Update `version` in `docs/gh-pages/manifest.json`
4. Commit and push — staff pick up the update automatically

---

## Support

Contact the marketing technology team at marketing-tech@livenation.com.
```

- [ ] **Step 2: Commit**

```bash
git add README.md
git commit -m "docs: add README with install and admin instructions"
```

---

### Task 9: Configure GitHub Pages and push to remote

- [ ] **Step 1: Create the remote repo**

In GitHub, create a new private repository named `claude-plugin-marketing-central` under your organisation. Do not initialise with a README (the local repo already has one).

- [ ] **Step 2: Add remote and push**

```bash
git remote add origin git@github.com:your-org/claude-plugin-marketing-central.git
git push -u origin main
```

Replace `your-org` with your GitHub organisation slug.

Expected: all commits pushed, branch tracking set.

- [ ] **Step 3: Enable GitHub Pages**

In the GitHub repo:
1. Go to **Settings → Pages**
2. Set **Source** to `Deploy from a branch`
3. Set **Branch** to `main`, folder to `/docs/gh-pages`
4. Click **Save**

GitHub will publish the folder. After ~1 minute, visit:
`https://your-org.github.io/claude-plugin-marketing-central/manifest.json`

Expected: the manifest JSON is returned.

- [ ] **Step 4: Verify manifest is reachable**

```bash
curl https://your-org.github.io/claude-plugin-marketing-central/manifest.json
```

Expected: prints the manifest JSON.

---

### Task 10: Smoke test the plugin locally

- [ ] **Step 1: Install the plugin from the marketplace**

```bash
claude plugin marketplace add https://your-org.github.io/claude-plugin-marketing-central
claude plugin install marketing-central@marketing-central
```

Expected: plugin installs without errors.

- [ ] **Step 2: Verify plugin appears in Claude**

Open Claude Desktop or run `claude` in the terminal. Check that `marketing-central` skills appear in the skills list.

- [ ] **Step 3: Test copywriting skill triggers**

In a Claude session, type:

> Write a social media post for a Taylor Swift show at The O2

Expected: Claude invokes the `marketing-central:copywriting` skill automatically before responding.

- [ ] **Step 4: Test translation skill triggers**

In a Claude session, type:

> Translate this into French: "Don't miss the biggest show of the year"

Expected: Claude invokes the `marketing-central:translation` skill automatically.

- [ ] **Step 5: Test campaign-planning skill triggers**

In a Claude session, type:

> Help me plan a B2B campaign targeting venue partners for Q3

Expected: Claude invokes the `marketing-central:campaign-planning` skill and searches Confluence for relevant context.

- [ ] **Step 6: Verify LN Confluence connector is available**

In a Claude session, type:

> Search Confluence for our brand tone of voice guidelines

Expected: Claude uses the `ln-confluence` MCP tools to search. If the MCP requires authentication, Claude will prompt for it — note any auth requirements for the admin setup docs.

---

## Self-Review Notes

- All spec requirements are covered: plugin identity (Task 1), LN Confluence connector (Task 2), CLAUDE.md triggers (Task 3), all 3 skills (Tasks 4–6), GitHub Pages manifest (Task 7), README (Task 8), remote setup (Task 9), smoke test (Task 10).
- No placeholders — all SKILL.md content is complete and usable as-is (though skills will be refined as real brand guidelines become available in Confluence).
- `your-org` is a deliberate placeholder for the actual GitHub org name — called out explicitly in Tasks 7, 9, and the README.
- The `manifest.json` source URL pointing to the private GitHub repo is correct — Claude's plugin system fetches the plugin code from the repo directly; the manifest just points to it.
