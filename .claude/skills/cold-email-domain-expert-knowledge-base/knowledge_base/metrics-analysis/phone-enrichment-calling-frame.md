---
name: PHONE_ENRICHMENT_CALLING_FRAME
description: Enrich phone numbers immediately on reply and use persona-based frame-setting script to convert to meetings
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
  - meeting-conversion
  - reply-rate-analysis
related_concepts:
  - "[[instant-response-protocol]]"
  - "[[front-end-offer-strategy]]"
  - "[[8-percent-reply-rate-winner]]"
source: "Mitchell Keller - I Booked 2230+ Calls In 2025"
source_url: "https://youtube.com"
date_accessed: "2026-01-16"
---

# Phone Enrichment + Calling Frame

Enrich phone numbers automatically when prospect replies, then immediately call using **persona-based frame** ("my assistant told me...") to convert warm leads into booked meetings.

## Core Principles

- **Phone = higher conversion** than email-only follow-up
- **Enrich automatically** via API on reply trigger
- **Call immediately after replying** (not hours later)
- **Frame with persona** - "assistant told me" if using fake persona
- **Time pressure** - "heading to my next appointment"
- **Consultant positioning** - "not sure if it's a fit"
- **Tomorrow bias** - assume they want to meet tomorrow
- **Specific time slots** - don't ask "when works," give 2 options

## When to Use

Use phone calling strategy when:
- Prospect replied positively to email
- High-value opportunity (enterprise, large deal)
- Booking rates need improvement
- Email-only follow-up isn't converting
- Want 30-50% booking rates

## How to Apply

### Phone Enrichment Setup

**API integration (Lead Magic example):**

```
1. Prospect replies to cold email
2. Trigger webhook/automation
3. Call Lead Magic API with prospect email
4. Receive phone number
5. Route to Slack notification
6. You see: "[Name] replied + phone: [number]"
```

**Tools:**
- Lead Magic (recommended for enrichment + validation)
- OpenPhone (Mitchell's choice for calling - easy API)
- WhatsApp (fallback if no calling software)
- Zoom Phone (alternative)

### Frame-Setting Script

**Opening (persona-based):**

If using fake persona (assistant/intern name in email signature):

```
"Hey [first name], it's [your real name - founder/owner].
My assistant [persona name] told me you were interested in
[offer topic], so wanted to give you a quick call just before
I head out the door to my next appointment."
```

**Why this works:**
- Reveals you're the founder (frames hierarchy)
- "Assistant" confirms legitimacy of outreach
- Time pressure ("heading to appointment")
- Positions them as warm lead, not cold call

**Confirmation + elaboration:**

```
"I think you were saying that [restate their pain/interest
from email]. Is that right?"
```

Let them talk. Confirm pain point. Build rapport.

**Consultant positioning:**

```
"Yeah, so to be honest, we've been helping a few people kind
of like you with [outcome], but I'm not really sure if it's
even a fit for your current situation."
```

**Key psychology:**
- "Not sure if it's a fit" = disqualification frame
- Makes them want to prove they ARE qualified
- Consultant vs salesperson positioning

**Soft close to discovery call:**

```
"What we typically do is a short consult where I look at what
you're doing, give you some things from best practices that
we've seen with [client X and Y], and then we can just have a
quick conversation to see if you're a fit for the system that's
worked for all these other people."
```

**Ask for meeting (assume tomorrow):**

```
"Does that sound okay for tomorrow?"
```

Don't ask "when are you free?" - creates friction.

**Create urgency with specific times:**

```
Prospect: "Tomorrow?"

You: "Yeah, tomorrow. I'm looking at my calendar here. I've got
2 and 3 p.m. ET. Does 2 p.m. work?"
```

**Confirm email:**

```
"Perfect. And the same email my assistant was talking to you
on is [their email]? Great. I'll send you a calendar invite
right now."
```

### Persona Strategy Benefits

**Why use fake personas (assistant names, random names):**

Mitchell uses "fake personas" - Latina names + AI-generated profile photos.

**Benefits:**

1. **Reputation protection:**
   - If messaging is off during testing, blame "new assistant"
   - If sequence mistake happens, not your fault
   - Protects founder/company reputation

2. **Frame-setting flexibility:**
   - Can position founder as busy, important
   - "My assistant manages outreach"
   - Sets hierarchy in prospect's mind

3. **Calling advantage:**
   - Founder calling = instant credibility boost
   - "Assistant" made initial contact, founder following up
   - Feels like VIP treatment

**Example persona setup:**
```
Email from: Maria Gonzalez <maria@yourcompany.com>
Signature: Maria | Lead Generation Assistant

Phone call from: [Your Name] (Founder)
"Hey, Maria told me you replied..."
```

### If They Don't Answer

**Voicemail script:**

```
"Hey [first name], it's [your name] from [company]. My
assistant [name] emailed you about [topic] and you replied
saying [their response]. I tried calling to discuss - I'll
send you a text and email as well. Looking forward to
connecting!"
```

**Text message:**

```
"Hi [first name], [your name] here from [company]. Tried
calling about [topic] - want to grab 15 min tomorrow?
I've got 2 and 3 p.m. Let me know!"
```

**Email follow-up:**

Include value (Loom, case study, insight) + meeting ask.

## Evidence

[VERIFIED: Mitchell Keller] "You want to immediately enrich their phone number. This is where lead magic comes in handy. You can set up a simple API request to enrich the phone number of the lead as the reply comes in and route that to your Slack channel so that when you go to reply, you can immediately call them after."

[DATA: Calling software] "For calling software, feel free to use something like WhatsApp if you don't have anything else. Use Zoom calls if you'd like. But for my business, we use Open Phone because it's easy and accessible and it has a very open API."

[VERIFIED: Frame setting script] "Set the frame by saying, 'My assistant told me you were interested in X.' Something like this. Hey, uh, first name. Oh, yeah. Yeah, it's it's Mitch. My assistant told me you were interested in X, so wanted to give you a quick call just before I head out the door to my next appointment."

[DATA: Warm calling script] "Uh, I think you were saying that XYZ. Is that right? Oh, yeah, that's right. Yeah. So to be honest, yada yada go through your kind of warm calling script and basically what you want to say throughout that script is um yeah, you know, we we've been helping a few people kind of like you with outcome, but I'm not really sure if if it's even a fit for your current situation."

[VERIFIED: Meeting close] "What we typically do is a short a short consult where I I look at what you're doing, give you some some things from best practices that we've seen with client X and Y. Uh, and then and then we can just have a a a quick conversation to see if you're a fit for the system that's worked for, you know, all these other people. Does that sound okay for tomorrow?"

[DATA: Persona strategy] "If you're like us, I would even recommend that you use fake personas. These can just be random Latina names and some nano banana generated images. The reason you may want to do this is because by doing this, you can actually protect your reputation. All of a sudden, any mistake that happens in your sequencing, especially early on, can just be chocked up to, or if your messaging is off while you test, can just be chocked up to an assistant making a silly mistake or an intern or a new hire."

## Related Concepts

- [[instant-response-protocol]] - Speed of response framework
- [[front-end-offer-strategy]] - What to offer on the call
- [[8-percent-reply-rate-winner]] - Getting the replies that trigger this process
