---
name: CONCEPT_NAME_IN_CAPS
description: One sentence description
domain: technical|business|methodology|emergent
node_type: concept|pattern|case-study|framework|anti-pattern|constraints
status: emergent|validated|canonical
client: CLIENT_SLUG
created: YYYY-MM-DD
last_updated: YYYY-MM-DD
source: [VERIFIED: source] | [INFERRED: logic] | [UNVERIFIABLE]
tags:
  - [domain]  # First tag must match domain
  - [tag-2]
  - [tag-3]
topics:
  - topic-1
  - topic-2
  - topic-3
related_concepts:
  - "[[related-concept-1]]"
  - "[[related-concept-2]]"
  - "[[related-concept-3]]"
---

# Concept Name

Brief explanation of the concept (2-3 paragraphs).

**SPECIFICITY REQUIREMENT:** Avoid vague abstractions. Use concrete language that prospects/stakeholders would actually use.

## Concrete Example

**REQUIRED:** Every knowledge node must include at least one concrete, real-world example.

**Example format:**
```
Instead of: "We provide market process optimization"
Use: "We connect sellers to buyers in our network OR buy businesses directly"

Instead of: "Comprehensive business analysis"
Use: "15-minute Loom video showing estimated valuation range based on comparable pottery deal"
```

**Why this example matters:** [Explain what makes this example representative and useful]

## How It Works

**REQUIRED:** Step-by-step breakdown of how this concept operates in practice.

1. **Step 1:** [Concrete action or component]
2. **Step 2:** [Concrete action or component]
3. **Step 3:** [Concrete outcome or result]

**Real-world walkthrough:**
[Describe how this plays out in an actual scenario - be specific about who does what and what happens]

## Key Points

- Key point 1 - [Use concrete language]
- Key point 2 - [Use concrete language]
- Key point 3 - [Use concrete language]

## Evidence

> "Direct quote or specific evidence supporting this concept"
> [VERIFIED: where this came from] or [INFERRED: logic] or [UNVERIFIABLE]

## Validation Questions

**Before using this concept in campaigns/messaging, verify:**
- [ ] Can I point to specific, tangible deliverables or actions?
- [ ] Would the target audience understand this in their own language?
- [ ] Does this avoid internal jargon or vague abstractions?
- [ ] Can I give a concrete example of how this works?

## How It Relates

- [[related-concept-1]] - Explanation of relationship
- [[related-concept-2]] - Explanation of relationship
- [[related-concept-3]] - Explanation of relationship

---

**Status:** emergent|validated|canonical
**Domain:** [domain]
**Source:** [VERIFIED: source] or [INFERRED: logic] or [UNVERIFIABLE]
**Next:** [If emergent: Validate through specific action]

---

## Template Usage Notes

**Specificity Standards:**
- ❌ "Market process" → ✅ "Connect to buyers in our network"
- ❌ "Comprehensive analysis" → ✅ "12-min video showing valuation estimate based on comparable deal"
- ❌ "Strategic consultation" → ✅ "30-min exploratory call to discuss two exit options"
- ❌ "Optimization services" → ✅ "We buy pottery businesses or introduce sellers to buyers"

**Evidence Requirements:**
- Use [VERIFIED: source] when you have direct proof (client docs, campaign data, call transcripts)
- Use [INFERRED: logic] when you're connecting dots from multiple sources
- Use [UNVERIFIABLE] sparingly - most knowledge should be verified or inferred

**Link Requirements:**
- Minimum 3 related_concepts per ontology
- Links should create useful navigation paths
- Don't link just to hit the minimum - make links meaningful

**New Node Types:**
- `anti-pattern` - Use templates/anti-pattern-template.md
- `constraints` - Use templates/campaign-constraints-template.md
- `pattern` - Use templates/email-pattern-template.md for email patterns
