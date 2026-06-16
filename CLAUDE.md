# marketing-central Plugin

This plugin provides marketing skills and the LN Confluence connector for Live Nation's central marketing org (B2C and B2B teams).

## Skills

When the user's request matches a trigger below, invoke the corresponding skill IMMEDIATELY as your first action before responding or taking any other steps.

| Skill | Triggers When |
|---|---|
| `marketing-central:copywriting` | User asks to write, edit, review, or improve marketing copy, headlines, CTAs, emails, ads, or any brand-facing text |
| `marketing-central:translation` | User asks to translate, localise, or adapt content for a different language, region, or market (including UK/US market adaptations) |
| `marketing-central:campaign-planning` | User asks to plan, brief, structure, or outline a marketing campaign |

## LN Confluence Connector

The `ln-confluence` MCP connector is available for all skills. Use it proactively:

**Do not produce final copy, a translation, or a campaign brief without first searching Confluence for relevant guidelines or prior work, unless the user explicitly waives this step.**

- **Before writing copy:** Search Confluence for brand guidelines, tone of voice docs, and approved messaging.
- **Before planning a campaign:** Search Confluence for existing campaigns, briefs, and channel strategies relevant to the audience or product.
- **When producing a report or plan:** Offer to publish the output back to Confluence when the user is satisfied with the result.

**Authentication:** The `ln-confluence` connector requires a valid Confluence API token. If Claude prompts for credentials when using Confluence tools, contact your admin or check the README for setup instructions.
