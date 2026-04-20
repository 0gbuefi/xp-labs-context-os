---
name: cold-email-domain-expert
description: XP Labs's cold email expertise knowledge base
model: inherit
---

# Cold Email Domain Expert Knowledge Base

## What Is This?

This is XP Labs's **cold email expertise repository** — methodology and best practices that power XP Labs's outbound campaigns.

**Purpose:**
- Store methodology, frameworks, and best practices for cold email campaigns
- Compound institutional knowledge over time
- Provide agents with expert guidance when working on campaigns

**Scope:**
- **Methodology-focused:** HOW to do cold email well, not WHAT to send in a specific campaign
- **Continuously evolving:** Grows smarter as you ingest more expertise

---

## When Agents Use This KB

Agents should query this knowledge base when:

1. **Making iteration decisions:** Should we iterate or ditch this campaign?
2. **Optimizing copy:** What patterns work for subject lines, CTAs, etc.?
3. **Analyzing metrics:** What do these open/reply rates signal?
4. **Diagnosing failures:** Why isn't this campaign working?
5. **Validating ICPs:** Is this target segment well-defined?
6. **Building lists:** What are best practices for list quality?
7. **Designing campaigns:** What angles/frameworks should we use?

**Example queries:**
- "What signals indicate we should ditch a campaign vs. iterate?"
- "What subject line patterns have high open rates?"
- "How do we diagnose low reply rates?"
- "What makes a strong cold email CTA?"

---

## Knowledge Base Structure

```
cold-email-domain-expert-knowledge-base/
├── SKILL.md                    # This file (how to use the KB)
├── canvas.md                   # Staging area for ingestion
├── knowledge_base/             # Atomic knowledge nodes
│   ├── campaign-strategy/      # Campaign ideation, offers, angles
│   ├── copywriting/            # Subject lines, CTAs, structure
│   ├── icp-research/           # ICP definition, pain points
│   ├── metrics-analysis/       # Open rates, reply rates, signals
│   ├── iteration-signals/      # When to iterate/ditch/optimize
│   └── list-building/          # Sourcing, hygiene, segmentation
└── _system/
    ├── taxonomy.yaml           # Blessed tags and categories
    └── ontology.yaml           # How concepts relate
```

---

## How to Use This KB

### For Users: Adding Knowledge

1. **Find valuable content** (YouTube video, article, case study)
2. **Paste into canvas.md** (full transcript or article text)
3. **Run command:**
   ```
   /ingest-expertise
   ```
4. **AI processes content:**
   - Extracts key concepts
   - Creates atomic knowledge nodes
   - Auto-links related concepts
   - Tags with taxonomy

5. **Review prompts:**
   - Every 25 nodes: "Review taxonomy?"
   - Tag sprawl warnings
   - Orphan node alerts

### For Agents: Querying Knowledge

**Pattern 1: Direct Concept Lookup**
```
Read relevant nodes when user asks about specific topics:
- User: "What makes a good subject line?"
- Agent: Read knowledge_base/copywriting/subject-line-*.md files
```

**Pattern 2: Diagnostic Decision**
```
When analyzing campaign performance:
1. Read metrics-analysis/ nodes for signal interpretation
2. Read iteration-signals/ nodes for decision criteria
3. Apply expertise to client's specific situation
```

**Pattern 3: Framework Application**
```
When creating campaigns:
1. Read campaign-strategy/ nodes for ideation frameworks
2. Read copywriting/ nodes for execution patterns
3. Combine with client's specific ICP/pain points
```

---

## Automatic Health Checks

**Every time this skill is invoked, check KB health:**

### 1. Node Count Milestone
```yaml
if total_nodes % 25 == 0:
  prompt_user:
    "📊 Milestone: You've ingested {total_nodes} nodes.

    Recommended: Review taxonomy for consolidation opportunities.
    See: _system/TAXONOMY-MAINTENANCE.md"
```

### 2. Tag Sprawl Detection
```yaml
tags_with_few_nodes = count(tags where node_count <= 2)

if tags_with_few_nodes >= 10:
  warn_user:
    "⚠️ Tag Sprawl Detected

    {tags_with_few_nodes} tags have ≤2 nodes each.
    Consider consolidating related tags.

    Review: _system/taxonomy.yaml"
```

### 3. Orphan Tags
```yaml
orphan_tags = count(tags where node_count == 0)

if orphan_tags > 0:
  warn_user:
    "⚠️ Orphan Tags Found

    {orphan_tags} tags have no nodes.
    Remove from taxonomy if no longer needed.

    Orphan tags: {list_orphan_tags}"
```

### 4. Weak Linking
```yaml
weak_nodes = count(nodes where links < 3)

if weak_nodes > 5:
  warn_user:
    "⚠️ Weak Linking Detected

    {weak_nodes} nodes have <3 links (ontology requires minimum 3).
    Strengthen connections to improve knowledge graph."
```

---

## Health Check Implementation

**When agent invokes this skill, run:**

```python
# Pseudo-code for health checks

def check_kb_health():
    kb_path = "knowledge_base/"

    # Count total nodes
    total_nodes = count_all_markdown_files(kb_path)

    # Check milestone
    if total_nodes % 25 == 0 and total_nodes > 0:
        display_milestone_prompt(total_nodes)

    # Analyze tag distribution
    tag_distribution = analyze_tags_across_nodes(kb_path)

    # Check tag sprawl
    sparse_tags = [tag for tag, count in tag_distribution if count <= 2]
    if len(sparse_tags) >= 10:
        display_tag_sprawl_warning(sparse_tags)

    # Check orphan tags
    taxonomy_tags = load_taxonomy_tags("_system/taxonomy.yaml")
    used_tags = tag_distribution.keys()
    orphan_tags = taxonomy_tags - used_tags
    if len(orphan_tags) > 0:
        display_orphan_warning(orphan_tags)

    # Check link density
    nodes_with_weak_links = count_nodes_with_links_less_than(kb_path, 3)
    if nodes_with_weak_links > 5:
        display_weak_linking_warning(nodes_with_weak_links)

    # Return health summary
    return {
        "total_nodes": total_nodes,
        "healthy": all_checks_passed,
        "warnings": list_of_warnings
    }
```

---

## Query Patterns for Agents

### Pattern 1: Topic-Based Search

**User asks about a topic:**
```
User: "How do I know when to iterate vs. ditch a campaign?"

Agent:
1. Read knowledge_base/iteration-signals/when-to-iterate.md
2. Read knowledge_base/iteration-signals/when-to-ditch.md
3. Read knowledge_base/iteration-signals/campaign-failure-signals.md
4. Synthesize answer from nodes
5. Apply to user's specific context
```

### Pattern 2: Diagnostic Application

**User has campaign data:**
```
User: "Campaign has 15% open rate, 0.5% reply rate. What should I do?"

Agent:
1. Read knowledge_base/metrics-analysis/open-rate-signals.md
2. Read knowledge_base/metrics-analysis/reply-rate-analysis.md
3. Interpret signals (low open = subject line issue)
4. Read knowledge_base/iteration-signals/when-to-iterate.md
5. Recommend action based on expertise
```

### Pattern 3: Framework Retrieval

**User needs methodology:**
```
User: "What frameworks exist for creating cold email offers?"

Agent:
1. Search knowledge_base/campaign-strategy/ for "offer" patterns
2. Read all offer-related framework nodes
3. Present frameworks with examples
4. Help user apply to their specific client
```

---

## Node Structure Standard

Every knowledge node in this KB follows this format:

```yaml
---
name: CONCEPT_NAME_IN_CAPS
description: One sentence description
scope: agency                    # Always "agency" for this KB
domain: campaign-strategy|copywriting|icp-research|metrics-analysis|iteration-signals|list-building
node_type: concept|pattern|framework|case-study|diagnostic
status: emergent|validated|canonical
created: YYYY-MM-DD
last_updated: YYYY-MM-DD
tags:
  - [domain]                     # First tag = domain
topics:
  - [3-7 topics from taxonomy]
related_concepts:
  - "[[concept-1]]"
  - "[[concept-2]]"
  - "[[concept-3]]"              # Minimum 3 links
source: "[YouTube video title / Article URL / Book name]"
date_accessed: YYYY-MM-DD
---

# Concept Name

[2-3 paragraph explanation of the concept, pattern, or framework]

## Core Principles

- [Key principle 1]
- [Key principle 2]
- [Key principle 3]

## When to Use

[Specific scenarios where this knowledge applies]

## How to Apply

[Step-by-step guidance or examples]

## Evidence

[VERIFIED: source] "[Direct quote or data from source]"

[VALIDATED: context] "[Real-world results from applying this]"

## Related Concepts

- [[related-concept-1]] - How they relate
- [[related-concept-2]] - How they relate
- [[related-concept-3]] - How they relate
```

---

## Integration with Client Work

### How This KB Relates to Client KBs

**XP Labs Knowledge Base (`knowledge_base/`):**
- Stores XP Labs-specific info (ICPs, pain points, competitors, product features)
- Located: `knowledge_base/`

**Cold Email Domain Expert KB:**
- Stores methodology and expertise (HOW to write emails, WHEN to iterate)
- Located: `.claude/skills/cold-email-domain-expert-knowledge-base/`

**Workflow Example:**

```
User: "Create cold email campaign for XP Labs"

Agent:
1. Read XP Labs's knowledge base:
   - ICP: [[icp-copywriters]]
   - Pain points: [[pain-point-manual-reddit-research]]
   - Value prop: [[value-prop-automated-language-mining]]

2. Query cold email domain expert KB:
   - [[campaign-ideation-framework]]
   - [[pain-first-opening-pattern]]
   - [[subject-line-patterns-high-open]]

3. Combine XP Labs-specific + methodology expertise:
   - Create campaign using XP Labs's pain points
   - Apply proven subject line patterns
   - Use campaign ideation framework
   - Result: Customized campaign with expert methodology
```

**Key Principle:**
- XP Labs KB = WHAT to say (specific to XP Labs's market)
- Domain Expert KB = HOW to say it (methodology)

---

## Knowledge Lifecycle

### Emergent → Validated → Canonical

**Emergent:**
- Just ingested from source content
- Not yet proven in real campaigns
- Used as hypothesis/guidance

**Validated:**
- Seen in 2-3+ sources OR proven in campaigns
- Reliable expertise
- Reference with confidence

**Canonical:**
- Referenced 5+ times across nodes
- Core expertise
- Foundation for XP Labs's outbound methodology

**Upgrade triggers:**
- Emergent → Validated: Multiple sources confirm OR campaign results validate
- Validated → Canonical: Becomes highly referenced hub in knowledge graph

---

## Maintenance Reminders

### Automatic Prompts (Every 25 Nodes)

```
📊 KB Milestone: 25 nodes ingested

Time to review taxonomy health:

1. Check _system/taxonomy.yaml
2. Look for tags with <3 nodes (consolidate?)
3. Look for unused tags (remove?)
4. Add new categories if needed

See: _system/TAXONOMY-MAINTENANCE.md for full guide
```

### Manual Review Triggers

You should manually review when:
- Can't find the right tag when ingesting content
- Tags feel ambiguous or overlapping
- Node count reaches 50, 100, 150, etc.
- Monthly (if actively using)

---

## Example Usage Scenarios

### Scenario 1: Campaign Performance Analysis

```
User: "Our campaign has 25% open rate, 2% reply rate, but only 10% meeting conversion. What's wrong?"

Agent uses this KB:
1. Read metrics-analysis/open-rate-signals.md
   → 25% open is decent, subject line works
2. Read metrics-analysis/reply-rate-analysis.md
   → 2% reply is okay, email resonates
3. Read metrics-analysis/meeting-conversion.md
   → 10% is low, CTA or offer might be weak
4. Read iteration-signals/when-to-iterate.md
   → Iterate CTA, not entire campaign
5. Read copywriting/cta-design.md
   → Apply CTA best practices

Result: Specific, expert diagnosis
```

### Scenario 2: Campaign Ideation

```
User: "I need 5 campaign ideas for a new B2B SaaS client"

Agent uses this KB:
1. Read campaign-strategy/campaign-ideation.md
   → Framework for generating angles
2. Read copywriting/opening-lines.md
   → Patterns for strong hooks
3. Read icp-research/pain-point-research.md
   → How to validate pain points

Agent then applies framework to client's specific context
```

---

## Quality Standards

### For Ingested Nodes:
- ✅ `scope: agency` in frontmatter
- ✅ Minimum 3 related_concepts links
- ✅ Tags align with taxonomy.yaml
- ✅ Source attribution included
- ✅ Clear, actionable guidance
- ✅ Domain correctly categorized

### For Knowledge Graph:
- ✅ No orphan nodes (<3 links)
- ✅ Cross-domain connections (not isolated)
- ✅ Bidirectional links where appropriate
- ✅ Clear relationship descriptions

---

## Advanced: Cross-Campaign Pattern Recognition

**Future capability:**
As you use this KB across campaigns, you'll identify patterns:
- "This subject line pattern works across multiple campaigns"
- "This pain point research method is consistently effective"
- "This iteration threshold (2 weeks) is standard"

These insights get ingested back into this KB, making it smarter over time.

---

## Quick Reference Commands

**Add knowledge:**
```
/ingest-expertise
```

**Check KB health:**
```
"Check cold email domain expert KB health"
```

**Query expertise:**
```
"What does the cold email KB say about [topic]?"
```

**Review taxonomy:**
```
Read: _system/taxonomy.yaml
```

---

**Created:** 2026-01-15
**Version:** 1.0.0
**Scope:** XP Labs cold email expertise
