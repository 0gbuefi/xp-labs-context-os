---
name: context-os-basics
description: Foundation patterns for XP Labs's context operating system
model: inherit
---

# Context OS Basics - XP Labs Edition

## What is a Context OS?

A context operating system is a structured knowledge system where:
- AI compounds intelligence over time (never re-teach)
- Knowledge persists across sessions
- Concepts link to each other (graph, not files)
- Two layers separate reusable knowledge from operational docs

**For XP Labs:** A Context OS where knowledge about XP Labs's product, market, and campaigns compounds over time to power increasingly effective GTM execution.

---

## System Architecture

### Structure

```
xp-labs/
├── .claude/                    # System resources
│   ├── agents/                 # Reusable agents
│   ├── commands/               # Commands
│   └── skills/                 # Skills (like this one)
├── templates/                  # Reusable templates
├── CLIENT_INFO.md              # Quick reference
├── knowledge_base/             # Layer 1: Atomic Knowledge
│   ├── technical/
│   ├── business/
│   └── methodology/
├── 00_foundation/              # Layer 2: Operational Docs
│   ├── positioning/
│   ├── messaging/
│   │   ├── front-end-offers.md
│   │   ├── idea-queue.md
│   │   ├── email-voice-and-tone.md
│   │   └── launched-campaigns/
│   └── _synthesis/
│       ├── weekly-sitreps/
│       ├── monthly-reviews/
│       └── strategic-synthesis.md
└── _system/
    └── knowledge_graph/
        ├── taxonomy.yaml
        └── ontology.yaml
```

### Key Principles

1. **Knowledge Compounding:** Intelligence about XP Labs's market, campaigns, and methodology grows over time
2. **Two-Layer Separation:** Atomic knowledge (reusable concepts) vs operational docs (strategic artifacts)
3. **Evidence-Based:** Every claim traced to a source
4. **Lifecycle Management:** Concepts progress from emergent to validated to canonical

---

## The Two-Layer Architecture

### Layer 1: Atomic Knowledge Graph (knowledge_base/)

Individual reusable concepts:
- **Technical:** Product features, integrations, capabilities
- **Business:** ICPs, pain points, value props, competitors
- **Methodology:** Email patterns, frameworks, objection handling

Each node:
- Has structured frontmatter
- Links to related concepts via [[wiki-links]]
- Follows lifecycle: emergent → validated → canonical
- **MUST include** `client: xp-labs` field

**Example node:**
```yaml
---
name: PAIN_POINT_MANUAL_RESEARCH
client: xp-labs
domain: business
status: validated
related_concepts:
  - "[[icp-copywriters]]"
  - "[[value-prop-automated-language-mining]]"
  - "[[pain-point-manual-reddit-research]]"
---
```

### Layer 2: Operational Documents (00_foundation/)

Strategic artifacts that COMPOSE Layer 1:
- **Positioning:** Market positioning, competitive strategy
- **Messaging:** Email templates, campaign ideas, voice/tone
  - front-end-offers.md: Client's lead magnets/offers
  - idea-queue.md: Campaign ideas waiting to launch
  - launched-campaigns/: Active campaigns tracked weekly
- **Synthesis:** Weekly sit-reps, monthly reviews, strategic insights

Key principle: Operational docs REFERENCE atomic concepts, they don't redefine them.

---

## Constitutional Documents

### taxonomy.yaml

Defines blessed tags for the client's system:
- **Domains:** technical, business, methodology
- **Node types:** concept, pattern, case-study, framework
- **Status values:** emergent, validated, canonical
- **Topic library:** Client-specific tags (customized by industry)

**Industry customization:**
- B2B SaaS: product-features, integrations, pricing
- B2B Services: service-offerings, deliverables, case-studies
- B2B Agency: service-packages, client-results, process

Start small. Add tags only after 3+ nodes demonstrate need.

### ontology.yaml

Defines how concepts relate:
- **Relationship types:** enables, supports, implements, addresses
- **Linking requirements:** Minimum 3 links per node
- **Quality thresholds:** Tag sprawl, orphan nodes

---

## Workflow Patterns

### Processing Content
```
"Process [file] into knowledge base"
→ Extracts concepts
→ Creates nodes in knowledge_base/
→ Links to existing nodes
```

### Generating Campaign Ideas
```
"Generate cold email ideas"
→ Reads knowledge_base/
→ Identifies pain points + ICPs
→ Creates campaign angles
→ Adds to idea-queue.md
```

### Launching Campaigns
```
"Log this campaign"
→ Creates entry in launched-campaigns/YYYY/Month/week-N/
→ References knowledge nodes
→ Tracks performance metrics
```

### Weekly Sit-Reps
```
"Create weekly sit-rep"
→ Analyzes campaign performance
→ Makes iterate/ditch/watch decisions
→ Updates knowledge nodes based on learnings
```

---

## Evidence-Based Attribution

Every claim needs a source:

- **[VERIFIED: source]** - Direct evidence from documents
- **[INFERRED: reasoning]** - Deduced from evidence
- **[UNVERIFIABLE]** - Cannot confirm (be honest)

Quality standard: If you can't cite a source, don't claim it.

**For XP Labs:**
- Source onboarding docs and product materials
- Source campaign performance data
- Source discovery call transcripts
- Source competitor research

---

## Knowledge Lifecycle

### Emergent → Validated → Canonical

**Emergent:**
- Just discovered from content
- Used in 0-1 campaigns
- Hypothesis, not proven

**Validated:**
- Seen in 2-3+ sources
- Used in actual campaigns
- Proven to work

**Canonical:**
- Referenced 5+ times
- Core to client's strategy
- Foundation for other concepts

**Example progression:**
```
Week 1: [[pain-point-data-silos]] - emergent
        (extracted from onboarding doc)

Week 4: [[pain-point-data-silos]] - validated
        (used in 3 campaigns, resonates with ICP)

Month 3: [[pain-point-data-silos]] - canonical
        (referenced in 12 campaigns, 8 synthesis docs)
```

---

## Campaign-Focused Knowledge Patterns

For XP Labs's B2B SaaS GTM context:

### Business Knowledge:
- **ICPs:** Who we target (enterprise SaaS, agencies, etc.)
- **Pain Points:** What hooks resonate ("15 hours/week wasted")
- **Value Props:** How client solves problems
- **Competitors:** Who we compete against, positioning angles
- **Use Cases:** Specific scenarios that work

### Methodology Knowledge:
- **Email Patterns:** What subject lines work ("Question?" format)
- **Campaign Frameworks:** Repeatable structures (pain-first, ROI-later)
- **Objection Handling:** Responses to common pushback
- **Discovery Insights:** What to look for in prospects

### Technical Knowledge:
- **Product Features:** What enables the value prop
- **Integrations:** Technical capabilities that differentiate
- **Service Offerings:** For service/agency clients

---

## Key Anti-Patterns

### 1. Context Explosion
**Problem:** "Need to read all files to answer this"
**Fix:** Use synthesis docs (weekly sit-reps, monthly reviews)

### 2. Missing Client Attribution
**Problem:** Knowledge nodes lack proper attribution
**Fix:** Always include `client: xp-labs` in frontmatter

### 3. Vague Attribution
**Problem:** "Campaigns are working" (no data)
**Fix:** Quantify everything: "3 of 5 campaigns (60% reply rate)"

### 4. Over-Generating Nodes
**Problem:** Creating nodes for every sentence
**Fix:** One clear concept per node, minimum 3 links

### 5. Tag Sprawl
**Problem:** 47 different tags, no consistency
**Fix:** Use blessed taxonomy, consolidate similar tags

---

## The 3-5 Sample Rule

Never automate without sampling first:
1. Run broad search
2. Sample 3-5 results with context
3. Validate patterns are accurate
4. Refine and scale

**For campaigns:**
- Don't assume pain point resonates across all prospects
- Test 3-5 variations before scaling
- Sample responses to validate angle

---

## XP Labs GTM Patterns

### Weekly Cadence:
- Launch campaigns (logged in launched-campaigns/)
- Track performance
- Create weekly sit-rep
- Iterate/ditch/watch decisions

### Monthly Cadence:
- Synthesize 4 weeks of data
- Identify patterns (what works, what doesn't)
- Update knowledge nodes (emergent → validated)
- Create monthly review
- Update strategic synthesis

### Knowledge Compounding:
```
Campaign Launch
    ↓
Performance Data
    ↓
Weekly Sit-Rep (tactical insights)
    ↓
Monthly Review (strategic patterns)
    ↓
Knowledge Nodes (validated concepts)
    ↓
Future Campaign Ideas (powered by knowledge)
```

---

## Advanced Patterns (Not Covered Here)

For complex implementations:
- Automated campaign performance tracking
- Chief of Staff orchestration
- Team governance patterns (multiple contributors)
- Enterprise taxonomy design

These require customization for your specific context.
Learn more: https://taste.systems

---

## Quick Reference

**Ingest content:** `"Process [file] into knowledge base"`
**Check health:** `/graph-health`
**Generate ideas:** `"Generate cold email ideas"`
