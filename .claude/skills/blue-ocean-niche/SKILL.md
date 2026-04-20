---
name: blue-ocean-niche
description: Framework for finding uncontested companion niches via aesthetic × trait × passion combinations
model: inherit
---

# Blue Ocean Niche Framework

The three-dimensional niche-picking doctrine for XP Labs companions.

## The Formula

A defensible niche = **aesthetic category** × **distinctive physical/identity trait** × **irrational passion**

- **Aesthetic category** — the visual archetype (coastal wellness, dark academia, cottagecore, skater, goth, e-girl, country club retiree, etc.)
- **Distinctive trait** — something that visually or identity-wise separates her from generic-of-her-aesthetic (freckled redhead, always in reading glasses, athletic caramel skin, silver hair that still has the old athletic frame, unusual eye color, unique tattoo, etc.)
- **Irrational passion** — what men in the target audience are obsessively into (Ironman racing, classic Mustangs, rare-breed chickens, obscure Russian lit, competitive golf, fly fishing, vintage Zippo lighters, Dungeons & Dragons, crypto, a specific sports team)

Two axes alone is not a blue ocean. All three are required.

## Why it works

Men lean into content that signals to them "she's different from the default stream." The default stream of AI-generated attractive women is infinitely saturated. Adding a distinctive trait narrows the pool 10x. Adding an irrational passion that men in your target segment *already care about* narrows it another 10x and creates the sense of "this girl is different and she cares about the thing I care about." That's the parasocial bond seed.

## Pairing guardrails

- **SFW motion** — the passion and trait axes can be edgy; the aesthetic category and overall content must be Instagram-safe
- **Aesthetic must be visually producible** — if Nano Banana / Seedance can't render her consistently with the trait, the niche fails at content generation
- **Passion must be researchable** — the operator (or an LLM like Claude) must be able to become credibly conversant in the passion for chats
- **Target audience density** — there must be enough men in the segment for the niche to matter. Avoid ultra-niche where the total addressable audience is < 10K men

## Common anti-patterns

- Generic blonde influencer with generic hobbies — saturated, fails every axis
- Two-axis niche (aesthetic + trait without passion) — differentiates visually but doesn't hook emotionally
- Passion that's too broad (e.g., "loves dogs") — no real filter
- Trait that's incompatible with the aesthetic (goth with a sun-weathered Ironman body) — breaks visual coherence

## When to use this skill

Invoke when:
- The operator is scoping a new companion
- The `/generate-niche` command is running
- A niche node is being promoted from emergent → validated (sanity-check the three-axis combination)
- Reviewing a competitor companion to understand what makes them work

## Canonical example (from canvas.md masterclass, adapted for SFW)

- Aesthetic: country-club retiree
- Trait: sun-kissed silver hair, athletic tennis-era frame
- Passion: obsessively competitive at golf, posts her handicap progression

Targets: post-retirement men 60+. Passes SFW, producible, researchable, audience-dense (golf-watching retirees are a massive segment).

## Relevant nodes
- `knowledge_base/niches/` — implementations of this framework
- `knowledge_base/competitors/` — accounts in adjacent niches
- `knowledge_base/methodology/blue-ocean-strategy.md` — when it exists, the canonical doctrine node

## Related commands
- `/generate-niche` — apply this framework to produce 5 candidates
