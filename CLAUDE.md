# XP Labs — Marketing & GTM Context OS

**This is XP Labs's marketing and go-to-market system** — a Context Operating System where AI compounds intelligence about XP Labs's audience, campaigns, and positioning over time.

**Product:** XP Labs — AI-Powered Customer Language Research from Reddit
**Audience:** Copywriters and Marketing Professionals
**Industry:** B2B SaaS

---

## What Is This?

A **self-contained knowledge system** where:
- AI compounds intelligence about XP Labs's audience and campaigns over time
- Campaign learnings become institutional knowledge
- Knowledge persists and improves with each interaction
- Audience intelligence (what copywriters experience, feel, struggle with) informs every campaign

**Philosophy:** Every campaign makes the system smarter. Research → Campaigns → Learnings → Better Campaigns.

---

## Directory Structure

```
xp-labs/
├── CLAUDE.md                           # ← YOU ARE HERE (System guide)
├── CLIENT_INFO.md                      # Quick reference (contacts, stats)
├── .claude/                            # System infrastructure
│   ├── commands/                       # Slash commands (/ingest, /write-campaign, etc.)
│   ├── skills/                         # Domain expertise knowledge bases
│   └── agents/                         # Autonomous agent definitions
├── templates/                          # File templates for all node types
├── knowledge_base/                     # Layer 1: Atomic Knowledge
│   ├── technical/                      # Product features, capabilities (15 nodes)
│   ├── business/                       # ICPs, pain points, value props, audience intel (50 nodes)
│   ├── methodology/                    # Objection handling, email patterns (6 nodes)
│   └── list-building/                  # Prospect lists, title vetting (GITIGNORED — local only)
├── 00_foundation/                      # Layer 2: Operational Docs
│   ├── positioning/                    # Market positioning
│   ├── messaging/
│   │   ├── idea-queue/                 # Campaign ideas backlog
│   │   ├── front-end-offers/           # Lead magnets and offers
│   │   ├── offer-inventory/            # Offer tracking and performance
│   │   ├── email-voice-and-tone.md     # Writing style guide
│   │   ├── active-campaigns.md         # Currently active campaigns
│   │   ├── inactive-campaigns.md       # Killed/paused campaigns
│   │   ├── copy-drafts.md              # Draft staging area
│   │   └── launched campaigns/         # Date-aware campaign logs
│   │       └── [YEAR]/[Month]/week_N/
│   └── _synthesis/
│       ├── strategic-synthesis.md      # High-level insights
│       ├── weekly-sitreps/             # Weekly campaign sit-reps
│       └── monthly-reviews/            # Monthly pattern analysis
└── _system/
    └── knowledge_graph/
        ├── taxonomy.yaml               # Blessed tags
        └── ontology.yaml               # Relationship rules
```

---

## Commands

| Command | Purpose |
|---------|---------|
| `/ingest` | Process raw content into XP Labs's knowledge graph |
| `/ingest-expertise` | Ingest domain expertise into XP Labs's methodology knowledge base |
| `/generate-campaign-ideas` | Generate cold email campaign ideas based on knowledge base |
| `/write-campaign` | Write campaign copy from an approved idea |
| `/cold-email-review` | Review weekly campaign performance and update synthesis |
| `/generate-offer-inventory` | Generate offer inventory from knowledge base |
| `/create-lead-magnet` | Create a lead magnet or front-end offer asset |
| `/graph-health` | Check knowledge graph health and get recommendations |
| `/quickstart` | Rebuild or reset XP Labs's directory structure |

**Tip:** Type `/` to see all available commands in Claude Code.

---

## Skills

### Context OS & Strategy

| Skill | Purpose |
|-------|---------|
| `context-os-basics` | Foundation patterns for the Context OS architecture |
| `cold-email-domain-expert-knowledge-base` | Cold email expertise — copywriting, strategy, metrics, list-building |
| `market-research-knowledge-base` | How to find and mine real-world audience language online |
| `email-format-writers` | Cold email format patterns (poke-the-bear, one-liner, front-end offer, bet-on-yourself) |
| `offer-generation` | Lead magnet and front-end offer creation |

### Prospect List Preparation

| Skill | Purpose |
|-------|---------|
| `csv-contact-normalizer` | Normalize first names and company names in prospect CSVs |
| `job-title-vetting` | Two-gate (seniority + persona) job title classification |
| `dud-removal-process` | Remove wrong contacts by cross-referencing database data with LinkedIn enrichment |
| `list-building-flow` | End-to-end list-building pipeline (pull, enrich, normalize, dud removal, format) |
| `list-export-formatter` | Reformat finalized lead lists into delivery-ready xlsx |

---

## Knowledge Base Overview

### Business Domain (50 nodes)

**ICP Segments (7):** Freelance copywriters, copywriting agencies, content marketing agencies, SaaS companies, DTC ecommerce brands, health/wellness brands, AI content operations

**Personas (7):** Freelance copywriter, agency copywriter, content marketer, founder (marketing-focused), head of marketing, SaaS marketer, AI prompt engineer

**Pain Points (6 product-level):** Manual research time, unorganized research, disposable research, limited query angles, no customer language, generic AI copy

**Audience Intelligence (21 nodes):** Deep audience psychology sourced from copywriter surveys and email subscriber data:
- **Root pain:** Confidence crisis / imposter syndrome (the #1 pain)
- **Research pains:** Data quality anxiety, completeness uncertainty, vulnerability fear, translating research to copy, source drought
- **Identity pains:** Authentic voice fear, AI threat anxiety, creative envy, explaining copywriting to outsiders, pricing confidence gap
- **Career patterns:** Upwork to first $10K, newbie outreach mistakes, non-native challenges, course-buying behavior, other courses failed
- **Aspirations:** Research framework, client-facing confidence, freelancer-to-business transition
- **Mindset:** Craft pride, client discount negotiations

**Value Props (5):** Exact phrases, real conversations, compounding library, awareness-stage organization, messaging matrix

**Competitors (4):** Manual research, SparkToro, social listening tools, Reddit monitoring tools

### Technical Domain (15 nodes)
Product features: three-tier pipeline, theme extraction, awareness-stage classification, voice profiles, saturation analysis, credit system, bookmarks, data export, quick mode, workspace collaboration, and more.

### Methodology Domain (6 nodes)
Objection handling: AI copy good enough, already use social listening, can search Reddit myself, different from ChatGPT, not for Reddit audiences, too expensive.

---

## Quick Start

### Process New Content
```
"Process this onboarding doc into the knowledge base"
/ingest [file]
```

### Generate Campaign Ideas
```
"Generate 5 cold email campaign ideas"
/generate-campaign-ideas
```

### Write Campaign Copy
```
"Write campaign copy for idea #3 from the queue"
/write-campaign
```

### Review Campaign Performance
```
"Review this week's campaign performance"
/cold-email-review
```

### Check Knowledge Health
```
/graph-health
```

---

## Knowledge Compounding Cycle

```
Raw Content (onboarding docs, audience research, campaign data)
    ↓
Knowledge Base (ICPs, pain points, audience intel, product features)
    ↓
Campaign Ideas (powered by knowledge)
    ↓
Launched Campaigns (with performance data)
    ↓
Weekly Sit-Reps (tactical insights)
    ↓
Monthly Reviews (strategic patterns)
    ↓
Updated Knowledge (emergent → validated → canonical)
    ↓
Better Future Campaigns (compound effect)
```

---

## Two-Layer Architecture

**Layer 1: Atomic Knowledge** (`knowledge_base/`)
- Individual reusable concepts (one per file)
- Structured with frontmatter metadata
- Linked via `[[wiki-links]]`
- Status lifecycle: emergent → validated → canonical

**Layer 2: Operational Docs** (`00_foundation/`)
- Strategic documents that compose Layer 1 concepts
- Positioning, messaging, campaign tracking
- Reference atomic concepts, don't redefine them

---

## XP Labs's Core Positioning

**The Confidence Story:** XP Labs's deepest value isn't time savings — it's certainty. The #1 pain copywriters carry is a fundamental lack of confidence in their research. XP Labs delivers systematic, exhaustive research that replaces fear with evidence.

**Key Campaign Hooks:**
- Confidence crisis → "The real reason research takes so long isn't the mechanics. It's that you don't trust what you've found."
- Authentic voice fear → "Stop sounding like a copywriter. Start sounding like your market."
- Other courses failed → "You've taken the courses. You know the theory. You need a tool, not more theory."
- AI threat → "AI can write. It can't research. That's your moat."
- Research framework aspiration → "XP Labs IS the framework."

**Core Differentiators:**
- Three-pass research methodology (broad → focused → edge cases)
- Full thread conversations, not snippets
- Automatic theme organization and awareness-stage tagging
- Saturation analysis to tell you when you're done
- Voice profile generation capturing audience language patterns

---

## Quality Standards

### Every Knowledge Node Must Have:
1. **Frontmatter with `client: xp-labs`**
2. **Minimum 3 links** to other nodes (per ontology.yaml)
3. **Source attribution** using `[VERIFIED: source]`, `[INFERRED: logic]`, or `[UNVERIFIABLE]`
4. **Status**: emergent → validated → canonical
5. **Topics** from taxonomy.yaml

### Campaign Logs Must Have:
1. **Date-aware location** (correct year/month/week folder)
2. **Wiki-links** to knowledge nodes (ICP, pain points, offers)
3. **Metrics** when available (open rate, reply rate, meetings)
4. **Clear angle/hook** description

---

## AI Efficiency Tips

### Fast Lookups:
- **Quick overview**: Read `CLIENT_INFO.md`
- **Strategic summary**: Read `00_foundation/_synthesis/strategic-synthesis.md`
- **All offers**: Read `00_foundation/messaging/front-end-offers/front-end-offers.md`
- **Voice guidelines**: Read `00_foundation/messaging/email-voice-and-tone.md`

### Deep Research:
- **ICP analysis**: Read all `knowledge_base/business/icp-*.md`
- **Audience psychology**: Read all `knowledge_base/business/audience-*.md`
- **Pain points**: Read all `knowledge_base/business/pain-point-*.md`
- **Product capabilities**: Read all `knowledge_base/technical/product-*.md`

---

## Gitignored Folders

- `knowledge_base/list-building/` — Prospect lists, CSV exports, title vetting work files. Too large and iterative for git.

---

## Templates

All file templates are in `templates/`. Key templates:
- `node_template.md` — Generic knowledge node
- `icp-node-template.md` — ICP node format
- `persona-node-template.md` — Persona node format
- `sitrep-week-template.md` — Weekly sit-rep format
- `monthly-review-template.md` — Monthly review format
- `campaigns-week-template.md` — Weekly campaign log
- `offer-inventory-template.md` — Offer inventory tracker

---

## System Maintenance

### Temporary File Cleanup
After completing tasks, scan for and delete: `tmpclaude-*`, `*.tmp`, `*~`, `.DS_Store`

### Pre-Push Documentation Checklist
| Change | Files to update |
|--------|----------------|
| New/removed command | This `CLAUDE.md` — Commands table |
| New/removed skill | This `CLAUDE.md` — Skills table |
| New knowledge node type | This `CLAUDE.md` — Knowledge Base Overview |
| Structure change | This `CLAUDE.md` — Directory Structure |

---

**Created:** 2026-04-13
**System:** XP Labs Marketing & GTM Context OS
**Architecture:** Two-layer (atomic knowledge + operational docs) with compounding intelligence
