# XP Labs - AI Navigation Guide

**Purpose:** Context Operating System for XP Labs's cold email campaigns ([Industry] - [Sub-Industry] targeting [Target Market]).

---

## What Is This?

This is **XP Labs's isolated Context OS** within the single-product system where:
- AI compounds intelligence about XP Labs over time
- Campaign learnings become institutional knowledge
- Knowledge persists and improves with each interaction
- All context is specific to XP Labs (no data integrity issues with other clients)

**Client:** XP Labs
**Industry:** [Industry]
**Sub-Industry:** [Sub-Industry]
**Slug:** `xp-labs`

---

## Directory Structure

```
xp-labs/
├── CLAUDE.md                           # ← YOU ARE HERE (Navigation guide)
├── CLIENT_INFO.md                      # Quick reference (contacts, stats)
├── knowledge_base/                     # Layer 1: Atomic Knowledge
│   ├── technical/                      # Services, capabilities, frameworks
│   ├── business/                       # ICPs, pain points, value props, competitors
│   ├── methodology/                    # Email patterns, outreach frameworks
│   └── list-building/                  # Prospect lists, title vetting (GITIGNORED — local only)
├── 00_foundation/                      # Layer 2: Operational Docs
│   ├── positioning/                    # Market positioning
│   ├── messaging/
│   │   ├── idea-queue/                 # Campaign ideas folder
│   │   │   └── idea-queue.md           # Campaign ideas backlog
│   │   ├── front-end-offers/           # Front-end offers folder
│   │   │   └── front-end-offers.md     # Lead magnets and offers
│   │   ├── email-voice-and-tone.md     # Writing style guide
│   │   ├── active-campaigns.md         # Currently active campaigns
│   │   ├── inactive-campaigns.md       # Killed/paused campaigns
│   │   └── launched campaigns/         # Date-aware campaign logs
│   │       └── [YEAR]/[Month]/
│   │           ├── week_1/
│   │           ├── week_2/
│   │           ├── week_3/
│   │           ├── week_4/
│   │           └── week_5/ (if applicable)
│   └── _synthesis/
│       ├── strategic-synthesis.md      # High-level insights
│       ├── weekly-sitreps/             # Weekly campaign sit-reps
│       └── monthly-reviews/            # Monthly pattern analysis
└── _system/
    └── knowledge_graph/
        ├── taxonomy.yaml               # Blessed tags for this client
        └── ontology.yaml               # Relationship rules
```

---

## Quick Reference Tasks

### 1. Generate Campaign Ideas for XP Labs
```
"Generate 5 cold email campaign ideas for xp-labs"
```

**What AI should do:**
1. Read `knowledge_base/business/icp-*.md` to understand target audience
2. Read `knowledge_base/business/pain-point-*.md` for messaging angles
3. Read `knowledge_base/business/value-prop-*.md` for differentiation
4. Read `00_foundation/messaging/front-end-offers/front-end-offers.md` for offers to use
5. Read `00_foundation/messaging/email-voice-and-tone.md` for style
6. Generate ideas that combine: ICP + Pain Point + Value Prop + Offer
7. Add to `00_foundation/messaging/idea-queue/idea-queue.md`

### 2. Log a Campaign Launch
```
"Log this campaign for xp-labs: [campaign details]"
```

**What AI should do:**
1. Identify current week (e.g., Week 3 of January 2026)
2. Navigate to: `00_foundation/messaging/launched campaigns/[YEAR]/[MONTH]/week_N/`
3. Open: `launched_campaigns_week_N_[month]_[year].md`
4. Add campaign entry with:
   - Campaign name and angle
   - Target ICP: [[icp-link]]
   - Pain point addressed: [[pain-point-link]]
   - Offer used: [[offer-link]]
   - Launch date and initial metrics
5. Link to relevant knowledge nodes

### 3. Create Weekly Sit-Rep
```
"Create weekly sit-rep for xp-labs with this data: [metrics]"
```

**What AI should do:**
1. Read the week's campaigns from `launched campaigns/[year]/[month]/week_N/`
2. Analyze: What worked, what didn't, iterate/ditch/watch decisions
3. Create sit-rep in: `00_foundation/_synthesis/weekly-sitreps/`
4. Update knowledge nodes if learnings warrant it (emergent → validated)
5. Reference specific campaigns with [[wiki-links]]

### 4. Fetch Client Information
```
"What are XP Labs's front-end offers?"
"What's the primary pain point for XP Labs's ICP?"
"Show me XP Labs's email voice guidelines"
```

**What AI should do:**
1. Check `CLIENT_INFO.md` for quick reference
2. For offers: Read `00_foundation/messaging/front-end-offers/front-end-offers.md`
3. For pain points: Read `knowledge_base/business/pain-point-*.md` files
4. For voice: Read `00_foundation/messaging/email-voice-and-tone.md`
5. For comprehensive view: Read `00_foundation/_synthesis/strategic-synthesis.md`

### 5. Check Knowledge Graph Health
```
"Run graph health check for xp-labs"
```

**What AI should do:**
1. Count nodes in each domain (technical, business, methodology)
2. Verify each node has minimum 3 links (per ontology.yaml)
3. Check for orphan nodes (no links)
4. Identify emergent nodes aging past 30 days (need validation)
5. Check for tag sprawl (per taxonomy.yaml thresholds)

---

## Common Workflows

### Workflow 1: New Campaign Angle Discovery
**Trigger:** User asks for campaign ideas

**Steps:**
1. Read ALL ICP nodes to understand target audience deeply
2. Read ALL pain point nodes to find resonant angles
3. Read ALL value prop nodes to understand differentiation
4. Check front-end-offers.md for available offers
5. Review email-voice-and-tone.md for style constraints
6. Review idea-queue.md to avoid duplicates
7. Generate 5-10 ideas combining different pain points + value props
8. Add to idea-queue.md with proper frontmatter

### Workflow 2: Campaign Performance Analysis
**Trigger:** User shares campaign metrics

**Steps:**
1. Locate campaign in launched campaigns/[year]/[month]/week_N/
2. Analyze metrics against benchmarks
3. Identify what worked/didn't work
4. Make iterate/ditch/watch recommendation
5. Update relevant knowledge nodes if insights warrant it
6. Create or update weekly sit-rep

### Workflow 3: Onboarding New Information
**Trigger:** User says "Process [content] into xp-labs knowledge base"

**Steps:**
1. Extract concepts from raw content
2. Identify which domain: technical, business, or methodology
3. Create atomic nodes with proper frontmatter (client: xp-labs)
4. Link to existing nodes (minimum 3 links per ontology)
5. Add proper source attribution [VERIFIED: source]
6. Set status: emergent (new) → validated (proven 1x) → canonical (proven 2+x)
7. Update taxonomy.yaml if new tags needed

---

## Knowledge Base Organization

### Business Domain (`knowledge_base/business/`)
**What goes here:** ICP definitions, pain points, value propositions, competitors

**Common node types:**
- `icp-*.md` - Target audience segments
- `pain-point-*.md` - Problems the client solves for their ICP
- `value-prop-*.md` - Differentiation and competitive advantages
- `competitor-*.md` - Competitive landscape and positioning

**When to add:** New ICP segments discovered, new pain points validated, new competitive intel gathered

### Technical Domain (`knowledge_base/technical/`)
**What goes here:** Services, capabilities, frameworks, technical offerings

**Common node types:**
- `service-*.md` - Service offerings and deliverables
- `framework-*.md` - Methodologies and processes
- `capability-*.md` - Technical capabilities and expertise

**When to add:** New service offerings, new technical capabilities, new frameworks developed

### Methodology Domain (`knowledge_base/methodology/`)
**What goes here:** Email patterns, outreach frameworks, discovery insights, objection handling

**Common node types:**
- `email-pattern-*.md` - Proven email/outreach patterns
- `discovery-insight-*.md` - Patterns from discovery calls
- `objection-*.md` - Common objections and responses
- `framework-*.md` - Process frameworks

**When to add:** New email patterns discovered, objection handling scripts, discovery frameworks

---

## Quality Standards for This Client

### Every Knowledge Node Must Have:
1. **Frontmatter with `client: xp-labs`** (CRITICAL - prevents data integrity issues)
2. **Minimum 3 links** to other nodes (per ontology.yaml)
3. **Source attribution** using [VERIFIED: source], [INFERRED: logic], or [UNVERIFIABLE]
4. **Status**: emergent → validated → canonical
5. **Topics** from taxonomy.yaml (don't create random tags)

### Campaign Logs Must Have:
1. **Date-aware location** (correct year/month/week folder)
2. **Wiki-links** to knowledge nodes (ICP, pain points, offers)
3. **Metrics** when available (open rate, reply rate, meetings)
4. **Clear angle/hook** description

### Voice/Tone Compliance:
Always check `00_foundation/messaging/email-voice-and-tone.md` when generating emails to ensure:
- Consistent brand voice
- Appropriate tone for target audience
- Messaging that aligns with client preferences

---

## Guardrails

### ALWAYS Specify Client:
When working with multiple clients, ALWAYS confirm you're working with `xp-labs` specifically. Never accidentally pull knowledge from other clients.

### NEVER Cross-Contaminate:
- Don't use knowledge from other clients
- Don't reference other client campaigns
- Keep XP Labs knowledge isolated
- Every node must have `client: xp-labs` in frontmatter

### Date-Aware Structure:
- Always use current year/month/week for campaign logs
- Don't create future or past month folders
- Week folders are dynamically calculated per month

### Respect Taxonomy:
- Only use blessed tags from `_system/knowledge_graph/taxonomy.yaml`
- Don't create random tags
- If new tag needed, add to taxonomy first

---

## AI Efficiency Tips

### Fast Lookups:
- **Quick client overview**: Read `CLIENT_INFO.md`
- **Strategic summary**: Read `00_foundation/_synthesis/strategic-synthesis.md`
- **All offers at once**: Read `00_foundation/messaging/front-end-offers/front-end-offers.md`
- **Voice guidelines**: Read `00_foundation/messaging/email-voice-and-tone.md`

### Deep Research:
- **Understand ICP fully**: Read all nodes in `knowledge_base/business/icp-*.md`
- **Pain point analysis**: Read all `pain-point-*.md` nodes
- **Competitive positioning**: Read all `competitor-*.md` nodes
- **Service offerings**: Read all nodes in `knowledge_base/technical/`

### Campaign Work:
- **Generate ideas**: Read ICP + pain points + value props + offers + voice
- **Log campaigns**: Navigate to current week's folder in launched campaigns
- **Create sit-reps**: Read week's campaigns + analyze + synthesize

---

## Special Considerations

### 1. Industry/Niche Expertise Matters
XP Labs may have specialization in specific verticals/niches. When generating campaigns:
- Reference vertical-specific expertise if documented in knowledge base
- Use industry-specific examples from case studies
- Don't be generic - be niche-specific when possible
- Check for patterns across similar client types (if documented)

### 2. Core Differentiators
Identify XP Labs's main competitive advantages from value-prop nodes. When positioning:
- Lead with strongest differentiators
- Reference specific frameworks/methodologies if they exist
- Use proven results/metrics when available
- Differentiate based on knowledge base insights

### 3. Competitor Context
XP Labs competes in a specific landscape. When crafting messaging:
- Review competitor-*.md nodes to understand positioning
- Emphasize differentiation points
- Address common competitive objections
- Position based on unique strengths

### 4. Qualification Criteria
XP Labs may have specific ICP qualification criteria. When outreach:
- Reference minimum requirements if documented
- Use qualifying language to filter prospects
- Don't waste time on out-of-ICP targets
- Check ICP nodes for red flags/disqualifiers

---

## Meta: About This Guide

**Created:** [DATE]
**Client:** XP Labs
**Industry:** [Industry]
**Status:** Active
**Purpose:** AI navigation guide for efficient and safe client knowledge management

**When this changes:**
- New knowledge nodes added → Update node count in CLIENT_INFO.md
- New workflows discovered → Add to Common Workflows
- New quality issues → Add to Guardrails
- Significant learnings → Update Special Considerations

**Questions?** Start with `CLIENT_INFO.md` for basics, then dive into `knowledge_base/` for depth.

---

## How to Use This System

### Finding Information

1. **Start with synthesis docs** - Check `_synthesis/` folders first for high-level insights
2. **Then atomic concepts** - Read specific nodes in `knowledge_base/` for details
3. **Follow wiki-links** - [[concept-name]] links to related ideas

### Adding Information

Process raw content (transcripts, docs, notes):
```
"Process [file] into xp-labs knowledge base"
```

The system will:
- Extract concepts
- Create structured nodes with proper frontmatter
- Link to related concepts (minimum 3 links)
- Set appropriate status (emergent → validated → canonical)

### Checking Health

Run graph health checks:
```
/graph-health xp-labs
```

This checks:
- Tag sprawl (too many unique tags)
- Orphan nodes (nodes with no links)
- Aging emergent concepts (need validation)
- Node count per domain
- Link density

---

**Remember:** This is a single-product system. Always specify `xp-labs` and never cross-contaminate knowledge between clients.
