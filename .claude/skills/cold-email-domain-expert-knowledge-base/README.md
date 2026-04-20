# Cold Email Domain Expert Knowledge Base

**XP Labs's Cold Email Expertise Repository**

---

## What Is This?

This is your **institutional knowledge base** for cold email methodology — separate from XP Labs-specific product/market knowledge.

**Think of it as:**
- Your cold email playbook
- Pattern library built from best content (videos, articles, case studies)
- Expertise that compounds over time
- Reference guide for all agents working on client campaigns

**Not this:**
- XP Labs-specific product/market info (that goes in `knowledge_base/`)
- Generic tips (only specific, actionable patterns)
- Aspirational knowledge (only what you've actually ingested and validated)

---

## Why This Exists

### The Problem
Every cold email operation has expertise scattered across:
- Expert YouTube channels you follow
- Articles bookmarked but never referenced
- Case studies saved somewhere
- Lessons learned but forgotten
- Individual team members' heads

### The Solution
**One central knowledge base that:**
1. Stores expertise as atomic, linked concepts
2. Gets queried by agents when helping clients
3. Compounds intelligence over time
4. Becomes XP Labs's competitive advantage in outbound

---

## Structure

```
cold-email-domain-expert-knowledge-base/
├── README.md                   # This file
├── SKILL.md                    # How agents use this KB
├── canvas.md                   # Staging area for new content
├── knowledge_base/             # All expertise nodes
│   ├── campaign-strategy/      # Campaign ideation, offers, angles
│   ├── copywriting/            # Subject lines, CTAs, structure
│   ├── icp-research/           # ICP definition, pain points
│   ├── metrics-analysis/       # Open rates, reply rates, diagnostics
│   ├── iteration-signals/      # When to iterate/ditch/optimize
│   └── list-building/          # Sourcing, hygiene, segmentation
└── _system/
    ├── taxonomy.yaml           # Blessed tags/categories
    ├── ontology.yaml           # How concepts relate
    └── TAXONOMY-MAINTENANCE.md # How to evolve taxonomy
```

---

## Quick Start

### Adding Expertise (You)

1. **Find valuable content:**
   - YouTube video about cold email
   - Article on subject line patterns
   - Case study with real metrics
   - Book chapter on campaign strategy

2. **Get the text:**
   - Video → copy YouTube transcript
   - Article → copy full article text
   - Book → copy chapter

3. **Paste into canvas:**
   ```
   Open: canvas.md
   Paste full content
   Save
   ```

4. **Run ingestion:**
   ```
   /ingest-expertise
   ```

5. **AI processes it:**
   - Extracts key concepts
   - Creates atomic knowledge nodes
   - Links related concepts
   - Tags with taxonomy
   - Reports what was created

6. **Review & refine:**
   - Check created nodes
   - Fix any links
   - Review at milestones (every 25 nodes)

### Querying Expertise (Agents)

When working on client campaigns, agents query this KB:

**Examples:**
```
"What does cold email KB say about subject lines?"
→ Reads all subject line nodes, synthesizes patterns

"How do I know when to iterate vs ditch a campaign?"
→ Reads iteration-signals/ nodes, provides criteria

"What are proven campaign frameworks?"
→ Reads campaign-strategy/ nodes, lists frameworks
```

**Integration with client work:**
- XP Labs KB (`knowledge_base/`) = WHAT to say (ICPs, pain points)
- Domain Expert KB = HOW to say it (proven patterns)
- Combined = Customized campaign with expert methodology

---

## How It Works

### Knowledge Lifecycle

**Emergent:**
- Just ingested from source
- Not yet validated in real campaigns
- Hypothesis / initial guidance

**Validated:**
- Confirmed by 2-3+ sources OR proven in campaigns
- Reliable expertise
- Reference with confidence

**Canonical:**
- Referenced 5+ times across knowledge graph
- Core XP Labs outbound methodology
- Foundational concept

**Progression example:**
```
Week 1: [[short-question-subject-lines]] - emergent
        (from one YouTube video)

Month 2: [[short-question-subject-lines]] - validated
         (confirmed in 3 articles + worked in campaigns)

Month 6: [[short-question-subject-lines]] - canonical
         (referenced in 8 other nodes, core pattern)
```

---

## Domains Covered

### 1. Campaign Strategy
- Campaign ideation frameworks
- Offer design principles
- Angle development methods
- Sequencing strategies
- Positioning approaches

### 2. Copywriting
- Subject line patterns
- Opening line tactics
- CTA design principles
- Email structure frameworks
- Personalization methods
- Tone and voice

### 3. ICP Research
- ICP definition methods
- Pain point discovery
- Buyer persona frameworks
- Decision-maker mapping
- Qualification criteria

### 4. Metrics Analysis
- Open rate benchmarks and signals
- Reply rate interpretation
- Meeting conversion patterns
- Negative reply diagnostics
- Performance indicators

### 5. Iteration Signals
- When to iterate vs ditch
- Campaign failure signals
- Success indicators
- Optimization triggers
- Angle pivot frameworks

### 6. List Building
- Data sourcing strategies
- List hygiene practices
- Segmentation frameworks
- Enrichment tactics
- Verification methods

---

## Example Knowledge Nodes

### Node: Subject Line Pattern - Short Questions
- **Domain:** Copywriting
- **Status:** Validated
- **Principle:** Question-based subjects <5 words get 1.5x open rates
- **When to use:** Cold outreach to busy executives
- **Evidence:** Alex Berman video + campaign data across 15 clients
- **Links to:** [[open-rate-signals]], [[personalization-tactics]], [[campaign-ideation]]

### Node: When to Iterate vs Ditch
- **Domain:** Iteration Signals
- **Status:** Emergent
- **Principle:** <1% reply after 100 sends = ditch, 1-3% = iterate
- **When to use:** Weekly campaign review
- **Evidence:** Cold Email Accelerator course
- **Links to:** [[campaign-failure-signals]], [[reply-rate-analysis]], [[copy-optimization]]

### Node: Pain-First Opening Framework
- **Domain:** Campaign Strategy
- **Status:** Validated
- **Principle:** Start with specific pain point before solution
- **When to use:** When ICP has clear, urgent pain
- **Evidence:** Multiple sources + proven in client campaigns
- **Links to:** [[pain-point-research]], [[value-prop-articulation]], [[email-structure]]

---

## How This Differs from the XP Labs Knowledge Base

| **Aspect** | **XP Labs KB** | **Domain Expert KB** |
|------------|-------------------|----------------------|
| **Scope** | XP Labs-specific | Methodology |
| **Content** | XP Labs's ICPs, pain points, competitors | Methodology, patterns, frameworks |
| **Question** | WHAT to say to prospects | HOW to do cold email well |
| **Example** | "XP Labs targets copywriters with manual research pain" | "Pain-first openings have 2x reply rates" |
| **Location** | `knowledge_base/` | `.claude/skills/cold-email-domain-expert-knowledge-base/` |
| **Frontmatter** | `client: xp-labs` | `scope: methodology` |

**They work together:**
```
XP Labs KB: "ICP = copywriters and marketing professionals"
Domain Expert KB: "Pain-first framework for opening lines"

Result: Campaign that targets copywriters with pain-first structure
```

---

## Maintenance

### Automatic Prompts

You'll be reminded to review when:
- **Every 25 nodes ingested** → "Review taxonomy?"
- **Tag sprawl detected** → 10+ tags with ≤2 nodes
- **Orphan tags found** → Tags with 0 nodes
- **Weak linking** → 5+ nodes with <3 links

### Manual Review

You should review:
- **Monthly** (if actively using)
- **Can't find right tag** (when ingesting)
- **After major ingestion** (book, large content batch)

**See:** `_system/TAXONOMY-MAINTENANCE.md` for full guide

---

## Commands

### Add Expertise
```
/ingest-expertise
```
(After pasting content into canvas.md)

### Query Expertise
```
"What does cold email KB say about [topic]?"
"Show me all nodes in copywriting category"
"How do I diagnose low reply rates?"
```

### Check Health
```
"Check cold email domain expert KB health"
```

### Review Taxonomy
```
Read: _system/taxonomy.yaml
```

---

## Growth Timeline

### Phase 1: Foundation (0-25 nodes)
- Seed from 3-5 key sources
- Cover all 6 domains
- Basic patterns established

### Phase 2: Validation (25-100 nodes)
- Multiple sources per topic
- Patterns validated
- Cross-domain links strong

### Phase 3: Maturity (100+ nodes)
- Canonical concepts emerge
- XP Labs's institutional outbound expertise
- Powers all client work
- Competitive advantage

---

## Best Practices

### When Ingesting:
✅ **Use high-quality sources** (expert content, data-backed)
✅ **Paste full content** (don't summarize first)
✅ **Let AI extract concepts** (don't pre-decide)
✅ **Review created nodes** (ensure quality)
✅ **Link related concepts** (strengthen graph)

❌ **Don't ingest fluff** (vague advice, common sense)
❌ **Don't add XP Labs-specific product/market info** (belongs in `knowledge_base/`)
❌ **Don't pre-create nodes** (use /ingest-expertise)

### When Querying:
✅ **Be specific** ("subject line patterns for B2B SaaS")
✅ **Cross-reference domains** (metrics + iteration signals)
✅ **Apply to client context** (methodology + their specifics)

---

## Success Metrics

**Healthy KB:**
- Growing steadily (new ingestions monthly)
- High link density (nodes well-connected)
- Regular usage (agents query frequently)
- Validated concepts emerging
- Clean taxonomy (minimal sprawl)

**Signs to improve:**
- No new ingestions in 30+ days
- Nodes isolated (weak linking)
- Never queried by agents
- All nodes still "emergent"
- Tag sprawl (20+ tags with 1-2 nodes)

---

## Vision

**Today:**
You manually find expertise, ingest it, build knowledge base.

**6 Months:**
Rich knowledge graph with 100+ validated concepts. Agents automatically query when building campaigns. XP Labs's institutional outbound knowledge is a clear competitive advantage.

**1 Year:**
Canonical patterns established. New team members get instant expertise. Every campaign benefits from compounded intelligence. XP Labs becomes a knowledge-driven outbound machine.

---

## Getting Help

**Learn the system:**
- Read: `SKILL.md` (how agents use this)
- Read: `_system/TAXONOMY-MAINTENANCE.md` (how to evolve taxonomy)
- Read: `.claude/commands/ingest-expertise.md` (how ingestion works)

**Questions:**
- "How does cold email domain expert KB work?"
- "Show me example nodes"
- "How do I maintain taxonomy?"

---

**Created:** 2026-01-15
**Version:** 1.0.0
**Purpose:** XP Labs's institutional cold email expertise
