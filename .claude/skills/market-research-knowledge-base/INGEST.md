---
name: ingest-to-market-research-kb
description: Step-by-step process for ingesting new content (transcripts, articles, sales pages, course notes) into this market research knowledge base. Self-contained and portable — works wherever this KB is located.
model: inherit
---

# How to Ingest New Content into This Knowledge Base

## Overview

This skill teaches you to take raw content — a video transcript, article, sales page, course summary, or any other source — and extract it into properly formatted atomic knowledge nodes inside this knowledge base.

**Portability note:** All file references in this skill are relative to the directory containing this file. Do not use absolute paths. If this KB has been moved or copied, the process is identical — just resolve paths relative to this `INGEST.md` file's location.

**Directory structure (relative to this file):**
```
./SKILL.md                    ← KB overview and query patterns
./INGEST.md                   ← This file
./canvas.md                   ← Staging area for raw content
./knowledge_base/
│   ├── source-platforms/     ← WHERE to find audiences online
│   ├── research-process/     ← HOW to execute research
│   ├── voice-of-customer/    ← WHAT to look for and extract
│   └── research-strategy/    ← WHEN/HOW MUCH research to do
./_system/
│   ├── taxonomy.yaml         ← Blessed tags and topics
│   └── ontology.yaml         ← Relationship rules
```

---

## Step 1: Receive the Content

Content arrives in one of two ways:

**A. Via canvas.md (standard)**
The user pastes raw content into `./canvas.md`. Read it fully before doing anything else.

**B. Via direct reference**
The user points to a file, URL, or pastes content directly in the conversation. Treat it the same way.

**Accepted content types:**
- Video/audio transcripts (timestamped or plain)
- Articles and blog posts
- Course notes or module summaries
- Sales pages (mine for methodology insights, not product pitches)
- PDF excerpts or pasted text
- Conversation notes or braindumps

**Before analysis:** Read the entire content once through without taking notes. Get a feel for the source's scope, quality, and domain focus. Then proceed.

---

## Step 2: Identify Candidate Concepts

Read through the content a second time and extract every distinct, potentially reusable insight. Look for:

- A named technique, framework, or methodology
- A principle that explains WHY something works
- A tactical pattern (repeatable how-to)
- A diagnostic rule (how to make a decision)
- A platform or tool with specific usage guidance
- A concept that has a named opposition (e.g. "surface statement vs. true desire")
- Any insight the source author treats as significant or original

**What to ignore:**
- Narrative filler, jokes, and transitional content
- Anecdotes that illustrate existing concepts without adding new ones
- Promotional content or testimonials (unless they contain methodology)
- Restatements of things already covered

**Output of this step:** A rough list of 2–8 candidate concepts with one-line descriptions. Hold these in working memory — do not create files yet.

---

## Step 3: Deduplication Check (Critical — Do Not Skip)

Before creating anything, scan existing nodes to identify what's already captured.

**Process:**
1. List all files in `./knowledge_base/source-platforms/`
2. List all files in `./knowledge_base/research-process/`
3. List all files in `./knowledge_base/voice-of-customer/`
4. List all files in `./knowledge_base/research-strategy/`
5. For each candidate concept from Step 2, read the most likely matching existing node(s)
6. Make an explicit verdict on each candidate:

| Candidate | Verdict | Action |
|---|---|---|
| Concept X | Already fully captured in `node-name.md` | Skip |
| Concept Y | Partially captured — missing angle Z | Update existing node |
| Concept Z | Not captured anywhere | Create new node |

**Signals that something is already captured:**
- The existing node's `description` frontmatter covers the concept
- Reading the node body, you find the insight is already there
- The concept is referenced as a `related_concepts` link in multiple nodes

**Signals that an update is warranted (not a new node):**
- The existing node covers the concept but is missing a specific sub-case, mode, or example from the new source
- The new source adds a concrete evidence quote that strengthens an existing claim
- The new source introduces a nuance that qualifies or extends an existing principle

**When in doubt:** Prefer updating an existing node over creating a new one. Fewer, richer nodes beat many thin ones.

---

## Step 4: Classify Each New Node by Domain

For each concept confirmed as new, assign it to exactly one domain using these criteria:

### `source-platforms/`
The concept is about **WHERE** to find audiences online — a specific platform, tool, or access method.
- Examples: Reddit research, Amazon reviews, Facebook Ads Library, inurl: operator, Clickbank VSLs
- Ask: "Is this primarily about a place or tool for finding data?"

### `research-process/`
The concept is about **HOW** to execute research — the mechanics and workflow.
- Examples: three-step introverted process, emotion word search targeting, customer zukan documentation
- Ask: "Is this primarily about the steps or mechanics of doing research?"

### `voice-of-customer/`
The concept is about **WHAT** to look for in research data — extracting, interpreting, and applying audience language.
- Examples: identity as primary buying driver, surface statement vs. true desire, specific situation beats generic pain
- Ask: "Is this primarily about understanding or using what the audience says?"

### `research-strategy/`
The concept is about **WHEN and HOW MUCH** — scoping, prioritisation, stopping criteria, or meta-decisions.
- Examples: market awareness spectrum, research saturation stopping criteria, AI limitations for market research
- Ask: "Is this primarily about deciding how to approach or scope the research effort?"

**If a concept touches two domains:** Assign to the domain it serves most directly. Add the secondary domain's topics to the `topics:` frontmatter field.

---

## Step 5: Author Each New Node

Create one file per concept in the appropriate domain folder. Use this exact format:

### File naming
- Lowercase, hyphen-separated
- Descriptive but concise (3–5 words)
- Should be readable as a wiki-link: `[[specific-situation-beats-generic-pain]]`
- Examples: `emotion-word-search-targeting.md`, `journey-to-this-moment.md`

### Frontmatter (required fields)

```yaml
---
name: CONCEPT_NAME_IN_CAPS_WITH_UNDERSCORES
description: One sentence. What this concept is and why it matters. Should be readable standalone.
scope: agency
domain: source-platforms|research-process|voice-of-customer|research-strategy
node_type: concept|pattern|framework|case-study|diagnostic
status: emergent|validated|canonical
created: YYYY-MM-DD
last_updated: YYYY-MM-DD
tags:
  - [primary domain tag — same as domain value]
topics:
  - [3–7 topics from taxonomy.yaml — read the file to choose correctly]
related_concepts:
  - "[[concept-slug-1]]"
  - "[[concept-slug-2]]"
  - "[[concept-slug-3]]"
source: "Title of source (video transcript / article / course notes / sales page)"
date_accessed: YYYY-MM-DD
---
```

**Node type guide:**
- `concept` — an atomic idea or principle
- `pattern` — a repeatable tactic or approach
- `framework` — a structured multi-part methodology
- `diagnostic` — decision-making criteria or a test
- `case-study` — real example with results (rare)

**Status guide:**
- `emergent` — from one source, not yet cross-validated
- `validated` — confirmed across 2–3+ scenarios or sources
- `canonical` — core expertise, referenced 5+ times across the KB

### Node body structure

```markdown
# [Concept Name in Title Case]

## [Hook — the problem this concept solves, or the core tension]

One or two sentences framing why this matters. What breaks without it?

---

## Core Principle

The single most important idea. If someone only reads this section, what must they understand?

---

## [Section 2 — varies by node_type]

For `concept`: "How It Works" or "Why This Is True"
For `pattern`: "How to Apply" with numbered steps
For `framework`: "The Components" with sub-sections per component
For `diagnostic`: "The Decision Criteria" with if-then logic

---

## [Section 3 — context and application]

When to use this. What triggers it. How it connects to actual cold email work.

---

## Evidence

[VERIFIED: Source name] "Direct quote from source, word for word."

[VERIFIED: Source name] "Second quote if available."

---

## Related Concepts

- [[concept-slug]] — One sentence on how this relates
- [[concept-slug]] — One sentence on how this relates
- [[concept-slug]] — One sentence on how this relates
```

**Evidence block rules:**
- Always quote directly — never paraphrase in Evidence
- Include source name in brackets
- At least one quote per node; two or three is better
- If the source is a video transcript, quote the spoken words verbatim

**Related concepts rules:**
- Minimum 3 links per node (KB health requirement from taxonomy.yaml)
- Link to nodes that already exist — do not link to nodes you haven't created yet unless you're creating them in this same ingestion batch
- One sentence per link explaining the relationship (not just restating the linked node's name)

---

## Step 6: Update Existing Nodes

For any candidate marked "update existing" in Step 3:

1. Read the full existing node
2. Identify exactly where the new content fits (which section, or as a new section)
3. Make the targeted edit — add the new sub-case, mode, example, or evidence quote
4. Update `last_updated:` in frontmatter to today's date
5. If the update adds a link to a new node you're creating in this batch, add it to `related_concepts:`

**What warrants a section addition vs. inline addition:**
- New mode, case, or variant → add as a new `### Sub-heading` within the relevant section
- New evidence quote → append to the Evidence block
- New related concept → append to Related Concepts
- New application nuance → add a paragraph within the relevant section

---

## Step 7: Add Backlinks to Existing Nodes (When Needed)

When you create a new node that is closely related to an existing node, add the new node as a backlink in the existing node's `related_concepts:` section — if it strengthens the existing node's usefulness.

**Do this when:**
- The new node is a direct extension, counterpart, or application of the existing one
- An agent querying the existing node would obviously want to know about the new one

**Don't do this for every link** — only where the relationship is meaningful and bidirectional.

---

## Step 8: Compile Your Report

Before clearing the canvas, output a summary to the user:

```
## Ingestion Complete

**New nodes created (N):**
- `domain/filename.md` — one-line description
- `domain/filename.md` — one-line description

**Existing nodes updated (N):**
- `domain/filename.md` — what was added/changed

**Already captured — skipped (N):**
- Concept X → already in `existing-node.md`

**Canvas:** Cleared
```

This gives the user a clear record of what changed and why nothing was missed.

---

## Step 9: Clear the Canvas

After ingestion is complete, reset `./canvas.md` to its default empty state:

```markdown
# [KB Name] - Canvas

**Purpose:** Staging area for content to be ingested into this knowledge base.

---

Paste transcripts, articles, or other content here, then run the ingest skill.
```

Do not leave source content in the canvas after ingestion.

---

## Step 10: Health Check

After any ingestion session, run a quick health check against the thresholds in `./_system/taxonomy.yaml`:

- **Node count milestone:** Count total nodes across all domains. If divisible by 25 (or just crossed a 25-node threshold), prompt the user: "You've hit [N] nodes — good time for a taxonomy review."
- **Tag sprawl:** If you notice you've been using tags not in `taxonomy.yaml`, flag them for review
- **Weak linking:** If any node you created has fewer than 3 related_concepts links, note it and suggest candidates

---

## Quick Reference: Common Mistakes to Avoid

| Mistake | Correct approach |
|---|---|
| Creating a node before scanning existing ones | Always do Step 3 first |
| Creating two thin nodes that cover the same concept | Merge into one richer node |
| Putting a "how to" tactic in research-strategy | Tactics go in research-process; strategy = scoping/prioritisation decisions |
| Linking to nodes that don't exist yet | Only link to existing nodes (or nodes in the same ingestion batch) |
| Paraphrasing in Evidence blocks | Quote directly, word for word |
| Leaving source content in canvas.md | Always clear after ingestion |
| Using absolute file paths | Always use paths relative to this file's location |
| Assigning `canonical` status on first ingestion | First ingestion = `emergent`; promote only after cross-validation |

---

## Taxonomy Reference

Before tagging any node, read `./_system/taxonomy.yaml` to confirm:
- Your `domain:` value matches one of the four blessed domains
- Your `topics:` values are drawn from the taxonomy's topic library
- You're not inventing new tags (add to taxonomy only if 3+ nodes would use them)

---

## Example Ingestion Walkthrough

**Input:** A transcript about how Amazon reviews reveal different buyer psychology than Reddit.

**Step 2 candidates:**
- Amazon reviews show post-purchase rationalisation (different from Reddit's pre-purchase frustration)
- Star rating as sentiment filter before reading

**Step 3 dedup check:**
- Read `./knowledge_base/source-platforms/amazon-reviews-voc-mining.md`
- First candidate: partially covered — node covers Amazon reviews generally but doesn't address the pre/post-purchase psychology distinction → **Update existing node**
- Second candidate: mentioned briefly in existing node → **Already captured, skip**

**Step 4:** Only one update needed, no new nodes.

**Step 6:** Add a "Pre vs. Post Purchase Psychology" sub-section to the existing `amazon-reviews-voc-mining.md` node. Add evidence quote. Update `last_updated:`.

**Step 8:** Report — 0 new nodes, 1 updated, 1 skipped.

**Step 9:** Clear canvas.

---

*This skill is self-contained. It works wherever this knowledge base directory is located.*
