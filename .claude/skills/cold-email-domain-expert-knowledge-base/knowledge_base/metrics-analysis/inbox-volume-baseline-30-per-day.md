---
name: INBOX_VOLUME_BASELINE_30_PER_DAY
description: Standard baseline of 30 emails per day per inbox for cold email deliverability and spam avoidance
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
  - "[[spam-rate-primary-metric]]"
  - "[[inbox-warmup-three-weeks]]"
  - "[[domain-structure-two-inboxes]]"
source: "GEX Wrapped 2024 by Eric Nowoslawski"
source_url: ""
date_accessed: 2026-01-15
---

# Inbox Volume Baseline: 30 Emails Per Day

The industry-standard baseline for cold email sending is **30 emails per day per inbox**. This volume balances deliverability, spam avoidance, and scalability while staying well below Google Workspace's 2,000/day limit.

## Core Principles

- Start at 30 emails/day after 3-week warmup
- Scale to 50 emails/day only after proven campaign success
- Maintain 10-minute minimum delay between sends
- Spam complaints matter more than volume limits
- Scale horizontally (more inboxes) not vertically (more volume per inbox)

## When to Use

Use 30 emails/day baseline when:
- Launching new inboxes after warmup period
- Running first campaigns for new clients
- Testing new messaging or offers
- Uncertain about spam complaint rates
- Following conservative deliverability practices

## How to Apply

**Standard Setup:**
1. Warm inbox for 3 weeks minimum
2. Start sending 30 emails/day
3. Monitor spam complaints and deliverability
4. If campaign performs well (low spam rate), test scaling to 50/day
5. If deliverability declines, return to 30/day or lower

**Volume Scaling Decision:**
```
IF spam_complaint_rate < 0.5% AND campaign_working:
    test_volume_increase_to_50_per_day()
ELSE:
    maintain_30_per_day()
```

**Example:**
GEX tested sending 1,000 emails from one inbox in one day to an opted-in list. The email still inboxed the next day. Lesson: **Spam complaints matter more than volume**. But 30/day remains the safe starting point for cold outreach.

## Evidence

[VERIFIED: GEX Wrapped 2024] "We set up 2 inboxes per each domain and warmed the domain for 3 weeks. We started sending 30 emails per day and when we knew we had a good campaign we saw that we could get away with sending 50 emails per day."

[DATA: Volume experiment] Sent 1,000 emails in one day from single inbox to opted-in list - still inboxed next day. Proves spam rate is primary factor, not volume.

[DATA: Google limit] Google Workspace official limit is 2,000 emails/day, but 30/day prevents spam complaints.

## Related Concepts

- [[spam-rate-primary-metric]] - Why spam complaint rate matters more than volume
- [[inbox-warmup-three-weeks]] - Required warmup before sending at baseline volume
- [[domain-structure-two-inboxes]] - Domain setup with 2 inboxes to distribute volume
