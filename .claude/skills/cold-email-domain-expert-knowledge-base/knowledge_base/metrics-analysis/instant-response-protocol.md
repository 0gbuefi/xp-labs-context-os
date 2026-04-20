---
name: INSTANT_RESPONSE_PROTOCOL
description: Respond to engaged leads instantly like your life depends on it - set up alerts and drop everything to reply and call immediately
scope: agency
domain: metrics-analysis
node_type: pattern
status: emergent
created: 2026-01-16
last_updated: 2026-01-16
ingestion_count: 1
tags:
  - metrics-analysis
topics:
  - reply-rate-analysis
  - meeting-conversion
related_concepts:
  - "[[phone-enrichment-calling-frame]]"
  - "[[8-percent-reply-rate-winner]]"
  - "[[loom-intro-offer-fallback]]"
source: "Mitchell Keller - I Booked 2230+ Calls In 2025"
source_url: "https://youtube.com"
date_accessed: "2026-01-16"
---

# Instant Response Protocol

Respond to engaged leads **instantly** - drop everything when notification comes in. Speed of response dramatically impacts conversion from reply to booked meeting.

## Core Principles

- **Response speed = conversion rate** - faster response = higher booking rate
- **Instant alerts required** - Slack, webhook, or phone notification
- **Drop everything** - treat like emergency
- **Call after replying** - enrich phone, call immediately
- **Set the frame** - "My assistant told me you were interested"
- **Book same-day if possible** - momentum is everything
- **Follow up relentlessly** - especially if they already said yes

## When to Use

Use instant response protocol for:
- All positive replies from cold campaigns
- High-intent signals ("yes," "interested," "tell me more")
- High-value prospects (enterprise, large deal size)
- Competitive markets where speed wins
- When booking rates are low and need improvement

## How to Apply

### Step 1: Set Up Alerts

**Slack integration (recommended):**

Most ESPs have native Slack integrations:
- Instantly → Slack
- Smartlead → Slack
- Email Bison → Slack

**Setup:**
1. Connect ESP to Slack workspace
2. Create dedicated #replies channel
3. Configure alert for positive replies only
4. Enable mobile notifications for that channel

**Alternative - Webhook:**

If Slack doesn't work:
1. Set up webhook in ESP
2. Route to notification service (Telegram, Discord, etc.)
3. Use ChatGPT/Claude/Gemini to help configure

**Mitchell quote:**
"If Slack doesn't work, use the web hook to alert yourself somewhere else. If you can't figure that out, ChatBT, Claude, Gemini, they will do it for you. We're in the world of AI, it is wonderful, wonderful place to be."

### Step 2: Immediate Enrichment

**When alert fires:**

Before replying, enrich contact information (if not already done):

**Phone enrichment via API:**
- Use Lead Magic API
- Automatically enrich phone number on reply trigger
- Route enriched data to Slack notification
- Have phone number ready when you go to reply

**Example automation:**
```
Reply comes in
→ Trigger Lead Magic API: enrich phone
→ Send to Slack: "[Name] replied + phone: [number]"
→ You see notification with everything needed
```

### Step 3: Reply Immediately

**Response template structure:**

**If using persona/assistant name:**
```
Hey [first name],

Glad to hear you're interested! [Quick 1-2 sentence
acknowledgment of their reply]

[Brief next step]

I'll give you a call in the next few minutes to discuss.

[Your name]
```

**Keep it short:**
- Acknowledge their interest
- Confirm you're following up
- Set expectation for call

### Step 4: Call Immediately After Replying

**Calling software options:**
- WhatsApp (if nothing else)
- Zoom Phone
- OpenPhone (Mitchell's choice - easy API)

**Frame-setting script:**

**Opening:**
```
"Hey [first name], it's [your name]. My assistant told me you
were interested in [offer/topic], so wanted to give you a
quick call just before I head out the door to my next
appointment."
```

**Why this works:**
- Establishes hierarchy (assistant → you)
- Creates time pressure (heading to appointment)
- Frames them as interested party (not cold call)
- Warm, not salesy

**Confirmation:**
```
"I think you were saying that [restate their interest/pain].
Is that right?"
```

Gets them to confirm and elaborate.

**Transition to value:**
```
"Yeah, so to be honest, we've been helping a few people kind
of like you with [outcome], but I'm not really sure if it's
even a fit for your current situation."
```

- Consultant positioning (not salesperson)
- "Not sure if it's a fit" = disqualification frame
- Makes them want to prove they ARE a fit

**Soft close to meeting:**
```
"What we typically do is a short consult where I look at what
you're doing, give you some things from best practices that
we've seen with [client X and Y], and then we can just have a
quick conversation to see if you're a fit for the system that's
worked for all these other people."
```

**Ask for meeting:**
```
"Does that sound okay for tomorrow?"
```

**Create urgency:**
```
"Tomorrow? I'm looking at my calendar here. I've got 2 and 3
p.m. ET. Does 2 p.m. work?"
```

- Assume they want tomorrow
- Give specific times (not "when works for you")
- Make them choose between options (both soon)

**Confirm details:**
```
"Perfect. And the same email my assistant was talking to you
on is [email]? Great. I'll send you a calendar invite."
```

### Step 5: Follow Up Relentlessly

**If they don't pick up:**
- Leave voicemail referencing email conversation
- Send text with same framing
- Email again with value
- Try at different times of day

**If they agree to meeting but don't confirm time:**

**Do not stop following up until they book.**

**Follow-up strategies:**

**Value-based:**
```
"Hey [name], wanted to send over this [relevant resource]
while you think about timing. Let me know what works."
```

**Humor-based:**
```
"[Name] - following up because I'm persistent, not annoying
(I hope 😅). Still interested in [outcome]?"
```

**Loom video:**
```
"Hey [name], recorded a quick Loom showing [specific insight
for their situation]. [Link]. Also - still good for that call?"
```

**High-value leads = video follow-ups:**

For very qualified leads:
- Send relevant YouTube video you created
- Send Loom with specific insight
- Send case study of similar business
- Deanonymize their website visitors and send as value

Mitchell: "Hey man, here's a video of a similar business that we did some stuff with. Hey man, I noticed that you guys have a lot of website visitors. Here's how you can turn them into campaigns to send to by deanonymizing them."

### Step 6: Newsletter Opt-In

**If they're engaged but not ready to book:**

Opt them into your newsletter:
- Convert sales call transcripts to newsletter content
- Value-bomb them into submission
- Send best-performing content expanded with AI
- Keep them warm until ready

**Booking rate optimization:**

Mitchell's data:
"This is going to be the number one way to get your booking rates from rock bottom up to 30, 40, and even as high as 50% depending on your offer."

## Evidence

[VERIFIED: Mitchell Keller] "When they respond, you need to respond as fast as possible. You literally need to be a nice guy experiencing sexing for the first time. Like your turnaround time is going to be absolutely instantaneous. You're going to drop everything. Buzz buzz. I need to jump on this."

[DATA: Alert setup] "To do this, set up Slack alerts. Almost every ESP has native Slack integrations to make sure you can alert yourself."

[DATA: Phone enrichment] "From there, you want to immediately enrich their phone number. This is where lead magic comes in handy. You can set up a simple API request to enrich the phone number of the lead as the reply comes in and route that to your Slack channel so that when you go to reply, you can immediately call them after."

[VERIFIED: Frame setting] "Set the frame by saying, 'My assistant told me you were interested in X.' Something like this. Hey, uh, first name. Oh, yeah. Yeah, it's it's Mitch. My assistant told me you were interested in X, so wanted to give you a quick call just before I head out the door to my next appointment."

[DATA: Booking rate impact] "This is going to be the number one way to get your booking rates from rock bottom up to 30, 40, and even as high as 50% depending on your offer."

[VERIFIED: Relentless follow-up] "Do not stop following up until they agreed to a meeting, especially if they already said yes to a meeting. This is very important. Follow up with value, humor, and just generally to get them on a call."

## Related Concepts

- [[phone-enrichment-calling-frame]] - Detailed calling framework and scripts
- [[8-percent-reply-rate-winner]] - Getting replies is step 1, converting them is step 2
- [[loom-intro-offer-fallback]] - Using video for follow-up and value delivery
