---
name: companion-building
description: Doctrine for building AI companion character sheets that stay in voice across platforms and months
model: inherit
---

# Companion Building Doctrine

How to design an AI companion persona that survives months of operation without drifting out of voice.

## The character-sheet schema

Use `templates/companion-node-template.md`. Every companion ships with six mandatory sections:

1. **Look / Appearance** — specific enough that 50 reference-image generations produce a recognizable same-woman
2. **Personality Traits** — 3–6 traits, each with an underlying tension ("confident but not arrogant", "subtly flirtatious")
3. **Lifestyle / Backstory** — D&D-character-sheet depth: where she's from, what she does, relationships, non-negotiables, pet peeves, what she posts about vs. what she keeps private
4. **Content Themes** — 4–6 content pillars
5. **Chat Tone Guide** — the most important section: sentence length, slang use, emoji use, formality, flirtation level, phrases she WILL use, phrases she WON'T use
6. **Operational metadata** — niche, target audience, platforms, monetization, linked scripts

## The consistency test

A ghost-writer or chatter-agency operator should be able to operate her after reading the sheet. If two operators produce DMs that sound like different women, the sheet is underspecified. The chat-tone guide is the lever that usually needs more specificity.

## Voice as the retention driver

Per the canvas.md masterclass: whales pay for the parasocial relationship, not the content. The relationship is built through voice consistency. A 21-month, $6,000+ subscriber described in the transcript retained because the companion felt like a consistent friend, not because the content was top-shelf.

Consequence: the Chat Tone Guide is load-bearing. Every companion-building session should spend 30–40% of its time there.

## Common failure modes

- **Generic blonde default** — every field filled with the obvious choice. She has no hook.
- **Mismatched axes** — sweet cottagecore aesthetic + aggressive gamer passion + goth personality. Breaks immersion.
- **Under-specified chat tone** — "friendly and flirty" is not enough. Give specific rules: "uses one emoji max per message, never LOL, prefers 'haha', always asks a follow-up question in the first reply."
- **No non-negotiables** — if she'll say anything to anyone, she has no shape. Pick things she WON'T do: won't discuss politics, won't answer "are you real" directly, won't pretend to remember things across reset without a prompt.
- **Backstory too generic** — "grew up in California, loves travel." Fails the Dungeons-&-Dragons depth test. Give her a specific town, a specific high school story, a specific weird thing about her family.

## Scaling pattern

Per canvas.md, winning companions either scale **vertical** (pour resources into one companion until she hits $30–50K/month) or **horizontal** (clone the formula into parallel companions). Both require the character sheet to be specific and defensible — vertical scaling reveals voice drift quickly; horizontal scaling reveals lazy differentiation.

## When to use this skill

- `/build-companion` is running
- The operator is reviewing or editing an existing companion character sheet
- A companion is being promoted from `queue` → `active`
- Chatter onboarding for a companion — give them the sheet as the canonical source

## Relevant nodes
- `knowledge_base/companions/` — all companion character sheets
- `knowledge_base/niches/` — the niche each companion implements
- `knowledge_base/methodology/parasocial-philosophy.md` — when it exists, the doctrine for why voice matters

## Related commands
- `/build-companion` — generates a full character sheet from a niche brief
- `/write-dm-script` — depends on the companion's chat tone guide
