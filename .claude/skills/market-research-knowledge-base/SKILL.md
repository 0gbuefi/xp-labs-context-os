---
name: market-research-knowledge-base
description: XP Labs's market research methodology knowledge base — how to find and mine real-world audience language online
model: inherit
---

# Market Research Knowledge Base

## What Is This?

XP Labs's **market research methodology repository** — methodology and best practices for finding and mining real-world audience language.

**Purpose:**
- Store techniques, platforms, and processes for finding where target audiences talk online
- Extract authentic voice-of-customer language to power cold email copy and campaign angles
- Compound research methodology expertise over time

**Scope:**
- **Methodology-focused:** HOW to research audiences, not WHAT to say in a specific campaign
- **Continuously evolving:** Grows smarter as you ingest more expertise

---

## When Agents Use This KB

Agents should query this knowledge base when:

1. **Starting ICP research for a new client:** Where should we look for this audience?
2. **Finding copy angles:** What language is the ICP using about their pain?
3. **Validating pain points:** Are we sure this is a real problem? What's the evidence?
4. **Mining voice-of-customer:** What words, phrases, metaphors do they use?
5. **Scoping research effort:** How much research is needed for this job?
6. **Deciding where to look:** Which platforms make sense for this niche?

**Example queries:**
- "Where should I do research for a B2B SaaS targeting CFOs?"
- "How do I extract copy-worthy language from a Reddit thread?"
- "What framework should I use for documenting research findings?"
- "When have we done enough research to start writing?"

---

## Knowledge Base Structure

```
market-research-knowledge-base/
├── SKILL.md                    # This file (how to use the KB)
├── canvas.md                   # Staging area for ingestion
├── knowledge_base/             # Atomic knowledge nodes
│   ├── source-platforms/       # Where to find audiences (Reddit, Amazon, YouTube, etc.)
│   ├── research-process/       # The actual steps and process for doing research
│   ├── voice-of-customer/      # Extracting language, identity, pain, dreams, obstacles
│   └── research-strategy/      # When to stop, how much to do, project scoping
└── _system/
    ├── taxonomy.yaml           # Blessed tags and categories
    └── ontology.yaml           # How concepts relate
```

---

## How to Use This KB

### For Users: Adding Knowledge

1. **Find valuable content** (YouTube video, course, article, case study)
2. **Paste into canvas.md** (full transcript or article text)
3. **Run command:**
   ```
   Ingest this canvas into the market research knowledge base
   ```
4. **AI processes content:**
   - Extracts key concepts
   - Creates atomic knowledge nodes
   - Auto-links related concepts
   - Tags with taxonomy

### For Agents: Querying Knowledge

**Pattern 1: Platform Selection**
```
When user asks where to research a specific audience:
1. Read source-platforms/ nodes for platform options
2. Apply anonymous-platform-advantage principle
3. Recommend platforms appropriate to the niche
```

**Pattern 2: Research Execution**
```
When user is starting research for a client:
1. Read research-process/ nodes for methodology
2. Read voice-of-customer/ nodes for what to look for
3. Guide user through the process
```

**Pattern 3: Research Scoping**
```
When deciding how much research to do:
1. Read research-strategy/ nodes for stopping criteria
2. Apply project-value threshold guidance
3. Recommend appropriate depth
```

---

## Node Structure Standard

Every knowledge node in this KB follows this format:

```yaml
---
name: CONCEPT_NAME_IN_CAPS
description: One sentence description
scope: agency
domain: source-platforms|research-process|voice-of-customer|research-strategy
node_type: concept|pattern|framework|case-study|diagnostic
status: emergent|validated|canonical
created: YYYY-MM-DD
last_updated: YYYY-MM-DD
tags:
  - [domain]
topics:
  - [3-7 topics from taxonomy]
related_concepts:
  - "[[concept-1]]"
  - "[[concept-2]]"
  - "[[concept-3]]"
source: "[Video title / Article URL / Book name]"
date_accessed: YYYY-MM-DD
---
```

---

## Integration with Client Work

### How This KB Relates to Client KBs

**XP Labs Knowledge Base (`knowledge_base/`):**
- Stores XP Labs-specific info (ICPs, pain points, competitors, product features)
- Located: `knowledge_base/`

**Market Research Domain Expert KB:**
- Stores methodology (HOW to find and extract audience language)
- Located: `.claude/skills/market-research-knowledge-base/`

**Workflow Example:**

```
User: "Research the ICP for XP Labs (B2B SaaS, targets copywriters)"

Agent:
1. Query market research KB:
   - [[anonymous-platform-advantage]] → go to Reddit first
   - [[three-step-introverted-research-process]] → find, read, document
   - [[identity-problems-dreams-obstacles-framework]] → what to look for

2. Execute research on Reddit/forums/Amazon
3. Extract voice-of-customer language
4. Store findings in XP Labs's knowledge base:
   - ICP: [[icp-copywriters]]
   - Pain points: [[pain-point-manual-reddit-research]]
   - Language: [[copywriter-research-language]]
```

**Key Principle:**
- Market Research KB = HOW to find audience language
- XP Labs KB = WHAT that audience says (specific to XP Labs's market)

---

## Automatic Health Checks

**Every time this skill is invoked, check KB health:**

- Node count milestone: every 25 nodes, prompt taxonomy review
- Tag sprawl: warn if >10 tags with ≤2 nodes
- Orphan tags: warn if any taxonomy tags have 0 nodes
- Weak linking: warn if >5 nodes have <3 links

---

## Quick Reference Commands

**Add knowledge:**
```
Ingest [canvas/transcript] into market research knowledge base
```

**Query expertise:**
```
"What does the market research KB say about [topic]?"
```

**Review taxonomy:**
```
Read: _system/taxonomy.yaml
```

---

**Created:** 2026-02-19
**Version:** 1.0.0
**Scope:** XP Labs market research methodology
