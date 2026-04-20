---
name: BATCH_TESTING_FRAMEWORK
description: Four-batch systematic testing framework - Batch 1 (AI messaging), Batch 2 (triggers/lists), Batch 3 (formatting), Batch 4 (hyper-specific)
scope: agency
domain: campaign-strategy
node_type: framework
status: emergent
created: 2026-01-15
last_updated: 2026-01-15
tags:
  - campaign-strategy
topics:
  - campaign-ideation
  - sequencing-strategy
  - angle-development
related_concepts:
  - "[[lookalike-campaign-template]]"
  - "[[standard-sequence-template]]"
  - "[[creative-ideas-campaign]]"
source: "GEX Wrapped 2024 by Eric Nowoslawski"
source_url: ""
date_accessed: 2026-01-15
---

# Batch Testing Framework (Finding Message-Market Fit)

Systematic **four-batch testing framework** for finding message-market fit. Each batch tests different variables (messaging, targeting, format, hyper-personalization) to ensure comprehensive experimentation.

## Core Principles

- Test one variable at a time when possible
- Batch 1-2: High-probability tests with AI and triggers
- Batch 3: Remove AI, test pure copywriting variations
- Batch 4: Hyper-specific, potentially unscalable tactics
- Framework ensures nothing gets forgotten
- Change value prop angle throughout (chunking up/down)

## When to Use

Use this framework when:
- Onboarding new clients (systematic testing)
- First campaigns fail (need structured experimentation)
- Want comprehensive test coverage
- Training team on test methodology
- Documenting what's been tried

## How to Apply

### BATCH 1: AI Messaging + Lookalike Targeting

**Hypothesis:** Most customers know their ICP. Test messaging variations with AI personalization.

**Three Campaign Templates:**

**1. Lookalike Campaign:**
- Find case study customers
- Use Ocean.io to build lookalike audience
- Message: "Saw you're in [industry] like our customer [Case Study]"
- Messaging = actual case study success (no guessing needed)
- Most specific, least scalable

**2. Standard Sequence Template:**
- AI-generated first line (why you, why now)
- Test 3 value prop versions (save time/money, make money, reduce risk)
- AI-generated line 3: "How this applies to YOUR specific situation"
- Training AI on: their company, our service, value prop being tested

**3. Creative Ideas Campaign:**
- AI generates 3 custom ideas for prospect
- Based on: their company mission + our services
- Often most successful - AI brainstorms angles humans might miss
- Review winning AI ideas, train it to replicate

**Process:**
- Run all 3 campaigns in parallel
- If one works, analyze why
- If all fail, proceed to Batch 2

### BATCH 2: Triggers + List Refinement

**Hypothesis:** Wrong targeting or timing, not wrong messaging.

**Trigger Tests:**
- New in role
- Hiring for roles
- Tech installed on site
- Specific keywords (LinkedIn profile or website)
- Past company experience at current customers
- First time in role
- New fundraise
- Employee headcount growth/decrease

**List Pivot Strategy:**
```
IF Batch_1_successful:
    use_similar_list_with_triggers()
ELSE:
    drastically_change_list()

Example:
- Batch 1: CTOs at HealthTech companies
- Batch 2A: Product Leaders at HealthTech (role change)
- Batch 2B: CTOs at FinTech (industry change)
```

**Keep messaging similar to isolate list variable.**

### BATCH 3: Copywriting Format + No AI

**Hypothesis:** After 1,000+ emails with no positive responses, need fundamental change.

**Remove AI entirely. Test pure copywriting formats:**

**1. Poke the Bear (Josh Braun)**
```
[Relevant first line]
[Poke the bear question]
Case study: [outcome] in [timeframe] without [risk]
Would this solve [problem] for you?
```

**2. Asking About Priority (PWJ)**
```
Subject: [priority question preview]
Are there any discussions internally re: [what you help with]?
We help companies like [case study] achieve [outcome].
Is this a priority over at [company]?
```

**3. Extremely Short**
```
[Relevant first line or fallback]
If I could help [outcome], is that interesting?

(Sometimes 2-3 sentences beats longer emails)
```

**Also test:**
- Different value prop angles (chunking up/down)
- New offers or lead magnets
- Weekend fact-finding emails to ICs (gather intel)

### BATCH 4: Hyper-Specific (Potentially Unscalable)

**Hypothesis:** Need ultra-high personalization, even if manual.

**Examples:**
- Screenshots of their website pages
- AI analysis of job descriptions
- Company news summarization
- Competitor call-outs
- Case study matching with Ocean.io
- Google review mentions
- Local restaurant offers
- Dynamic meme/image generation

**These may not scale but:**
- Validate if message resonates
- Can inform simpler scalable version
- Prove channel viability before investing

**Process:**
- Test 10-20 hyper-personalized sends
- If responses come in, find automation angle
- If still nothing, consider channel fit

## Evidence

[VERIFIED: GEX Wrapped 2024] "This is the order of campaigns and templates we are currently using in an attempt to find message market fit for our customers. Stressing the keyword here 'Hypothesis' as I'm still exploring if this is the best way to test things for customers."

[DATA: Four batches defined]
- "Batch 1 - we test messaging with lookalike targeting and AI generated copy"
- "Batch 2 - we test triggers and changing their lists a ton"
- "Batch 3 - we throw out the AI messaging and use new messaging templates"
- "Batch 4 - we do things that might not be scalable but are ways to create hyper specific lists"

[VERIFIED: Purpose] "I developed these batches so that we had a checklist to follow so that we didn't forget any idea that would be useful for a customer of ours to try and experiment with. The batches are basically ways to make sure you are testing different lists, variations of AI, no AI, and formats to try as many experiments as you can."

## Related Concepts

- [[lookalike-campaign-template]] - Batch 1 template details
- [[standard-sequence-template]] - Batch 1 AI personalization approach
- [[creative-ideas-campaign]] - Batch 1 highest-performing template
