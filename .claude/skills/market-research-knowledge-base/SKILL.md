---
name: market-research-knowledge-base
description: XP Labs's audience-research methodology — how to find and mine the exact language lonely men use online
model: inherit
---

# Audience Research Knowledge Base

## What Is This?

XP Labs's **audience research methodology repository** — the HOW of finding and mining the real language of men seeking companionship.

**Purpose:**
- Store techniques, platforms, and processes for finding where target audiences talk online
- Extract authentic voice-of-audience phrases to power niche ideation, content hooks, and DM scripts
- Compound research methodology expertise over time

**Scope:**
- **Methodology-focused:** HOW to research audiences, not WHAT specific companions say
- Continuously evolving as the operator ingests new research techniques

## When to use this skill

Invoke when:
1. **Scoping a new audience segment** — e.g., "Where do post-divorce men in their 40s talk about loneliness online?"
2. **Finding content/script hooks** — What phrases is the segment using to describe their pain?
3. **Validating a pain point** — Is this pain real and specific, or are we projecting?
4. **Mining voice-of-audience** — What words, metaphors, and rhythms do these men use so a companion can mirror them?
5. **Scoping research effort** — How much intel do we need before launching a new companion?
6. **Deciding where to look** — Which platforms surface this segment most densely?

## Canonical sources for XP Labs's motion

Lonely-men audience density is high on:
- **Reddit:** r/lonely, r/ForeverAlone, r/Divorce, r/Widowers, r/AskMenOver30, r/dating_advice (men's perspective), niche-specific subreddits matching each companion's passion axis
- **YouTube comment sections:** male-targeted self-help / dating / fitness / stoicism channels
- **Forums:** PurseForum (no), pick-up artist forums (legacy), MMA / gear / hobby forums where men vent in off-topic threads
- **Twitter/X:** reply guys under male-self-help posts, quote-tweets of influencers addressing dating market
- **TikTok comment sections:** same as YouTube, faster cadence
- **Discord / niche communities:** gaming / hobby / crypto servers where loneliness leaks into general-chat

## Core principles (methodology doctrine)

1. **Anonymous-platform advantage** — men are more honest about loneliness when their real identity isn't attached. Reddit > LinkedIn > X personal account.
2. **Listen, don't ask** — direct surveys produce sanitized answers. Reading existing threads where men were already venting produces raw language.
3. **Identity × Problems × Dreams × Obstacles** — for any segment, extract all four: who he thinks he is, what's wrong, what he wants, what blocks him.
4. **Capture verbatim, not paraphrased** — the value is in exact phrases. Paraphrasing strips the raw material.
5. **Three-pass research:** broad (find the watering holes) → focused (the top 5–10 threads or posts) → edge cases (where does the pattern break?)
6. **Saturation threshold** — stop when new threads stop producing new phrases or patterns. Usually 15–30 sources per segment.

## Integration with the main knowledge graph

- This skill holds **methodology** (HOW)
- `knowledge_base/audience/` in the main repo holds **instances** (WHAT specific men say, organized by segment/pain/desire/language)
- When running research, apply the methodology here → produce nodes there

Example flow:
```
Task: research the "post-divorce men 40s" segment for XP Labs

1. Apply anonymous-platform-advantage → start on r/Divorce and r/DadForADay
2. Apply three-pass research → scan 20 threads, collect verbatim
3. Apply Identity × Problems × Dreams × Obstacles → organize findings
4. Produce nodes:
   knowledge_base/audience/segment-post-divorce-men-40s.md
   knowledge_base/audience/pain-co-parenting-loneliness.md
   knowledge_base/audience/language-common-phrases-r-divorce.md
```

## Node structure (for nodes inside this skill's internal KB)

Methodology nodes inside this skill follow the same format as the main Context OS:
- Frontmatter with domain, status, topics, related_concepts
- Minimum 3 links
- Source attribution

## Quick reference
- **Ingest methodology content into this skill's KB:** paste into `canvas.md`, run `Ingest this canvas into the audience research knowledge base`
- **Apply methodology to a real research task:** invoke this skill, then save outputs to `knowledge_base/audience/` in the main repo

---

**Scope:** XP Labs audience-research methodology (companionship-for-men motion)
