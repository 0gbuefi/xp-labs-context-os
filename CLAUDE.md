# XP Labs — Multi-Model Companionship Context OS

**This is XP Labs's command center** — a multi-model Context Operating System where AI compounds intelligence about our audience, each companion persona, their niches, platforms, and campaigns over time.

**Motion:** Provide companionship to men in the AI age via **explicitly AI-disclosed** companion personas operated across social platforms.
**Audience:** Men who knowingly seek AI companionship — they value the judgment-free, always-available, no-pressure dynamic specifically because it's AI.
**Model:** SFW companion personas. XP Labs is the command center; content operations happen downstream.

---

## The multi-model layout

Each companion persona ("model") lives in its own top-level folder at the repo root. Models share the repo-level infrastructure but hold their own audience intel, niches, platform playbooks, monetization, scripts, campaigns, and synthesis.

```
XP Labs/
├── CLAUDE.md                       # ← THIS FILE (shared system guide)
├── CLIENT_INFO.md                  # Shared quick reference
├── .claude/                        # SHARED — commands, skills, agents
│   ├── commands/                   # /ingest, /build-companion, etc. — all model-aware
│   ├── skills/                     # Domain doctrine
│   └── agents/                     # Ingestion agent etc.
├── templates/                      # SHARED — node and doc templates
├── _system/                        # SHARED — knowledge graph config
│   └── knowledge_graph/
│       ├── taxonomy.yaml           # One canonical taxonomy across all models
│       └── ontology.yaml           # One canonical relationship vocabulary
├── notes/                          # SHARED — raw ingest source material (canvas.md, etc.)
│
├── <model-name-1>/                 # MODEL FOLDER (e.g., ava-laurent/)
│   ├── knowledge_base/             # This model's atomic knowledge
│   │   ├── audience/               # who she targets
│   │   ├── companions/             # her character sheet
│   │   ├── niches/                 # her niche
│   │   ├── platforms/              # her platform playbooks
│   │   ├── monetization/           # her revenue mechanics
│   │   ├── sales-scripts/          # scripts in her voice
│   │   ├── tech-stack/             # model-specific tools
│   │   ├── competitors/            # competitors in her niche space
│   │   └── methodology/            # model-specific doctrine (if any)
│   └── 00_foundation/              # This model's operational layer
│       ├── positioning/
│       ├── strategy/
│       ├── companions/{active,queue,retired}/
│       ├── campaigns/{idea-queue,launched/[YEAR]/[M]/week_N/}/
│       ├── content-playbook/
│       ├── sales-playbook/
│       └── _synthesis/{weekly-sitreps,monthly-reviews}/
│
├── <model-name-2>/                 # Another model, same shape
└── ...
```

**Why shared `_system/`:** the taxonomy and ontology are universal — if one model introduces a validated topic tag, every future model inherits it.

**Why shared `templates/`:** one blueprint set across all models keeps nodes uniform and cross-model queries reliable.

**Why shared `notes/`:** raw source material (masterclasses, research inputs, competitor teardowns) feeds any model. The processed atomic nodes land in the target model's folder.

---

## The AI-disclosure rail (hardcoded into the architecture)

XP Labs commits to **upfront AI-disclosure** as a core product property, not a platform-compliance afterthought. This is enforced structurally:

1. **Every companion character sheet** must contain a non-empty `## AI Disclosure` section with verbatim bio text, verbatim first-DM line, pinned-post/story-highlight description, and verbatim response to "are you real?" A companion without this section **cannot be promoted from `emergent` to `validated`**.
2. **Every platform playbook** must contain an `## AI Disclosure` section specifying how disclosure surfaces on that platform (profile bio, first-interaction surface, pinned/featured content).
3. **`/graph-health`** blocks motion-readiness on these rails — a model with any companion missing disclosure is flagged as `❌ BLOCKING`.

The customer thesis: our users knowingly seek AI companionship. Transparent disclosure is what makes that relationship valid.

---

## Commands (all model-aware)

| Command | Purpose | Model arg |
|---|---|---|
| `/quickstart <model-name>` | Scaffold a new model folder at the repo root | positional |
| `/ingest <file> --model <name>` | Process raw content into a model's knowledge graph | `--model` |
| `/generate-niche --model <name>` | Generate 5 blue-ocean niche candidates for a model | `--model` |
| `/build-companion --model <name>` | Draft the full character sheet (auto-runs `/quickstart` if model folder missing) | `--model` |
| `/write-dm-script --model <name>` | Draft a DM/chat script in her voice | `--model` |
| `/draft-story-arc --model <name>` | Draft a multi-day content+script arc | `--model` |
| `/performance-review --model <name> \| --all` | Per-model sitrep, or iterate all models | `--model` or `--all` |
| `/graph-health --model <name> \| --all` | Per-model graph health + AI-disclosure rail check | `--model` or `--all` |
| `/git-workflow` | Stage, commit, push, open PR | n/a |

Type `/` in Claude Code to see all.

---

## Skills

| Skill | Purpose |
|-------|---------|
| `context-os-basics` | Foundation patterns for the multi-model Context OS |
| `market-research-knowledge-base` | Methodology for mining audience language online |
| `blue-ocean-niche` | Aesthetic × trait × passion framework for niches |
| `companion-building` | Character-sheet doctrine (including the AI-disclosure rail) |
| `dm-script-writing` | Parasocial-first chat-script doctrine |
| `platform-playbooks` | Per-platform doctrine including the AI-disclosure rail |

---

## Quick start for the first model

```
# 1. Seed the knowledge base from the masterclass (shared source)
/ingest notes/canvas.md --model <your-first-model>
# (this auto-scaffolds the model folder if it doesn't exist via /quickstart)

# 2. Generate niche candidates
/generate-niche --model <your-first-model>

# 3. Build the character sheet
/build-companion --model <your-first-model>

# 4. Draft the first story arc
/draft-story-arc --model <your-first-model>

# 5. Draft the intro DM script
/write-dm-script --model <your-first-model>

# 6. Check graph health + AI-disclosure rails
/graph-health --model <your-first-model>
```

---

## Two-layer architecture (per model)

**Layer 1: Atomic knowledge** (`<model>/knowledge_base/`)
- Individual reusable concepts, one per file
- Frontmatter includes `client: xp-labs` and the `<model>` is implicit in the path
- `[[wiki-links]]` between nodes (minimum 3)
- Status: emergent → validated → canonical

**Layer 2: Operational docs** (`<model>/00_foundation/`)
- Strategic artifacts composing Layer 1 nodes
- Positioning, strategy, live companion state, campaigns, synthesis
- Reference atomic concepts — don't redefine them

---

## Quality standards

### Every knowledge node must have
1. Frontmatter with `client: xp-labs`
2. Minimum 3 `[[wiki-links]]`
3. Source attribution: `[VERIFIED: source]`, `[INFERRED: logic]`, or `[UNVERIFIABLE]`
4. Status: emergent → validated → canonical
5. Topics from shared `_system/knowledge_graph/taxonomy.yaml`

### Every companion character sheet must have
1. Concrete Look/Appearance (passes "50 consistent reference images" test)
2. Personality Traits with underlying tension
3. Backstory at D&D-character-sheet depth
4. Chat Tone Guide specific enough for chatter handoff
5. **AI Disclosure section (BLOCKING)** — see rail above
6. Links to: niche, target audience, platforms, monetization mechanics, scripts

### Every campaign log must have
1. Date-aware location (`<model>/00_foundation/campaigns/launched/[YEAR]/[M]/week_N/`)
2. Wiki-links to the companion, scripts, and monetization mechanics used
3. Metrics (followers, subs, PPV revenue, DM conversion, tips)
4. Clear hypothesis and outcome

---

## Ethical guardrails (enforced structurally where possible)

- **SFW only.** No explicit images or videos.
- **Upfront AI-disclosure.** Enforced by the architecture via required sections in companion + platform nodes, checked by `/graph-health`.
- **No targeting of acute crisis signals.** Any script-trigger hitting self-harm / suicidal / abusive-situation signals routes to a resource link, not a PPV.
- **No subscriber-data exfiltration.** DMs stay on-platform.

These live in full form at `<model>/00_foundation/positioning/ethical-guardrails.md` when a model is scaffolded.

---

## Templates (shared at repo root)

- `node_template.md` — generic knowledge node
- `companion-node-template.md` — character sheet with AI-disclosure rail
- `audience-segment-template.md` / `audience-pain-template.md`
- `niche-template.md`
- `script-template.md`
- `platform-playbook-template.md` — with AI-disclosure rail
- `monetization-template.md`
- `tool-template.md`
- `sitrep-week-template.md` / `monthly-review-template.md`
- `strategic-synthesis-template.md`

---

## System maintenance

### Temporary file cleanup
After completing tasks, remove: `tmpclaude-*`, `*.tmp`, `*~`, `.DS_Store`

### Pre-push checklist
| Change | File to update |
|---|---|
| New/removed command | This `CLAUDE.md` — Commands table |
| New/removed skill | This `CLAUDE.md` — Skills table |
| New knowledge node type | `_system/knowledge_graph/taxonomy.yaml` |
| Structure change | This `CLAUDE.md` — Directory Structure |
| New model onboarded | Add to `CLIENT_INFO.md` under "Active models" |

---

**Pivoted:** 2026-04-20 — from PhraseMine B2B-SaaS shape → companion-persona motion
**Restructured:** 2026-04-20 — single-model → multi-model layout with AI-disclosure rail
**Architecture:** Two-layer Context OS (atomic + operational), per-model isolation, shared infrastructure
