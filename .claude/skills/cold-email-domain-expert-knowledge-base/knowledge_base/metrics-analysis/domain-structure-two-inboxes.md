---
name: DOMAIN_STRUCTURE_TWO_INBOXES
description: Set up 2 inboxes per domain maximum - balances deliverability risk across domain-level and inbox-level reputation
scope: agency
domain: metrics-analysis
node_type: pattern
status: emergent
created: 2026-01-15
last_updated: 2026-01-15
tags:
  - metrics-analysis
topics:
  - open-rate-signals
  - bounce-rate-analysis
related_concepts:
  - "[[inbox-volume-baseline-30-per-day]]"
  - "[[inbox-warmup-three-weeks]]"
  - "[[horizontal-scaling-strategy]]"
source: "GEX Wrapped 2024 by Eric Nowoslawski"
source_url: ""
date_accessed: 2026-01-15
---

# Domain Structure: 2 Inboxes Per Domain

Set up **2 inboxes per domain** (not 3, not 10). This balances inbox capacity with domain-level reputation risk. Domain reputation affects all inboxes on that domain - mess up the domain, all inboxes get flagged.

## Core Principles

- Each inbox has individual spam reputation
- Domain has overarching spam reputation affecting all inboxes
- 2-3 inboxes per domain is sweet spot (GEX uses 2)
- 10+ inboxes per domain concentrates risk too much
- Scale horizontally: more domains, not more inboxes per domain
- Use separate domains from main brand domain

## When to Use

Use 2-inbox structure when:
- Setting up new cold email infrastructure
- Scaling sending capacity
- Want to minimize domain-level risk
- Following conservative best practices
- Don't have hard data supporting 3+ inboxes

## How to Apply

**Standard Setup:**

**Per Domain:**
- Domain: tryacmecorp.com (NOT main domain acmecorp.com)
- Inbox 1: [email protected]
- Inbox 2: [email protected]
- Forward domain to main domain: tryacmecorp.com → acmecorp.com

**Sending Capacity:**
- 2 inboxes × 30 emails/day = 60 emails/day per domain
- Want 1,000 emails/day? Need ~17 domains (34 inboxes)

**Why Not 3-10 Inboxes Per Domain:**

While GEX doesn't have proof 2 is definitively better than 3, they know:
- **Too many inboxes per domain = concentrated risk**
- **Domain reputation > inbox reputation**
- If domain gets flagged, ALL inboxes on it go to spam
- 2-3 seems safer than 10 (less eggs in one basket)

**Risk Calculation:**
```
10 inboxes on 1 domain:
- If domain burns, lose 10 inboxes (300 emails/day capacity)

2 inboxes on 5 domains:
- If 1 domain burns, lose 2 inboxes (60 emails/day capacity)
- 80% capacity remains operational
```

**Alternative Domain Name:**

Don't send from main brand domain. Buy variations:
- Main: acmecorp.com
- Cold email: tryacmecorp.com, getacmecorp.com, goacmecorp.com

**Why:**
- No matter how good campaign is, you'll get spam complaints
- Protect main domain's sending reputation
- Main domain = internal comms, customer comms, exec communications
- Can't risk those going to spam

**Prospect Perception:**

"Won't people think I'm a spammer with alternate domain?"

GEX experience:
- Top 20 website globally (NDA client) uses 200+ sending domains
- Gets 7-26 positive responses/day
- Prospects don't care about domain as long as it forwards to real site
- If reaching out cold, they haven't heard of you anyway
- Just ensure domain forwards to main brand site

**Example Setup for 1,000 emails/day:**

Need: 1,000 ÷ 30/inbox ≈ 34 inboxes

**Domain structure:**
- 17 domains × 2 inboxes each = 34 inboxes

Domains:
- tryacmecorp.com
- getacmecorp.com
- goacmecorp.com
- joinacmecorp.com
- helloacmecorp.com
- (etc., 12 more)

Each domain has [email protected] and [email protected]

## Evidence

[VERIFIED: GEX Wrapped 2024] "Why do we put 2 inboxes on each domain instead of 3? This is one of those things with email deliverability that I don't quite have proof for it necessarily being better. I just know that 2 or 3 is better than putting 10 inboxes on a domain for sure."

[DATA: Domain vs inbox reputation] "The reasoning here is that an inbox has a spam reputation for sure but the domain has an overarching spam reputation that affects all of the inboxes. Mess up a domain and every inbox on that domain will be flagged as spam as well."

[DATA: Setup standard] "In 2024, we set up 2 inboxes per each domain and warmed the domain for 3 weeks."

[DATA: Alternate domain success] "That customer I mentioned before that is a top 20 website in the world that we do outbound for, uses over 200 different domains and we get between 7-26 positive responses per day."

[VERIFIED: Perception] "Keep in mind, if you're reaching out cold, they haven't heard of you before anyway. They don't know what your real domain is. Just make sure it forwards back to your real domain."

## Related Concepts

- [[inbox-volume-baseline-30-per-day]] - Sending capacity per inbox calculation
- [[inbox-warmup-three-weeks]] - Required warmup before using inboxes
- [[horizontal-scaling-strategy]] - How to scale with more domains vs more volume
