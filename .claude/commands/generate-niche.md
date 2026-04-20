---
name: generate-niche
description: Generate blue-ocean niche ideas for XP Labs companions
model: inherit
---

# Generate Niche — XP Labs

Generate blue-ocean niche candidates using the three-dimensional formula:
**aesthetic category × distinctive trait × irrational passion**

## Input

Required: `--model <model-name>` — the target model folder whose niche is being scoped or swapped. If missing, list existing model folders at the repo root and ask which one this niche is for. If no model folders exist, tell the user to run `/quickstart <model-name>` first.

Optionally the user may also provide:
- A target audience segment (e.g., "post-divorce men in their 40s")
- A free slot in the portfolio ("we already have a cottagecore homesteader and a skater — find us a third")
- No extra context — in which case propose a starting set

## Process

### 1. Ground in audience
Read `<model-name>/knowledge_base/audience/` to identify:
- Which segments we have intel on
- Which pains are most acute (status: validated or canonical preferred)
- What desires and exact-language phrases are documented

If the knowledge base is empty, note that and propose niches speculatively with explicit `[INFERRED]` attribution.

### 2. Survey existing niches and competitors
- Read `<model-name>/knowledge_base/niches/` — what we've already tried, what's validated
- Read `<model-name>/knowledge_base/competitors/` — what's saturated vs. underserved
- Read `<model-name>/knowledge_base/companions/active/` (via `00_foundation/companions/active/`) — what aesthetics/passions are already deployed (avoid overlap)

### 3. Generate candidates

Propose **5 niche candidates**. For each, provide:

```
### Niche [N]: [Niche name]

**Aesthetic:** [category — e.g., coastal wellness, dark academia, cottagecore]
**Trait:** [distinctive physical or identity trait — e.g., freckled redhead, athletic caramel skin, always in reading glasses]
**Passion:** [something men are irrationally passionate about — e.g., Ironman, classic cars, rare-breed chickens, obscure Russian literature]

**Targets:** [[segment-*]] or [audience hypothesis if no segment exists]

**Why it's blue ocean:** [what makes this combination uncontested — what's adjacent but NOT this]

**Content angle hypotheses:** [3–5 reel / carousel / post ideas that demonstrate the niche immediately]

**Risk:** [what could go wrong — too narrow, too adjacent to a banned category, hard to visually represent, etc.]
```

### 4. Recommendation

After the five candidates, recommend:
- **Top pick** to scope next — which niche has the strongest signal-to-risk ratio
- **Runner-up** — a backup if the top pick proves impractical
- **Skip** — candidates that look interesting but shouldn't be pursued (and why)

### 5. Offer to persist

Offer to write the top pick as a new node in `<model-name>/knowledge_base/niches/niche-<slug>.md` using `templates/niche-template.md`, with `status: emergent`.

## Guardrails
- Every niche must have an audience hook — not "this looks cool" but "this addresses pain/desire X in segment Y"
- No explicit content — this is the non-explicit motion. The passion and trait axes can be edgy; the aesthetic category and overall content must be Instagram-safe
- Avoid direct clones of examples in `<model-name>/knowledge_base/competitors/`
- Flag any niche that might be banned by IG/TikTok content policy

## Example (from the canvas.md masterclass, adapted for SFW)
```
Niche: Grandmother golfer with a brunette bob
  - Aesthetic: country-club retiree
  - Trait: sun-kissed silver hair, still has the athletic frame from her tennis years
  - Passion: obsessively competitive at golf, posts her handicap progression
  - Targets: [[segment-post-retirement-men-60s]] — the widower pain cluster
  - Blue ocean: adjacent to the generic-blonde-influencer saturation, taps men with a "sophisticated older woman" kink that IG won't ban as long as dress stays country-club
```
