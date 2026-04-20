---
client_name: XP Labs
client_slug: xp-labs
motion: companionship-for-men (multi-model)
created: 2026-04-13
pivoted: 2026-04-20
restructured_multimodel: 2026-04-20
status: pre-first-model
---

# XP Labs — Quick Reference

## Motion Overview
- **What XP Labs is:** the multi-model command center for operating **explicitly AI-disclosed** companion personas that provide companionship to men who knowingly seek AI companionship.
- **What XP Labs is NOT:** a content-generation platform, a producer of explicit media, or a system that hides the AI nature of its personas.
- **Revenue model:** each companion monetizes via subscriptions + PPV messaging on downstream fan platforms. XP Labs captures the operating intelligence across models.

## Core product commitment
**Upfront AI-disclosure** on every platform, every companion, every first interaction. Enforced structurally — see the AI-disclosure rail in `CLAUDE.md`. Customers are men who *prefer* AI specifically because it's judgment-free and pressure-free; our disclosure is what makes that relationship legitimate.

## Target audience
Men who knowingly seek AI companionship. Sub-segments to research:
- Post-divorce men 35–50
- Remote-work isolated men 25–40
- Widowers 55+
- Never-married men 35+
- Men who specifically prefer AI over human interaction for judgment-free venting

(See `<model>/knowledge_base/audience/` once models are populated.)

## Active models
| Model | Status | Niche | Primary Platform | AI-Disclosure ✓ |
|---|---|---|---|---|
| _(none yet — first model pending)_ | | | | |

## Current state
- **Repo pivoted + restructured:** 2026-04-20 (companionship motion, multi-model layout)
- **Seed source:** `notes/canvas.md` — masterclass transcript on AI-companion-persona operations. Not yet ingested.
- **Total models:** 0
- **Total knowledge nodes across all models:** 0

## Priority actions
1. Decide on the first model's slug (e.g., `ava-laurent`)
2. `/ingest notes/canvas.md --model <first-model>` (auto-runs `/quickstart` to scaffold)
3. Run audience research via the `market-research-knowledge-base` skill → populates `<model>/knowledge_base/audience/`
4. `/generate-niche --model <first-model>`
5. `/build-companion --model <first-model>` — make sure AI Disclosure section is filled concretely
6. `/draft-story-arc` + `/write-dm-script`
7. `/graph-health --model <first-model>` to verify rails pass before any launch

## Navigation
- System guide: `CLAUDE.md`
- Shared taxonomy/ontology: `_system/knowledge_graph/`
- Shared templates: `templates/`
- Seed notes: `notes/canvas.md`
- Per-model workspace: `<model-name>/knowledge_base/` + `<model-name>/00_foundation/`

## Ethical guardrails (enforced structurally)
- SFW only — no explicit content
- Upfront AI-disclosure (rail-enforced; graph-health blocks on missing disclosures)
- No targeting acute crisis signals — scripts must route to resource links, not PPV
- Subscriber DMs stay on-platform; no data exfiltration
