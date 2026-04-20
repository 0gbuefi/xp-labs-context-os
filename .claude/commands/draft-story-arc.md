---
name: draft-story-arc
description: Draft a multi-day / scenario-based story arc for a companion
model: inherit
---

# Draft Story Arc — XP Labs

Produce a multi-day or scenario-based content+script arc that drips content with urgency and builds anticipation.

## Input

Required: `--model <model-name>` — the model folder to read from and write into. If missing, list existing models and ask.

The user also provides:
- **Companion** — which companion inside this model
- **Theme or scenario** — Christmas 12-day, Easter, birthday, a vacation, an outfit drop, "she just moved apartments", a countdown
- **Duration** — 3 / 7 / 12 / 14 / custom days
- **Intended price arc** — free → low → mid → high tiers, or annual-upsell gate

If missing, ask.

## Process

### 1. Ground in companion and audience
Pull companion character sheet + audience segment intel, same as `/write-dm-script`.

### 2. Structure the arc

Design with four elements per day:
- **Content post** (feed / reel / carousel) — what goes on IG/X publicly for attention
- **Story** (24-hour) — what goes on IG Stories / X Fleets / Snap for FOMO
- **DM drop** — what goes to subs that day, with price point
- **Hook for next day** — tease or cliffhanger that pulls engagement forward

### 3. Map to monetization

The arc should route subs through the price ladder. For a 12-day arc:
- Days 1–3: free teases and low-price unlocks ($5–$25)
- Days 4–8: mid-tier unlocks ($50–$100), VIP-tier gates
- Days 9–12: hero content ($150–$300), annual upsell offer

For a 3-day arc: compressed version of the above.

### 4. Build the asset list
Enumerate every image, video, outfit, location, and prop needed to produce the arc. Group by generation batch so the operator can batch-produce on `my postgen` efficiently.

### 5. Save

Write to `<model-name>/00_foundation/campaigns/idea-queue/arc-<companion-slug>-<theme>.md` (if still an idea) or directly to `<model-name>/00_foundation/campaigns/launched/[YEAR]/[MONTH]/week_N/campaign-arc-<slug>.md` if the operator wants to launch now.

Cross-link:
- The companion node gains a link under "Active Scripts" or "Campaigns"
- Any new scripts or content patterns extracted become knowledge_base nodes

### 6. Report
```
✅ Story arc drafted: [theme] for [[companion-<slug>]]

Duration: [N] days
Revenue target: $[low]–$[high] across the arc
Content assets needed: [N images, N videos, N outfits]
Generation batches: [N]

Structure:
- Day 1: [one-line summary]
- Day 2: [...]
- ...

Next steps:
1. Generate asset batches (/tech-stack workflows)
2. Lock draft with operator — move to <model-name>/00_foundation/campaigns/launched/ when scheduled
3. Post-launch: track per-day conversion for the /performance-review
```

## Guardrails
- The arc must have real narrative cohesion — not 12 random posts. Think "movie release: teaser trailer → main trailer → release → epilogue"
- Urgency is earned, not spammed. Only one genuine deadline per arc.
- Match the companion's voice at every step
- SFW only — hero content can be flirty/suggestive, never explicit
