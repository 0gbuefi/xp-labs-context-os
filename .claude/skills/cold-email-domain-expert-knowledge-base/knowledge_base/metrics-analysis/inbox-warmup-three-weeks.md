---
name: INBOX_WARMUP_THREE_WEEKS
description: Standard inbox warmup period of 3 weeks minimum before sending cold emails - establishes sending reputation
scope: agency
domain: metrics-analysis
node_type: pattern
status: canonical
created: 2026-01-15
last_updated: 2026-01-16
ingestion_count: 3
tags:
  - metrics-analysis
topics:
  - open-rate-signals
  - bounce-rate-analysis
related_concepts:
  - "[[inbox-volume-baseline-30-per-day]]"
  - "[[domain-structure-two-inboxes]]"
  - "[[batch-rotation-strategy]]"
  - "[[infrastructure-diversification-2-5x]]"
  - "[[deliverability-engagement-loop]]"
source: "GEX Wrapped 2024 by Eric Nowoslawski | Mitchell Keller - I Booked 2230+ Calls | Instantly.ai Cold Email Benchmark Report 2026"
source_url: " | https://youtube.com | https://instantly.ai"
date_accessed: "2026-01-15, 2026-01-16, 2026-01-16"
---

# Inbox Warmup: 3 Weeks Minimum

Warm up all new inboxes for **3 weeks minimum** before sending cold emails. Warmup establishes sending reputation by having inbox exchange emails with warmup pool before real campaigns launch.

## Core Principles

- **21-28 days minimum** (3-4 weeks) before going live
- 3 weeks = standard baseline (can extend to 6-8 weeks for extra safety)
- Warmup = automated email exchange with pool of other inboxes
- Builds sending reputation with Gmail/Outlook before cold sending
- Platforms like Instantly and Smartlead have built-in warmup
- Can reuse burned domains after 3 weeks of re-warming (sometimes)
- Longer warmup = better for reserve batches
- **Ramp warming gradually:** Start at 3 sends/day, scale to 20 over 3-day increments
- **Reply rate setting:** Configure 60-80% reply rate during warmup
- **Reserve infrastructure strategy:** Warm extra inboxes (51+ days) for rock-star performance

## When to Use

Warmup for 3 weeks when:
- Setting up new domains and inboxes
- Standard campaign launch (not emergency)
- Following conservative best practices
- Using inboxes for first time
- Re-warming previously burned inboxes (sometimes works)

**Warmup for 6+ weeks when:**
- Creating reserve batch (insurance capacity)
- May 2024-style deliverability crisis happens again
- Want maximum reputation before sending
- High-value campaign launch

## How to Apply

**Standard Warmup Process:**

**Week 1:**
- Connect inbox to Instantly/Smartlead
- Join warmup pool
- Automated emails sent/received between pool members
- Volume starts low, increases gradually

**Week 2:**
- Warmup volume continues increasing
- Inbox reputation building with email providers
- Still exchanging with warmup pool only

**Week 3:**
- Warmup volume at full level
- Inbox reputation established
- **Ready to send cold emails**

**Day 22+:**
- Begin cold email campaigns at 30/day

**Warmup Mechanics:**

Warmup tools work by:
1. Joining pool of other warming inboxes
2. Automatically emailing each other
3. Automatically responding to each other
4. AI-generated content (or random book paragraphs historically)
5. Marks emails as "not spam" and moves to inbox
6. Builds positive sending reputation

**GEX 2024 Deliverability Crisis:**

May-July 2024: Standard 3-week warmup wasn't working.
- New customers warmed 3 weeks → 20% open rates
- Old customers maintained 70% open rates
- Unknown cause (Google/Outlook crackdown?)

**GEX Response:**
Changed infrastructure to batch rotation system:

**Batch 1:** Google inboxes (warmup 3 weeks, use immediately)
**Batch 2:** Hypertide inboxes (warmup 8 weeks while Batch 1 sends)
**Batch 3:** More Google (warmup 12 weeks while Batch 1-2 send)
**Batch 4:** More Hypertide (warmup 16 weeks while Batch 1-3 send)

Result: Always have fresh, well-warmed inboxes in reserve.

**Batch Rotation Strategy:**

Setup 4× your needed volume:

Need 1,000 emails/day? Set up capacity for 4,000/day split into batches.

```
Week 0: Start warming all 4 batches
Week 3: Batch 1 ready (3 weeks warm)
Week 8: Batch 2 ready (8 weeks warm) - Batch 1 insurance
Week 12: Batch 3 ready (12 weeks warm) - Batch 1-2 insurance
Week 16: Batch 4 ready (16 weeks warm) - Batch 1-3 insurance
```

If you burn Batch 1, Batch 2 has been warming for 8 weeks (better than standard 3).

**Re-Warming Burned Domains:**

Pre-2024: Could let burned domain re-warm for 3 weeks, use again.

Post-2024 crisis: Less reliable, but GEX still maintains this strategy.

**Warmup vs. Real Campaign Copy:**

**Current:** Warmup sends AI-generated generic content.

**GEX Hypothesis (Future):** Will become important to warm up using actual campaign copy you'll send. Too many times they saw:
- 100% warmup reputation score
- Launch real campaign
- Deliverability drops

Only variable that changed: copywriting.

**Future recommendation:** Warm up with your actual email templates.

### Gradual Volume Ramp (Industry Standard)

**Instantly.ai recommendation:**

**Initial warmup protocol:**
- Start: 5-10 emails/day initially
- Ramp: Gradually increase over 4-6 weeks
- Signal: Legitimate sender (not spam operation overnight)
- Goal: Build reputation with email providers

**Why gradual:**
- Erratic volume kills deliverability
- Sending 500 Monday, nothing Tuesday-Thursday, then 1,000 Friday = suspicious
- Email providers learn to trust predictable patterns
- Sudden volume spikes trigger spam filters

**Campaign limits:**
Set daily send limits to maintain consistent volume that providers trust.

### Deliverability Non-Negotiables (Instantly.ai)

**Before launching campaigns, ensure these fundamentals are locked:**

**1. Infrastructure Distribution**
- Don't concentrate all volume on single domain
- Distribute sends across multiple domains
- Prevents overload triggering spam filters
- "Don't put all eggs in one basket"

**2. Bounce Rate Discipline**
- Keep below 2% (ideally much lower)
- Every bounce damages sender reputation
- Clean lists frequently
- Use email verification before sending
- Remove addresses that consistently bounce

**3. Engagement Signal Management**
- Providers watch: opens, replies, spam complaints
- High engagement = value signal
- Low engagement = spam signal
- Quality targeting/messaging directly impacts infrastructure health

**4. Domain Authentication**
- SPF, DKIM, DMARC properly configured
- Non-negotiable requirement
- Verifies authorization to send from domains
- Prevents spoofing
- Use done-for-you accounts to skip setup hassle

**5. Enterprise Gateway Awareness**
- Large companies use security layers (Proofpoint, Mimecast, Barracuda)
- Aggressively filter bulk senders
- Better to avoid these inboxes entirely
- Or have specific strategy for engaging them

**6. Catch-All Email Caution**
- Catch-all domains accept any email format
- Makes validation difficult
- Higher bounce risk
- Approach carefully or avoid entirely
- Instantly's verification handles catch-alls automatically

**7. Domain Rotation & Aging**
- Domains fatigue with heavy use
- Rest overused domains, bring back gradually
- Think: rotating crops (can't farm same field continuously)
- Maintains long-term health

**8. Inbox Placement Monitoring**
- Don't assume emails land in primary inbox
- Test across Gmail, Outlook, etc.
- Verify actual placement
- Catch deliverability drops early
- Prevents compounding damage

### The Engagement-Deliverability Loop

**Positive feedback loop:**
High engagement → better placement → even more engagement

**Negative feedback loop:**
Low engagement → worse placement → even lower engagement

**Why reply rate matters beyond conversion:**
Reply rate directly impacts inbox placement for future sends.

**Data insight:**
Teams maintaining stable domain health + consistent sending see **+15-20% higher replies**.

**Strategy shift:**
- Old: "How many can we send?"
- New: "How precisely can we target to maximize engagement?"

Optimize for engagement, not raw send volume.

## Evidence

[VERIFIED: GEX Wrapped 2024] "In 2024, we set up 2 inboxes per each domain and warmed the domain for 3 weeks. We started sending 30 emails per day and when we knew we had a good campaign we saw that we could get away with sending 50 emails per day."

[DATA: Pre-2024 re-warming] "I also found that if domains stopped working, you could let them warm up for another 3 weeks and use them again."

[DATA: 2024 crisis] "On May 1st it felt like everything changed. Outlook accounts were getting banned en masse. We would onboard customers, warm up their domains for 3 weeks and couldn't get past a 20% open rate. Old domains weren't working either."

[DATA: Batch strategy response] "Now, we estimate how many emails per day a customer is going to be sending and we set up 3 or 4 iterations of that volume... We set up batches like this and start warming them all at the same time. This way everything at least warms up for 3 weeks. If we burn the Google inboxes, now their Hypertide inboxes may have warmed up for 8 weeks."

[VERIFIED: Warmup copy hypothesis] "I think it will become more and more important to use the actual email copywriting you will be using in your campaign to warmup the emails. We've just seen too many times that we get 100% reputation in smartlead or instantly from the warmup pool and then when we launch we have lower delivery. The only variable that changed is the copywriting being sent."

[VERIFIED: Mitchell Keller - NEW] "You want your warming phase to be 21 to 28 days, but the longer the better. If you can afford to warm for longer, I would recommend doing that."

[DATA: Ramping protocol - NEW] "You ramp your warming every 3 days and you do that on repeat until you reach 20 sends per day with your warming. Start at three, scale to 20, increase by about three per time that you increase the amount... Set your reply rate to between 60 and 80%."

[DATA: Reserve infrastructure strategy - NEW] "If you send day one with half your infrastructure or less than half, you can then send at day 30 with infrastructure that has now been warming for 51 days, that infrastructure is going to perform like a rock star. That's where we see 4 to 8% reply rates."

[DATA: Pattern confirmed across 2 sources] Both GEX and Mitchell Keller independently confirm 21-28 day (3-4 week) warmup minimum with longer being better for performance.

[VERIFIED: Instantly.ai Benchmark Report 2026 - NEW] "Gradual Domain Warm-Up: New sending domains need time to build a reputation. Starting slow with 5-10 emails per day initially, then gradually increasing over 4-6 weeks signals to email providers that you're a legitimate sender, not a spam operation firing up overnight."

[DATA: Consistency requirement - NEW] "Erratic volume kills deliverability. Sending 500 emails Monday, nothing Tuesday-Thursday, then 1,000 Friday looks suspicious. Set campaign limits to maintain predictable daily volumes that email providers learn to trust."

[DATA: Bounce discipline - NEW] "Keep bounce rates below 2% (ideally much lower). Every bounced email damages your sender reputation."

[DATA: Engagement loop - NEW] "Consistency pays: Teams that keep domain health stable and send consistently see +15–20% higher replies in our dataset."

[DATA: Pattern confirmed across 3 sources] GEX, Mitchell Keller, and Instantly.ai all independently confirm gradual warmup over 3-6 weeks with consistent volume as foundation for deliverability.

## Related Concepts

- [[inbox-volume-baseline-30-per-day]] - Volume to send after warmup complete
- [[domain-structure-two-inboxes]] - Domain setup for warmup
- [[batch-rotation-strategy]] - Advanced warmup strategy with reserve capacity
