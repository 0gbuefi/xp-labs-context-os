---
name: context-os-basics
description: Foundation patterns for XP Labs's context operating system
model: inherit
---

# Context OS Basics — XP Labs Edition

## What is a Context OS?

A context operating system is a structured knowledge system where:
- AI compounds intelligence over time (never re-teach)
- Knowledge persists across sessions
- Concepts link to each other (graph, not files)
- Two layers separate reusable knowledge from operational docs

**For XP Labs:** a Context OS where knowledge about our audience (men seeking companionship), our companion personas, our niches, our platforms, our scripts, and our campaign results compounds over time to power an increasingly effective companion-persona operation.

---

## System Architecture (multi-model)

The repo hosts multiple models (companion personas). Infrastructure is shared at the repo root; each model has its own isolated knowledge + operational layers.

```
xp-labs/
├── CLAUDE.md                              # Shared system guide
├── CLIENT_INFO.md                         # Shared quick reference
├── .claude/                               # SHARED
│   ├── agents/                            # Reusable agents (ingestion, etc.)
│   ├── commands/                          # All commands are model-aware (--model arg)
│   └── skills/                            # Including this one
├── templates/                             # SHARED — node templates
├── _system/                               # SHARED
│   └── knowledge_graph/
│       ├── taxonomy.yaml                  # Canonical tags across all models
│       └── ontology.yaml                  # Canonical relationship rules
├── notes/                                 # SHARED — raw ingest source material (canvas.md, etc.)
│
├── <model-name>/                          # Per-model workspace
│   ├── knowledge_base/                    # Layer 1: Atomic Knowledge for this model
│   │   ├── audience/                      # who she targets
│   │   ├── companions/                    # her character sheet (with AI-disclosure rail)
│   │   ├── niches/                        # her niche
│   │   ├── platforms/                     # her platform playbooks (with AI-disclosure rail)
│   │   ├── monetization/                  # her revenue mechanics
│   │   ├── sales-scripts/                 # scripts in her voice
│   │   ├── tech-stack/                    # model-specific tools
│   │   ├── competitors/                   # competitors in her niche space
│   │   └── methodology/                   # model-specific doctrine
│   └── 00_foundation/                     # Layer 2: Operational Docs for this model
│       ├── positioning/
│       ├── strategy/
│       ├── companions/{active,queue,retired}/
│       ├── campaigns/{idea-queue,launched/[YEAR]/[M]/week_N}/
│       ├── content-playbook/
│       ├── sales-playbook/
│       └── _synthesis/{weekly-sitreps,monthly-reviews}/
│
└── <other-model-name>/                    # Another model, same shape
```

**Shared vs per-model:**
- Shared: `_system/` (taxonomy + ontology), `templates/`, `.claude/`, `notes/`, root docs
- Per-model: everything under `<model-name>/`

---

## The Two-Layer Architecture

### Layer 1: Atomic Knowledge (`knowledge_base/`)

Individual reusable concepts — one per file. Each node:
- Has structured frontmatter (name, description, domain, node_type, status, client, topics, related_concepts)
- Links to related concepts via `[[wiki-links]]` (minimum 3 per node)
- Follows the lifecycle: **emergent → validated → canonical**
- Includes source attribution: `[VERIFIED: source]`, `[INFERRED: logic]`, `[UNVERIFIABLE]`
- **MUST include** `client: xp-labs`

### Layer 2: Operational Docs (`00_foundation/`)

Strategic and operational artifacts that **compose** Layer 1 atomic nodes:
- Positioning, strategy, content playbook, sales playbook
- The live companion roster (active/queue/retired)
- Campaign idea queue and dated launched-campaign logs
- Synthesis (weekly sitreps, monthly reviews)

Operational docs **reference** atomic concepts. They should not re-define them.

---

## Constitutional Documents

### `_system/knowledge_graph/taxonomy.yaml`
Blessed tags for the XP Labs companionship motion:
- **Domains:** audience, companion, niche, platform, monetization, sales-scripts, tech-stack, competitors, methodology, emergent
- **Node types:** concept, pattern, case-study, framework, persona, segment, niche, script, playbook, tool, competitor
- **Status values:** emergent, validated, canonical
- **Topic library** — see the YAML file for the canonical list

Start small. Add new tags only after 3+ nodes demonstrate need. `/graph-health` flags tag sprawl.

### `_system/knowledge_graph/ontology.yaml`
Relationship types that nodes use to link:
- `enables` / `supports` / `implements`
- `targets` (companion/niche/script → audience-segment)
- `distributed-via` (companion → platform)
- `monetized-by` (companion → monetization-mechanic)
- `derived-from` (niche/script → pain/desire)
- `used-by` (script/tool → companion)
- `competes-with` (our motion → competitor)
- `scales-from` (companion-v2 → companion-v1)

Minimum 3 links per node.

---

## Workflow Patterns (all model-aware)

Every content-producing command takes `--model <name>`. `/quickstart` takes the model name positionally.

### Scaffold a new model
```
/quickstart <model-name>
→ Creates <model-name>/knowledge_base/ and <model-name>/00_foundation/ subtrees
→ Date-aware campaigns folder for current year/month
→ READMEs in every subfolder
```

### Process new content
```
/ingest <file> --model <name>
→ Extracts audience/niche/script/platform/etc. signals
→ Creates atomic nodes under <name>/knowledge_base/
→ Links to existing nodes
→ Flags taxonomy drift
```

### Generate a niche for a model
```
/generate-niche --model <name>
→ Reads audience intel + existing niches + competitors for this model
→ Proposes 5 candidates in the aesthetic × trait × passion frame
→ Offers to save the top pick as <name>/knowledge_base/niches/
```

### Build a companion from a niche
```
/build-companion --model <name>
→ Auto-runs /quickstart if the model folder doesn't exist
→ Reads the niche + audience
→ Drafts the full character sheet including the AI-disclosure rail
→ Saves to <name>/knowledge_base/companions/
→ Creates a queue entry in <name>/00_foundation/companions/queue/
```

### Draft chat scripts
```
/write-dm-script --model <name>
→ Reads companion voice + methodology doctrine + audience pain
→ Produces a ready-to-use intro/escalation/re-engagement/VIP/mass-DM script
→ Links back to companion and pain nodes
```

### Run a multi-day story arc
```
/draft-story-arc --model <name>
→ 3/7/12-day scenario arc with content + story + DM + cliffhanger per day
→ Maps to the model's monetization price ladder
→ Enumerates content assets grouped by generation batch
```

### Performance review
```
/performance-review --model <name>     # one model
/performance-review --all              # iterate every model folder
→ Pulls metrics per companion
→ Writes sitrep to <name>/00_foundation/_synthesis/weekly-sitreps/
→ Promotes nodes emergent → validated based on evidence
→ Flags stale nodes
```

### Graph health
```
/graph-health --model <name>           # one model
/graph-health --all                    # iterate every model folder
→ Tag sprawl %, orphan nodes, broken links, aging emergent nodes
→ Motion-readiness checklist
→ AI-disclosure rail check (BLOCKING — companions + platforms must have the section)
→ Top 3 recommendations
```

---

## Knowledge Lifecycle

**Emergent** — just discovered, hypothesis
**Validated** — used in 2+ campaigns/companions with positive signal
**Canonical** — referenced 5+ times, foundation for other concepts

Example progression:
- Week 1: `[[script-intro-backyard]]` — emergent (drafted from canvas.md masterclass pattern)
- Week 4: same node → validated (used by 2 companions, conversion confirmed)
- Month 3: same node → canonical (used by 5+ companions across niches)

The `/performance-review` command does the promotions.

---

## Evidence-Based Attribution

Every claim needs a source:
- **[VERIFIED: source:location]** — direct evidence (transcript line, screenshot, metric)
- **[INFERRED: logic]** — deduced from evidence
- **[UNVERIFIABLE]** — honest that we can't confirm

If you can't cite a source, don't claim it.

---

## Key Anti-Patterns

1. **Context explosion** — "need to read every file to answer this". Fix: use synthesis docs, scan frontmatter.
2. **Missing client attribution** — frontmatter lacks `client: xp-labs`. Fix: enforce at ingestion.
3. **Vague attribution** — "scripts are working". Fix: quantify (e.g., "23% conversion across 47 sends").
4. **Over-creating nodes** — a node per sentence. Fix: one concept per node, minimum 3 links, concrete example required.
5. **Tag sprawl** — 60+ tags with no consistency. Fix: use blessed taxonomy; `/graph-health` warns.
6. **Vibes-based companion sheets** — "she's cool and mysterious". Fix: concrete traits with underlying tension; pass the "ghost-writer can operate her" test.

---

## The 3–5 Sample Rule

Never automate without sampling first:
1. Run broad search
2. Sample 3–5 examples with context
3. Validate patterns are accurate
4. Refine and scale

For scripts: test 3–5 variations before promoting one to canonical. Sample replies to validate the angle.

---

## XP Labs Cadence

### Weekly
- Post content per companion
- Run DMs (or chatters do)
- Log campaigns launched
- Run `/performance-review` → sitrep

### Monthly
- Synthesize 4 weeks of sitreps into a monthly review
- Update `00_foundation/_synthesis/strategic-synthesis.md` with canonical insights
- Kill underperforming companions; plan next quarter's new companions

### Knowledge compounding loop
```
Campaign launch → Performance data → Weekly sitrep → Monthly review
    → Validated knowledge nodes → Better next campaign
```

---

## Quick Reference

- **Ingest content:** `/ingest [file]`
- **Find a niche:** `/generate-niche`
- **Build a companion:** `/build-companion`
- **Draft a script:** `/write-dm-script`
- **Draft a multi-day arc:** `/draft-story-arc`
- **Weekly review:** `/performance-review`
- **Graph health:** `/graph-health`
- **Reset structure:** `/quickstart`
