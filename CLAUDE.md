# tm-marketing-core Plugin

This plugin provides marketing skills and the LN Confluence connector for Ticketmaster's central marketing org (B2C and B2B teams).

## Skills

| Skill | When to use |
|---|---|
| `marketing-wizard` | Default entry point — works out what a marketing request needs and routes it to the right skill |
| `backstage-writer` | Write, rewrite, or review marketing copy in the TM/LN brand voice (B2C or B2B) |
| `brief-writer` | Draft a Campaign and Creative Brief for Fan Product Marketing / Brand and Content (B2C only) |
| `content-creator` | Build a B2B campaign — Campaign Messaging Plan plus its assets — around a product, theme, or proposition |
| `content-localiser` | Localise or translate already-approved content for a named market, using that market's approved rules |
| `social-pulse` | Check social performance against market history or peer markets; surface testable content ideas |

Each skill fetches its live Confluence page before producing anything — the page, not the skill file, is the source of truth.

## LN Confluence Connector

The `ln-confluence` MCP connector is available for all skills. Use it proactively:

**Do not produce final copy, a translation, or a campaign brief without first searching Confluence for relevant guidelines or prior work, unless the user explicitly waives this step.**

- **Before writing copy:** Search Confluence for brand guidelines, tone of voice docs, and approved messaging.
- **Before planning a campaign:** Search Confluence for existing campaigns, briefs, and channel strategies relevant to the audience or product.
- **When producing a report or plan:** Offer to publish the output back to Confluence when the user is satisfied with the result.

The `ln-confluence` connector authenticates via SSO — no API key is required.
