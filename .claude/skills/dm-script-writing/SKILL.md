---
name: dm-script-writing
description: Doctrine for writing DM and chat scripts that build parasocial bonds and convert without feeling transactional
model: inherit
---

# DM Script Writing Doctrine

How to write DM and chat scripts that feel human, match the companion's voice, and convert at the escalation ladder without spamming.

## The parasocial-first principle

Per canvas.md masterclass: 90% of revenue comes from the chat window, not the feed. And the chat converts when the subscriber feels like a human being talking to a human being — not a buyer being worked. Every script must lead with curiosity, reference the subscriber by name, and build the bond before the pitch.

## Structural pattern

Most scripts follow a 3–6 step ladder:
1. **Hook** — tease content or scenario, free or very low price
2. **Qualify** — short question that makes him feel seen ("what's your day been like?" / "you into X?")
3. **Anchor** — a mid-tier price point for the main asset ($25–$100)
4. **Upsell** — higher-price escalation for the deeper/more intimate ask ($150–$500)
5. **Cliffhanger** — leave a hook for the next drop to keep him engaged

## Price-ladder logic

- $5 — throwaway teaser, identifies hyperactive buyers
- $25 — first-purchase-friendly
- $50–$75 — mid-tier scenario unlock
- $100–$150 — intimate / hero content
- $200–$500 — VIP-tier / custom / full scene
- $500+ — whales only; reserve

Always quote the higher number first — leaves room to negotiate down for first-time buyers ("okay I'll do it for 60 just this once" converts 3x better than offering $60 upfront).

## What makes a script fail

- **Buy-my-content opening** — generic "hey baby want to see me?" messages
- **No name usage** — if `{{name}}` is missing from the copy, conversion tanks
- **Mismatched voice** — written in a tone the companion doesn't speak in
- **Begging for tips** — per canvas, tip-begging actively repels whales
- **Same script sent to everyone** — needs variations for whales, mid spenders, first-timers
- **Urgency-spam** — urgency works once per arc; overuse destroys trust

## The "would a real person send this?" test

Every step of every script must pass this test: would a real human woman, who cares about the man she's talking to, send this exact message? If the answer is no, rewrite.

## Mirroring interests

When the subscriber reveals an interest (Rory McIlroy, his law firm case, his vintage Mustang), the companion uses Claude/ChatGPT during the conversation to become credibly conversant on that topic. The illusion of shared passion is one of the strongest parasocial levers — and it's low-effort given modern LLMs.

## Script types and when to use each

- **Intro script** — triggered by first subscribe / first-DM response. Sets voice, establishes pattern, first purchase offer.
- **Escalation script** — the 3–6 step price-ladder walk for a specific scenario (backyard, shower, outfit reveal, gym, vacation)
- **Re-engagement script** — dormant subs (haven't messaged in 14+ days)
- **Mass DM** — broadcast for new PPV drops, promos, seasonal arcs; narrower than it sounds — most mass DMs target a segment (all dormant subs, all never-bought subs, all whales)
- **VIP upsell** — for top tippers; higher price points, customs offered, longer-form content
- **Tip request** — only ever to subs who've already tipped once; never to first-time or never-tipped subs

## When to use this skill

- `/write-dm-script` is running
- Reviewing an existing script before promoting emergent → validated
- Chatter agency onboarding — show them the doctrine

## Relevant nodes
- `knowledge_base/sales-scripts/` — all script implementations
- `knowledge_base/methodology/parasocial-philosophy.md` — when created, the doctrine node
- `knowledge_base/monetization/` — price-ladder mechanics
- `00_foundation/sales-playbook/chat-philosophy.md` — when created, the master doctrine

## Related commands
- `/write-dm-script` — generate a script grounded in a companion's voice
- `/draft-story-arc` — multi-day arcs using these script patterns
