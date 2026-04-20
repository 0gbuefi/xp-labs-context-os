---
name: performance-review
description: Weekly performance review across XP Labs's active companions
model: inherit
---

# Performance Review — XP Labs

Run a weekly or monthly review across all active companions, produce a sitrep, and promote emergent patterns to validated/canonical status.

## Input

Required: one of `--model <model-name>` or `--all`.
- `--model <name>` → review a single model
- `--all` → iterate every model folder at the repo root and produce per-model sitreps (no cross-model rollup yet)

The user also specifies:
- **Cadence** — `weekly` (default) or `monthly`
- **Date range** (optional) — defaults to the last 7 or 30 days

## Process

### 1. Read operational state

- List `<model-name>/00_foundation/companions/active/` — every active companion
- Read each companion's latest operational file + the knowledge_base node

### 2. Collect metrics

For each companion, the operator should have supplied (or you should prompt for):
- Followers gained this period (per platform)
- Subs gained / churned
- Revenue: subs, PPV, tips, mass-DM recoveries
- DM conversion rate (subs → first PPV buyer)
- Best-performing post / reel / story arc
- Worst-performing ditto
- Any ban risk events, account warnings, platform issues

If the operator hasn't recorded metrics, tell them clearly what's missing and ask for input before proceeding.

### 3. Identify patterns

Across all companions this period, look for:
- **Scripts that outperformed** — candidates to promote to `validated`
- **Scripts that underperformed twice or more** — candidates to archive or rewrite
- **Niche signals** — which niches are pulling more than others? Scale vertical or horizontal?
- **Platform signals** — which platforms returned the best per-hour ROI?
- **Objection patterns** — what's coming up repeatedly in DMs that the current script library doesn't address? Create a new objection-handling node.

### 4. Write the sitrep

Save to `<model-name>/00_foundation/_synthesis/weekly-sitreps/sitrep-[YEAR]-W[NN].md` (or `monthly-reviews/review-[YEAR]-[MM].md`).

Include:
- **Headline** — the one sentence the operator should know if they only read the title
- **Wins** — top 3–5
- **Losses** — top 3 with brief post-mortem
- **Companion-by-companion rundown** — 3-line summary each
- **Emergent patterns** — bullet list of hypotheses this week produced
- **Knowledge graph actions taken** — which nodes were promoted in status, which were created, which were retired
- **Next week priorities** — 3 concrete actions with owners

### 5. Promote nodes

Based on patterns:
- Promote `status: emergent → validated` on any node that proved out this period (reference ≥ 2 uses with positive signal)
- Promote `status: validated → canonical` on any node referenced ≥ 5 times across companions
- Flag `emergent` nodes > 90 days old with no validation for archive

Update the affected nodes directly.

### 6. Update strategic synthesis

If any pattern this week is big enough to affect the quarterly plan, add a line to `<model-name>/00_foundation/_synthesis/strategic-synthesis.md` with the date and the insight.

### 7. Report

```
✅ Sitrep written: <model-name>/00_foundation/_synthesis/weekly-sitreps/sitrep-2026-W16.md

Period: [date range]
Companions reviewed: [N]
Revenue (period total): $[N]
Best performer: [[companion-<slug>]] at $[N]

Nodes promoted:
- [[script-intro-backyard]]: emergent → validated
- [[monetization-easter-arc]]: validated → canonical

Nodes flagged for review:
- [[niche-<slug>]]: 90+ days emergent, no traction

Top priorities next period:
1. [...]
2. [...]
3. [...]
```

## Guardrails
- Never invent metrics. If the operator hasn't provided them, stop and request them.
- Every promotion or archival action gets an explicit reason in the sitrep
- Keep sitreps tight — a sitrep longer than one screen means you tried to say too much
