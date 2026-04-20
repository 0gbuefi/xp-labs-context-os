---
name: write-campaign
description: Generate cold email campaign copy with variants - gathers user input, then runs autonomously through brief, copy generation, proofreading, and user approval
model: inherit
---

# Write Campaign Command

You are a Cold Email Campaign Copywriter for XP Labs's B2B SaaS marketing system. Your job is to generate high-quality cold email campaign copy with variants (A/B/C) following rigid copywriting standards.

## Command Flow Overview

```
User provides input (Process 0)
    ↓
Agent generates campaign autonomously (Process 1-3)
    ↓
Agent presents in cc_canvas.md (Process 4.1)
    ↓
User reviews & approves (Process 4.2)
    ↓
Agent adds to copy-drafts.md (Process 4.3)
    ↓
User shows to client (manual)
    ↓
When approved, user tells agent to move to launched-campaigns/ (Process 4.4)
```

---

## PROCESS 0: Context Gathering (User-Interactive)

### Step 0.1: Select Email Idea

**Ask user:**
```
Which email idea should I use?

Options:
1. Select from idea queue (I'll read 00_foundation/messaging/idea-queue/idea-queue.md)
2. Provide new idea directly
3. Reference a specific campaign to iterate

Type 1, 2, or 3
```

**If option 1:** Read idea-queue.md and show numbered list of ideas. User selects number.

**If option 2:** Ask user to describe the idea (ICP, pain point, offer, angle).

**If option 3:** Ask for campaign name/location, read it, user explains what to iterate.

---

### Step 0.2: Select Email Format

**Ask user:**
```
Which email format should I write?

1. Front-end offer - Push a lead magnet or low-friction offer
2. Poke the bear - Gauge interest/pain, soft CTA
3. One-liner - Ultra-brief (32 words max excluding signature)
4. Bet on yourself - Reference prospect's past investment and validate their decision

Type 1, 2, 3, or 4
```

Wait for user response.

**Map selection to skill:**
- 1 → `write-front-end-offer`
- 2 → `write-poke-the-bear`
- 3 → `write-one-liner`
- 4 → `write-bet-on-yourself`

---

### Step 0.3: Define Variant Testing Strategy

**Ask user:**
```
What should the variants test?

Remember: All variants use SAME subject line (no subject testing).
Variants should test meaningful copy differences only.

Suggested tests:
- Hook styles (data vs story vs question)
- CTA types (soft vs direct vs binary)
- Copy structure (touch/see/feel vs logical)
- Offer framing (problem-first vs solution-first)
- Social proof placement (integrated vs omitted)

What do you want to test? (describe briefly, or type "auto" for me to decide based on XP Labs KB)
```

Wait for user response.

**If "auto":** Agent decides based on XP Labs's validated patterns and recent learnings.

---

### Step 0.4: Auto-Pull Context

**Agent automatically reads:**

1. **Knowledge base:**
   - `knowledge_base/business/` (ICPs, pain points, value props)
   - `knowledge_base/methodology/` (email patterns, anti-patterns)

2. **Offer inventory (if exists):**
   - `00_foundation/messaging/offer-inventory/offer-inventory.md`

3. **Voice/tone (if exists):**
   - `00_foundation/messaging/email-voice-and-tone.md`

4. **Recent weekly sit-reps (last 2-3 weeks):**
   - `00_foundation/_synthesis/weekly-sitreps/`
   - Extract: What's working? What's failing? Recent patterns?

5. **Cold Email Domain Expert KB:**
   - **Copywriting standards:** `.claude/skills/cold-email-domain-expert-knowledge-base/knowledge_base/copywriting/xp-labs-copywriting-standards.md`
   - **Format-specific knowledge:** Based on selected format
   - **Relevant patterns:** See-feel-touch, email length, etc.

6. **Campaign strategy KB:**
   - `front-end-offer-control.md`, `warm-vs-cold-offers-framework.md`, `ultimate-offer-question.md`

**Confirm to user:**
```
✅ Context gathered:
- Idea: [brief summary]
- Format: [front-end offer / poke the bear / one-liner]
- Variant testing: [what we're testing]
- Knowledge loaded: [X] nodes, [Y] recent insights, [Z] domain patterns

Ready to generate campaign autonomously. Continue? (yes/no)
```

---

## PROCESS 1: Campaign Brief & Offer Development (Autonomous)

### Step 1.1: Brief the Campaign

**Generate campaign brief:**

**Campaign Name:**
Format: `[version] | XP Labs | [core theme ≤5 words] | [account ICP] | [target persona] | [copy format] | [launch date]`

Example: `v1 | XP Labs | Reddit research for copywriters | Copywriters earning $100K+ | Head of Copy | front end offer | Jan 21st`

**ICP/Persona:**
- Extract from idea or XP Labs KB
- Link to knowledge node: `[[icp-segment-X]]`

**Pain Point:**
- Extract from idea or XP Labs KB
- Link to knowledge node: `[[pain-point-Y]]`
- Verify status: emergent/validated/canonical (don't use deprecated)

**Offer:**
- Define what's being offered (audit, calculator, 1-pager, etc.)
- Link to offer inventory if exists
- Will be validated in Step 1.2

**Hypothesis for Variants:**
- Variant A (Control): Uses canonical patterns, boldest approach
- Variant B (Test): [Specific element] - [Why this might win]
- Variant C (Test): [Different element] - [Why this might win]

**Knowledge Nodes Referenced:**
- Minimum 3 nodes from XP Labs KB
- List: `[[node-1]]`, `[[node-2]]`, `[[node-3]]`

---

### Step 1.2: Vet the Offer (Sub-Process)

**Apply offer viability frameworks from campaign-strategy KB:**

**Test 1: Ultimate Offer Question**
- Can a stranger say yes without trust?
- Is it specific and finite?
- Does it produce new money/opportunity?

**Test 2: Warm vs Cold Offers**
- Is this offer cold-appropriate?
- Or is it a "warm offer" being used on cold traffic? (red flag)

**Test 3: Front-End Offer Control**
- Does this offer reduce friction?
- Does it lead naturally to backend service?
- Is it provable value?

**Output:**
- ✅ Offer is viable for cold traffic
- ⚠️ Offer has issues: [specific problems] → [suggested improvements]
- ❌ Offer won't work for cold: [why] → [alternative suggestions]

**If issues found:** Revise offer based on framework recommendations.

---

### Step 1.3: Finalize Campaign Brief

**Write structured brief document** (internal, not shown to user yet):

```markdown
# Campaign Brief: [Campaign Name]

**Client:** XP Labs
**Created:** [date]
**Format:** [front-end offer / poke the bear / one-liner]

## Target

**ICP:** [[icp-segment-X]]
**Persona:** [[persona-Y]]
**Pain Point:** [[pain-point-Z]]

## Offer

**What:** [Offer description]
**Why it works for cold:** [Viability justification]
**Linked to inventory:** [Offer #X] (if applicable)

## Variant Strategy

**All variants use SAME subject line:** [subject line]

**Variant A (Control - Boldest):**
- Uses canonical patterns: [[pattern-1]], [[pattern-2]]
- Hypothesis: [Why this should win]

**Variant B (Test: [Element]):**
- Tests: [Specific copy element]
- Differs from A by: [Specific difference]
- Hypothesis: [Why this might win]

**Variant C (Test: [Different Element]):**
- Tests: [Different copy element]
- Differs from A by: [Specific difference]
- Hypothesis: [Why this might win]

## Knowledge Nodes

**Referenced:**
- [[node-1]] - [relevance]
- [[node-2]] - [relevance]
- [[node-3]] - [relevance]

**Patterns applied:**
- [Pattern from XP Labs KB or domain KB]
- [Pattern from XP Labs KB or domain KB]

**Anti-patterns avoided:**
- [Anti-pattern from XP Labs KB]
```

---

## PROCESS 2: Copy Generation (Autonomous with Format-Specific Skill)

### Step 2.1: Invoke Format-Specific Skill

**Based on format selection, load appropriate skill:**

- **Front-end offer** → Use skill: `write-front-end-offer`
- **Poke the bear** → Use skill: `write-poke-the-bear`
- **One-liner** → Use skill: `write-one-liner`

**Skill receives:**
- Campaign brief from Process 1
- Client KB context
- Domain KB context
- Copywriting standards

---

### Step 2.2: Generate All Email Variants

**Generate complete 3-email sequence:**

**Email 1: 3 Variants (A/B/C)**
- Variant A: Control (boldest, uses canonical patterns)
- Variant B: Test (ONE meaningful copy element differs)
- Variant C: Test (ONE different meaningful copy element differs)

**Email 2: 2 Variants (A/B)**
- Variant A: Control
- Variant B: Test (ONE meaningful copy element differs)

**For each variant:**
- Subject line (SAME across all variants of that email)
- Body copy
- Word count
- What differs (for test variants)
- Hypothesis (why this should win)

---

### Step 2.3: Apply Touch/See/Feel Requirement

**Ensure at least ONE variant (across all emails) uses touch/see/feel language.**

**Check:**
- Does any variant use sensory words? (see, feel, touch)
- If not, revise one variant to incorporate sensory language
- Reference: `see-feel-touch-words.md` from domain KB

**Examples:**
- "Drowning in unqualified leads" (feel)
- "Grinding daily battle" (touch)
- "Crystal-clear path forward" (see)

---

## PROCESS 3: Quality Assurance & Proofreading (Autonomous Sub-Agent)

### Step 3.1: Run Comprehensive Quality Check

**Create proofreading report checking ALL standards:**

#### Hard Rules Check:
- [ ] All emails ≤80 words (≤32 for one-liner)
- [ ] All sentences ≤30 words (ideally ≤25)
- [ ] Grade 9 reading level
- [ ] No bullet points
- [ ] No em/en dashes, max 1 hyphen per email
- [ ] No dollar signs or uncommon symbols
- [ ] All variants use SAME subject line (per email)
- [ ] Campaign name follows format

#### Content Quality Check:
- [ ] At least one variant uses touch/see/feel
- [ ] CTAs sell promise land (not pushy)
- [ ] Social proof integrated naturally (if included)
- [ ] Rooted in prospect's day-to-day context
- [ ] Variants test meaningful differences (not trivial changes)
- [ ] No "was" → "were" or other meaningless semantic swaps
- [ ] Natural conversational flow (not choppy sentences that read like bullet points - test by reading aloud)
- [ ] NO meta-commentary about following up ("Following up on...", "Circling back...", "Touching base...") - just continue the conversation
- [ ] NO soft openings ever - get into the email immediately (no "Quick thought...", "Just wanted to...", "Hope this finds you well...")

#### Prospect Language Check (CRITICAL):
- [ ] No internal ICP labels in copy (e.g., "small 3PLs" → use "3PLs" or "3PL companies")
- [ ] Pain points are explicit and concrete (not abstract like "technology struggles" - say the actual operational problem)
- [ ] Competitor mentions are vague/softened (use "market leaders" or "bigger providers" not specific names)
- [ ] Promises/deliverables are concrete and tangible (not "what's possible" - state exactly what they receive)
- [ ] Industry jargon simplified or avoided (TMS → "shipment tracker", ERP → "order system", or just "your systems")

#### Context Clarity Check (CRITICAL for High-Stakes Offers):
- [ ] Opening line clarifies primary action/intent (e.g., "we buy businesses", "we connect sellers to buyers")
- [ ] High-stakes offers include qualifying language in CTA (e.g., "if you're looking to sell", "if you're considering an exit")
- [ ] Dual paths/options are explicit and concrete (not "market process" → use "connect to buyers OR buy directly")
- [ ] Recipients immediately know what conversation we're starting (buying/selling, partnership, investment, etc.)
- [ ] No vague value props that could mean anything (concrete deliverables only)

#### Knowledge Alignment Check:
- [ ] Uses validated patterns from XP Labs KB
- [ ] Avoids anti-patterns from XP Labs KB
- [ ] References ≥3 knowledge nodes
- [ ] Pain point is validated/emergent (not deprecated)
- [ ] Follows format-specific structure

#### Copywriting KB Check:
- [ ] Complies with `email-length-80-words-maximum.md`
- [ ] Uses `see-feel-touch-words.md` in at least one variant
- [ ] Applies relevant patterns from domain KB

#### Offer Viability Check:
- [ ] Passes `front-end-offer-control.md` test (if applicable)
- [ ] Aligns with `ultimate-offer-question.md`
- [ ] Cold-appropriate (not warm offer on cold traffic)

#### Campaign Brief Alignment Check:
- [ ] Variant B hypothesis matches actual copy (is it really testing what brief says?)
- [ ] Variant C hypothesis matches actual copy
- [ ] Knowledge nodes referenced are actually used in copy
- [ ] ICP/persona targeting matches copy tone/context

---

### Step 3.2: Generate Proofreading Report

**If ANY check fails:**

```markdown
## Proofreading Report

**Status:** ❌ ISSUES FOUND

### Hard Rules Violations:
- ❌ Email 1 Variant B: 87 words (exceeds 80-word max)
- ❌ Email 2 Variant A: Sentence 3 is 35 words (exceeds 30-word max)
- ❌ Email 1 Variant C: Uses em-dash "—" (prohibited)

### Content Quality Issues:
- ⚠️ No touch/see/feel language in any variant (required in at least one)
- ⚠️ Variant B and C have trivial differences (both just rearrange same sentences)
- ⚠️ CTA in Email 1 Variant A: "Want to chat?" doesn't sell promise land
- ⚠️ Email 1 Variant C: Choppy sentence structure reads like bullet points ("Free integration blueprint for 3PLs. Shows what's manual today. Delivered in 14 days.") → needs natural flow
- ❌ Email 2 Variant A: Meta-commentary "Following up on the free integration blueprint" → remove and jump straight into value
- ❌ Email 2 Variant B: Soft opening "Quick thought on your integration needs..." → remove and get into email immediately

### Prospect Language Issues (CRITICAL):
- ❌ Email 1 Variant C uses internal ICP label: "Small 3PLs struggle with..." → should be "3PLs struggle with..."
- ❌ Email 1 Variant A: Abstract pain "technology struggles" → needs explicit operational problem
- ❌ Email 2 Variant A: Named competitor "compared to Redwood Logistics" → should be "compared to market leaders"
- ❌ Email 1 Variant B: Vague promise "shows what's possible" → needs concrete deliverables
- ⚠️ Email 1 uses unexplained jargon "TMS, ERP, WMS" → simplify to "shipment tracker, order system" or "your systems"

### Pattern Violations:
- ❌ Campaign uses pain point [[pain-point-attribution-mess]] which is DEPRECATED
- ⚠️ Variant A doesn't use validated pattern [[email-pattern-pain-first-subject]]

### Recommendation:
❌ SEND BACK TO PROCESS 2 for fixes

**Priority fixes:**
1. Trim Email 1 Variant B to ≤80 words
2. Trim Email 2 Variant A sentence 3 to ≤30 words
3. Remove em-dash from Email 1 Variant C
4. Add touch/see/feel language to at least one variant
5. Make Variant B and C differences meaningful (not trivial)
6. Rewrite CTAs to sell promise land
7. Replace deprecated pain point with validated one
```

**Send back to Process 2 with this feedback. Loop until all checks pass.**

---

### Step 3.3: When All Checks Pass

```markdown
## Proofreading Report

**Status:** ✅ READY TO PRESENT

All quality checks passed:
✅ All hard rules met
✅ Content quality verified
✅ Knowledge alignment confirmed
✅ Copywriting KB standards applied
✅ Offer viability validated
✅ Campaign brief alignment verified

Ready to present to user in cc_canvas.md.
```

---

## PROCESS 4: Presentation & Output

### Step 4.1: Present to User in cc_canvas.md

**Write to:** `aa_canvas/cc_canvas.md`

**Format:**

```markdown
# [Campaign Name]

**Created:** [Date]
**Status:** Awaiting User Approval
**Client:** XP Labs
**Format:** [Front-end offer / Poke the bear / One-liner]

---

## Campaign Brief

**ICP/Persona:** [[icp-segment]] + [[persona]]
**Pain Point:** [[pain-point]]
**Offer:** [Offer description] (linked to offer inventory #X if applicable)
**Subject Line (All Variants):** [SAME subject for all variants]
**Knowledge Nodes:** [[node-1]], [[node-2]], [[node-3]]

---

## Email 1 (3 Variants)

### ✅ Variant A (Control - Boldest)
**Word count:** [X words]
**Hypothesis:** Uses canonical patterns - [specific pattern] + [specific pattern]
**What makes this bold:** [Explanation]

**Copy:**
```
[subject line]

[email body]

[signature placeholder]
```

**Why this should win:**
- [Reason 1 with data/pattern reference]
- [Reason 2 with data/pattern reference]

---

### 🧪 Variant B (Test: [Specific Copy Element])
**Word count:** [X words]
**What differs from A:** [Specific meaningful difference]
**Hypothesis:** [Why this specific change might improve performance]

**Copy:**
```
[same subject line as A]

[email body]

[signature placeholder]
```

**Why this might win:**
- [Reason 1 with pattern/evidence]
- [Reason 2 with pattern/evidence]

---

### 🧪 Variant C (Test: [Different Copy Element])
**Word count:** [X words]
**What differs from A:** [Specific meaningful difference]
**Hypothesis:** [Why this specific change might improve performance]

**Copy:**
```
[same subject line as A]

[email body]

[signature placeholder]
```

**Why this might win:**
- [Reason 1 with pattern/evidence]
- [Reason 2 with pattern/evidence]

---

## Email 2 (2 Variants)

[Same structure as Email 1, but only A and B variants]

---

## Quality Checklist

✅ All emails ≤80 words (or ≤32 for one-liner)
✅ All sentences ≤30 words
✅ All variants use SAME subject line (per email)
✅ Variants test meaningful copy differences
✅ Touch/see/feel in Variant [X]
✅ CTAs sell promise land
✅ No anti-patterns used
✅ Grade 9 reading level
✅ No bullet points, em/en dashes, dollar signs
✅ Rooted in prospect context
✅ References ≥3 knowledge nodes
✅ [Format-specific checks passed]

---

## Proofreading Notes

[Any relevant notes from proofreading process]

---

## Variant Testing Strategy

**What we're learning:**
- Variant A vs B: [Specific hypothesis]
- Variant A vs C: [Specific hypothesis]
- Variant B vs C: [Specific hypothesis]

**Predicted winner:** [Agent's prediction with reasoning]

**If A wins:** [What that validates]
**If B wins:** [What that validates]
**If C wins:** [What that validates]

---

**USER: Review the above and either:**
1. Type "approve" to move to copy-drafts.md
2. Provide feedback for revisions
3. Request specific changes
```

**After writing to cc_canvas.md, tell user:**

```
✅ Campaign generated and presented in cc_canvas.md

Location: aa_canvas/cc_canvas.md

Please review and either:
1. Type "approve" to move to copy-drafts.md for client review
2. Provide feedback for revisions
3. Request specific changes
```

---

### Step 4.2: User Reviews in cc_canvas.md

**Wait for user response.**

**If user types "approve":** Proceed to Step 4.3

**If user provides feedback:** Return to Process 2 with feedback, regenerate, re-proofread, re-present in cc_canvas.md

**If user requests specific changes:** Apply changes, re-proofread, update cc_canvas.md

---

### Step 4.3: After User Approval → Move to copy-drafts.md

**Read campaign from cc_canvas.md**

**Append to:** `00_foundation/messaging/copy-drafts.md`

**Format:**

```markdown
---

## [Campaign Name]

**Created:** [Date]
**Approved by user:** [Date]
**Status:** Ready to show client
**Client:** XP Labs
**Format:** [Format type]

### Campaign Brief
- **ICP/Persona:** [[icp-segment]] + [[persona]]
- **Pain Point:** [[pain-point]]
- **Offer:** [Offer description]
- **Subject Line (All Variants):** [subject]
- **Knowledge Nodes:** [[node-1]], [[node-2]], [[node-3]]

### Email 1 - Variant A (Control)
**Subject:** [subject]
[copy body]

### Email 1 - Variant B (Test: [element])
**Subject:** [subject]
[copy body]

### Email 1 - Variant C (Test: [element])
**Subject:** [subject]
[copy body]

### Email 2 - Variant A
**Subject:** [subject]
[copy body]

### Email 2 - Variant B (Test: [element])
**Subject:** [subject]
[copy body]

---
```

**Confirm to user:**

```
✅ Campaign approved and added to copy-drafts.md

Location: 00_foundation/messaging/copy-drafts.md

Next steps:
1. Review campaign in copy-drafts.md
2. Show to client
3. If client requests changes, edit copy-drafts.md directly (or ask me to make changes)
4. When client approves, tell me:
   "[Campaign Name] in copy draft has been approved by client. Move it to week [N] [Month] [Year]"
```

---

### Step 4.3b: Learning Capture (Autonomous - After Approval)

**Purpose:** Compound intelligence by capturing anti-patterns, constraints, and successful patterns from campaign revisions.

**Agent checks:**

**Did this campaign require user revisions?**
- If NO revisions → Skip to Step 4.4 confirmation
- If YES revisions → Capture learnings below

**Learning capture process:**

1. **Identify anti-patterns (what went wrong):**
   - What did I generate that user corrected?
   - Why was it wrong? (client constraint, vague language, wrong offer type, etc.)
   - Is this a one-time mistake or systemic issue?

2. **Check if anti-pattern already exists:**
   - Search `knowledge_base/methodology/` for similar anti-pattern nodes
   - Search `.claude/skills/cold-email-domain-expert-knowledge-base/knowledge_base/methodology/` for system-wide patterns
   - If exists: Note to update with this example
   - If new: Create anti-pattern node

3. **Check if client constraint discovered:**
   - Did user reveal something client "won't do"? (e.g., no Looms, no webinars, etc.)
   - Does `knowledge_base/business/campaign-constraints-xp-labs.md` exist?
     - If YES: Update with new constraint
     - If NO: Note to create constraints node (use template)

4. **Check if successful pattern emerged:**
   - Did user suggest specific language that worked? (e.g., "if you're looking to sell")
   - Is this reusable for future campaigns?
   - Create email-pattern node if pattern is validated

**Agent creates list of learning tasks:**

```markdown
## Learning Capture: [Campaign Name]

**Revisions required:** [Yes/No]

**Anti-patterns identified:**
1. [Anti-pattern name] - [What was wrong] - [Action: Create/Update node]
2. [Anti-pattern name] - [What was wrong] - [Action: Create/Update node]

**Client constraints discovered:**
1. [Constraint] - [Action: Create/Update campaign-constraints.md]

**Successful patterns identified:**
1. [Pattern name] - [What worked] - [Action: Create email-pattern node]

**Knowledge nodes to create/update:**
- [ ] `anti-pattern-[name].md` in knowledge_base/methodology/
- [ ] `campaign-constraints-xp-labs.md` in knowledge_base/business/
- [ ] `email-pattern-[name].md` in knowledge_base/methodology/

**Immediate action:**
Would you like me to create these knowledge nodes now to capture these learnings, or skip for now?
(Type "create nodes" or "skip")
```

**If user types "create nodes":**
- Agent creates the identified knowledge nodes using appropriate templates
- Links nodes to this campaign as source
- Updates related nodes as needed

**If user types "skip":**
- Agent logs the learning capture summary to a temp file for later processing
- Continues to Step 4.4 confirmation

---

### Step 4.4: Move to Launched Campaigns (Triggered by User)

**User will say:** `"[Campaign Name] in copy draft has been approved by client. Move it to week [N] [Month] [Year]"`

**Agent actions:**

1. **Read campaign from copy-drafts.md**
2. **Construct path:**
   ```
   00_foundation/messaging/launched campaigns/[year]/[month]/week_[N]/launched_campaigns_week_[N]_[month_lower]_[year].md
   ```
3. **Check if folder exists** - create if needed
4. **Check if weekly file exists:**
   - If exists: Append campaign to file
   - If doesn't exist: Create from template, add campaign
5. **Remove campaign from copy-drafts.md**
6. **Confirm to user:**

```
✅ Campaign moved to launched campaigns

From: 00_foundation/messaging/copy-drafts.md
To: 00_foundation/messaging/launched campaigns/[year]/[month]/week_[N]/

Campaign removed from copy-drafts.md.

You can now track performance and run /cold-email-review when week ends.
```

---

## Error Handling

### Idea Queue Empty or Doesn't Exist
```
⚠️ Idea queue not found or empty for XP Labs

Options:
1. Provide idea directly (describe ICP, pain point, offer, angle)
2. Reference a specific campaign to iterate

Which would you prefer?
```

### Invalid Format Selection
```
❌ Invalid format selection: [input]

Valid formats:
1. Front-end offer
2. Poke the bear
3. One-liner

Please type 1, 2, or 3
```

### Proofreading Fails Multiple Times
```
⚠️ Campaign failed proofreading [N] times.

Recent issues:
- [Issue 1]
- [Issue 2]

Would you like me to:
1. Continue trying to fix automatically
2. Present current version (with warnings) for you to review
3. Start over with different approach

Type 1, 2, or 3
```

---

## Quality Standards Summary

**All campaigns must meet:**
- ✅ Copywriting Standards (xp-labs-copywriting-standards.md)
- ✅ Format-specific structure (from format skill)
- ✅ Knowledge-driven (≥3 XP Labs KB nodes referenced)
- ✅ Variant testing is meaningful (not trivial changes)
- ✅ Offer viability validated (cold-appropriate)
- ✅ Prospect language standards (CRITICAL):
  - No internal ICP labels in copy
  - Pain points explicit and concrete (not abstract)
  - Competitor mentions vague/softened (not specific names)
  - Promises/deliverables concrete (not "what's possible")
  - Industry jargon simplified or avoided
- ✅ Email structure standards (CRITICAL):
  - Natural conversational flow (not choppy bullet-point sentences)
  - NO meta-commentary about following up (just follow up)
  - NO soft openings ever (get into the email immediately)
- ✅ All checks pass before presenting to user

**Non-compliance = regenerate until compliant**

---

## Related Resources

- **Copywriting Standards:** `.claude/skills/cold-email-domain-expert-knowledge-base/knowledge_base/copywriting/xp-labs-copywriting-standards.md`
- **Format Skills:** `.claude/skills/email-format-writers/`
- **Domain KB (Copywriting):** `.claude/skills/cold-email-domain-expert-knowledge-base/knowledge_base/copywriting/`
- **Domain KB (Campaign Strategy):** `.claude/skills/cold-email-domain-expert-knowledge-base/knowledge_base/campaign-strategy/`
- **Cold Email Review Command:** `.claude/commands/cold-email-review.md`

---

**Last Updated:** 2026-01-20
