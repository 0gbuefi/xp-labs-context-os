---
name: write-dm-script
description: Draft a DM / chat script for a companion (intro, escalation, re-engagement, VIP, mass DM)
model: inherit
---

# Write DM Script — XP Labs

Produce a ready-to-use DM script for a companion, in her voice, grounded in audience intel.

## Input

Required: `--model <model-name>` — the model folder to read from and write into. If missing, list existing models and ask.

The user also specifies:
- **Companion** — which companion inside this model (usually the model's own companion — 1 companion per model in the typical case)
- **Script type** — intro / escalation / re-engagement / mass-dm / vip-upsell / tip-request / story-arc
- **Scenario** (optional) — e.g., "just got home from gym", "Easter", "she just bought a new camera"
- **Price ladder** (optional) — if not provided, derive from companion's monetization mechanics

If the user omits any of these, ask. Don't guess the companion.

## Process

### 1. Read companion
Pull the companion character sheet — especially the **Chat Tone Guide**, **Personality Traits**, and **Lifestyle/Backstory**. The script must match her voice exactly.

### 2. Read methodology
Read `<model-name>/knowledge_base/methodology/parasocial-philosophy.md` and `subscriber-segmentation.md` (if they exist). The script must follow the human-first doctrine:
- Use the recipient's name
- Lead with curiosity, not content
- Mirror his interests (even if fabricated on-the-fly via ChatGPT/Claude lookup)
- Build the parasocial bond before any price
- No begging, no spammy "buy my content"

### 3. Read existing scripts
Check `<model-name>/knowledge_base/sales-scripts/` for similar existing scripts. Don't duplicate — reference and vary.

### 4. Ground in audience pain / desire
Pick 1–2 specific pain or desire nodes the script is `derived-from`. The emotional hook should tie to something real we've documented about the target segment.

### 5. Draft the script

Use `templates/script-template.md`. Fill every step with:
- **Exact message copy** (with `{{name}}` placeholder for personalization)
- **Asset** — what image or video accompanies it (describe in enough detail that a content creator can generate it)
- **Price point** — free / $X / free with sub / etc.
- **Expected positive reply** — what engagement looks like when it's working
- **Fallback** — what to send if the recipient goes quiet or pushes back

### 6. Add variations
Provide at least 2 variations:
- **For whales** — extra personalization, more story, higher opening price
- **For cautious first-timers** — lower first unlock, heavier tease, soft urgency only

### 7. Save and report

Save to `<model-name>/knowledge_base/sales-scripts/script-<type>-<slug>.md`. Link the companion back to the script.

Report:
```
✅ Script drafted: script-<type>-<slug>.md

For: [[companion-<slug>]]
Type: [script type]
Sequence length: [N] steps
Price range: $[low]–$[high]
Derived from: [[pain-<slug>]] or [[desire-<slug>]]

Next:
1. Test on [N] subs this week
2. After [N] uses, review performance and upgrade status to validated if conversion > [X]%
```

## Guardrails
- The script must sound like the companion, not a generic template
- Keep steps concrete — generic "tease her" steps are failures
- SFW motion: the escalation ladder can get flirty but never explicit
- Every price point has a rationale — not arbitrary round numbers
- When in doubt, read the canvas.md masterclass sections on script design and chat philosophy (<model-name>/knowledge_base/notes/canvas.md around lines 430–510 for the canonical astronaut/backyard script examples)
