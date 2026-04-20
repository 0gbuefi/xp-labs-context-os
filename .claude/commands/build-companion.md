---
name: build-companion
description: Draft a full companion character sheet from a niche brief
model: inherit
---

# Build Companion — XP Labs

Turn a niche brief into a full companion character sheet ready to be brought to life on platforms.

## Input

Required: `--model <model-name>` — the model folder this companion belongs to. Conventionally this is the same as the companion's firstname-lastname slug.

**Auto-scaffold behavior:** if `<model-name>/` doesn't exist at the repo root, automatically run `/quickstart <model-name>` first (no prompt needed — the companion needs a home).

The user also provides one of:
- A niche name or slug already in `<model-name>/knowledge_base/niches/`
- A niche brief inline ("I want a dark-academia bookstore girl who's into obscure Russian literature")
- Nothing — in which case, ask which niche to build from (list `<model-name>/knowledge_base/niches/` for options)

## Process

### 1. Ground in the niche

Read the niche node. Pull:
- The three-dimensional formula (aesthetic × trait × passion)
- The audience segment it targets
- Content angle hypotheses

If the niche doesn't exist as a node yet, propose creating one first with `/generate-niche`.

### 2. Ground in audience

Read the audience segment(s) the niche targets. Pull:
- Daily reality of the target men
- Exact-language phrases
- Top pains and desires

### 3. Draft the character sheet

Use `templates/companion-node-template.md`. Fill every section concretely — no placeholders:

- **Name** — pick a first+last name that fits the aesthetic and niche. Not generic.
- **Look / Appearance** — age range, hair, eyes, build, signature aesthetic (outfit palette, silhouette, accessories). Must pass "I can generate 50 consistent images of her" test.
- **Personality Traits** — 3–6 traits with the underlying tension (e.g., "Confident but not arrogant"). Match the niche vibe.
- **Lifestyle / Backstory** — where she's from, what she does, what her days look like, relationships, non-negotiables. This is the D&D character sheet — deep enough that a chatter can stay in voice after months.
- **Content Themes** — 4–6 content pillars that echo the audience's desires and the niche's passion axis.
- **Chat Tone Guide** — specific rules. Sentence length, slang use, emoji use, formality, flirtation level, exact phrases she WILL use and WON'T use. Critical for consistency across IG captions, bridge-page copy, and DMs.

### 4. Propose supporting nodes

Also generate (or propose) the companion's starter ecosystem:
- **Suggested platforms** — which 2–3 platforms to launch on (usually IG primary + X secondary + one feeder like TikTok or Threads). Link the relevant `[[platform-*]]` playbooks.
- **Suggested monetization** — subscription price, 3-tier PPV ladder, recommended story-arc themes. Link the relevant `[[monetization-*]]` mechanics.
- **Intro script hook** — a 3-step intro DM sequence that matches her voice. Can link to an existing `[[script-intro-*]]` template or propose a new one.

### 5. Write the node

Save to `<model-name>/knowledge_base/companions/companion-<firstname>-<lastname>.md` with:
- `status: emergent`
- Full frontmatter per template
- All required links (niche, audience segment, platforms, monetization mechanics)

Also create a stub in `<model-name>/00_foundation/companions/queue/<slug>.md` with:
- Link back to the knowledge_base node
- Launch checklist: reference images ready, platform accounts registered, bridge page set up, first 7 days of content drafted

### 6. Report

Output:
```
✅ Companion drafted: [Name]

Knowledge node:  <model-name>/knowledge_base/companions/companion-<slug>.md
Queue entry:     <model-name>/00_foundation/companions/queue/<slug>.md

Niche: [[niche-<slug>]]
Targets: [[segment-<slug>]]
Platforms: IG, X, [feeder]
Monetization: sub $13/mo, PPV ladder 25/75/150, Easter story-arc

Next steps:
1. Generate reference image set (5–10 poses, consistent face via Nano Banana 2 + reference image)
2. Register platform handles
3. Draft week 1 content: /draft-story-arc
4. Draft intro DM: /write-dm-script
```

## Guardrails
- Every section must be concrete. No "vibes-based". A ghost-writer should be able to operate her after reading the sheet.
- Voice consistency is the #1 predictor of whale retention per canvas.md — give the Chat Tone Guide extra care.
- This is the SFW motion — she can be flirty but not explicit. Content themes must be IG-safe.
