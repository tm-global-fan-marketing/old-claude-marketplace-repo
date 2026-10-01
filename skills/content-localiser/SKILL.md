---
name: content-localiser
description: Localise or translate already-approved Ticketmaster and Live Nation content for named markets, applying that market's own approved nuance, positioning, terminology and formatting. Use when a request asks to localise, translate, adapt or "make this work for" a named market or region; asks for a market version of an existing campaign, blog, case study, email, social post or one-sheet; asks what approved content would look like in a market's language; asks to apply a market's date, time, currency or number conventions; or asks to find an existing approved campaign so it can then be localised. Covers fan-facing and client-facing content. Which markets are covered, each market's rules, what is never translated, and where files are published are set by the live Confluence page this skill fetches, not by this description. Do NOT use to write new content, to rewrite copy for brand voice, for social performance reporting, or to draft or validate legal, refund, pricing or consent wording.
---

# Content Localiser

Before producing anything, fetch the live Content Localiser page (`674155845`, space `GB2CM`) via the Confluence MCP connector and follow it exactly.

That page is the source of truth for this skill — the two operating modes and which one applies, the source pages to read and when, the hard limits, the file naming convention, where output is published, and the step-by-step process. Do not reconstruct any of it from memory, and do not treat the `description` above as a substitute for reading the page.

## How pages are read

Only the most current version of any page is ever referenced. Read pages live. Whatever a page says at that moment is what applies, and where something has been taken off a page it no longer applies.

A market's own page governs that market. Nothing about it is cached in this file — not its language, not its rules, not its status. Read it.

## Two rules that are not recoverable if got wrong

- **A market with no approved parameters page is a stop, not a caveat.** Produce nothing for that market and say who to contact. Never fall back on posture-level or global defaults to fill the gap — content built from defaults reads as approved local guidance and is not. Where several markets were named, continue with the ones that have pages and report the gap for the rest.
- **Where the requester asked to localise first and translate after, nothing is published until they have confirmed the draft.** The draft is shown to them, and only a confirmation moves it forward.

## If a page can't be read

- **Can't be reached** — stop, say which page, and ask whether to wait or proceed with the gap flagged.
- **Reached but empty, or doesn't cover what's needed** — say so plainly and don't fill the gap. Carry on with the rest if the rest is enough.
- **Gone, deleted, or archived** — say so. This needs the skill's owner to repoint it; waiting won't fix it.

Never fall back on general knowledge for brand, market, legal, or compliance content. A plausible-sounding translation built from general knowledge is the specific failure this skill exists to prevent.

## Escalation

Owners of source pages set the rules for their subject. They are the escalation point when a source is unclear, contradicts another page, or doesn't cover the request. **They do not approve individual outputs.**

Every output is a draft requiring human review before use — by the market owner named on that market's page, or their team. This skill never represents its output as approved.

## Before editing the description

The `description` is the only part of this skill that can't be fetched live, so it's the only part that can go stale. It's written to describe the kinds of request the page covers, never the page's contents — no market names, no product names, no language lists, no coverage gaps, no claims about other skills.

**A change to the Confluence page should not require a change here.** A market being added, removed, or having its parameters updated changes nothing in this file. Regenerate only when the kind of work changes: a new mode, a new audience class, a new verb.

**It must also stay under the 1024-character SKILL.md limit.** The v1 description exceeded it and was rejected at save time.
