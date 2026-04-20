---
name: CAMPAIGN_CONSTRAINTS_CLIENT_NAME
description: What this client will and won't do for campaigns
domain: business
node_type: constraints
status: canonical
client: CLIENT_SLUG
created: YYYY-MM-DD
updated: YYYY-MM-DD
source: [VERIFIED: client-onboarding] or [VERIFIED: campaign-feedback]
topics:
  - client-operations
  - campaign-execution
  - offer-viability
related_nodes:
  - "[[front-end-offers]]"
  - "[[email-voice-and-tone]]"
  - "[[value-prop-nodes]]"
---

# Campaign Constraints - CLIENT_NAME

## Purpose

Defines what CLIENT_NAME will and won't do for cold email campaigns to prevent generating non-viable offers and ensure all campaigns align with client capabilities and preferences.

**Last updated:** YYYY-MM-DD

---

## Will Do

### Offers & Deliverables

**High-priority (client loves these):**
- [ ] [Deliverable type 1] - [Why client likes this]
- [ ] [Deliverable type 2] - [Why client likes this]

**Acceptable (client will do if needed):**
- [ ] [Deliverable type 3] - [Any conditions/limitations]
- [ ] [Deliverable type 4] - [Any conditions/limitations]

Example:
**High-priority:**
- Direct exploratory calls - Client prefers human conversation, closes well on calls
- 1-pagers/brief documents - Low time investment, high perceived value

**Acceptable:**
- Email sequences (2-3 emails max) - Will do but prefers shorter sequences

### Communication Channels

- [ ] Email outreach
- [ ] LinkedIn outreach
- [ ] Phone calls (for qualified prospects)
- [ ] [Other channels]

### Time/Effort Commitments

**Per prospect:**
- Initial outreach: [Time commitment]
- Follow-up: [Time commitment]
- Discovery call: [Typical duration]

Example:
- Initial outreach: Automated sequences (minimal time)
- Follow-up: 30-min exploratory calls
- Discovery: 45-60 min deep-dive calls

---

## Won't Do

### Offers & Deliverables (HARD NO)

**Never offer these:**
- ❌ [Deliverable type 1] - [Why client refuses]
- ❌ [Deliverable type 2] - [Why client refuses]

Example:
- ❌ Loom video audits - Client uncomfortable on camera, doesn't want to record videos
- ❌ Free consulting sessions (>60 min) - Time constraints, devalues expertise
- ❌ Free implementation work - Scope creep risk, sets bad precedent

**Source:** [VERIFIED: client feedback on Campaign X, Date]

### Communication Approaches

**Avoid:**
- [Approach 1] - [Why]
- [Approach 2] - [Why]

Example:
- Aggressive urgency tactics - Doesn't align with brand positioning
- Discounting/pricing in cold emails - Cheapens perception

### Audience/ICP Restrictions

**Don't target:**
- [Segment 1] - [Reason]
- [Segment 2] - [Reason]

Example:
- Businesses under $X revenue - Below client's minimum deal size
- [Industry/vertical] - Client lacks expertise/interest

---

## Conditional (Ask First)

**Requires approval:**
- [ ] [Activity 1] - [Why it needs approval]
- [ ] [Activity 2] - [Why it needs approval]

Example:
- Case study creation - Depends on NDA constraints, client approval needed
- Webinar/workshop format - Client interest varies, check bandwidth first

---

## Messaging Preferences

### Must Include

**Required elements in all campaigns:**
- [Element 1] - [Why]
- [Element 2] - [Why]

Example:
- Clarify buying/selling context early - Prevents confusion in acquisition outreach
- Mention dual path explicitly - Core differentiator for this client

### Must Avoid

**Forbidden language/approaches:**
- [Approach 1] - [Why]
- [Approach 2] - [Why]

Example:
- Generic M&A jargon - Target audience doesn't speak this language
- Vague "market process" language - Be specific about "connect to buyers OR buy directly"

---

## Validation Questions

**Before generating any campaign for CLIENT_NAME, ask:**

1. Does this offer require the client to do anything in the "Won't Do" list?
   - If YES → ❌ Invalid offer
   - If NO → Continue

2. Does this offer align with "Will Do" deliverables?
   - If YES → ✅ Viable offer
   - If UNSURE → Check "Conditional" section

3. Does the copy include all "Must Include" elements?
   - If NO → ❌ Revise before presenting

4. Does the copy avoid all "Must Avoid" elements?
   - If NO → ❌ Revise before presenting

---

## Examples

### ✅ Good Offer (Aligned)
```
Offer: 30-min exploratory call to discuss dual exit paths
Why: Direct call (client loves), clarifies dual path (must include), no video/Loom required
```

### ❌ Bad Offer (Misaligned)
```
Offer: 15-min Loom video audit of exit strategy
Why: Client won't do Looms (hard no from campaign feedback Jan 26, 2026)
```

---

## Change Log

| Date | Change | Source |
|------|--------|--------|
| YYYY-MM-DD | Added "No Looms" constraint | [VERIFIED: Campaign X revision feedback] |
| YYYY-MM-DD | Added "Clarify dual path" requirement | [VERIFIED: Campaign X revision feedback] |

---

## Related Knowledge

**See also:**
- [[front-end-offers]] - All approved offers for this client
- [[email-voice-and-tone]] - Writing style preferences
- [[value-prop-nodes]] - Core differentiators to emphasize
- [[anti-pattern-nodes]] - What NOT to do (system-wide learnings)

---

**Status:** canonical (updated with each campaign learning)
**Domain:** business
**Source:** [VERIFIED: client onboarding, campaign feedback, revision notes]
