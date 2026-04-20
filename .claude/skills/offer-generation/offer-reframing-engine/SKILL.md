# Offer Reframing Engine

**Purpose:** Transform base offers into multiple compelling angles by reframing them for different contexts, situations, and emotional triggers in the prospect's work life.

---

## What This Skill Does

This skill implements **Framework 1: Contextual Offer Reframing**.

**Core concept:** The same base offer can be positioned differently depending on the prospect's current context, job-to-be-done, and emotional state. By identifying different situations where the offer applies, we create multiple campaign angles from a single core offering.

---

## The Reframing Process

### Step 1: Understand the Base Offer

**What you receive:**
- Base offer description (e.g., "Capital lending for founders", "FB ads management", "Sales enablement software")
- Full service/product details
- Core value proposition

**What to extract:**
- What problem does this fundamentally solve?
- What outcome does it deliver?
- What's the core mechanism/approach?

**Example:**
```
Base Offer: "Capital lending for founders"
Core problem solved: Need for cash/funding
Core outcome: Access to capital without equity dilution
Core mechanism: Non-dilutive debt financing
```

---

### Step 2: Identify Prospect Contexts & Jobs-to-be-Done

**What you receive:**
- Pain point nodes (specific problems prospects face)
- Persona nodes (roles, responsibilities, motivations, fears)
- ICP nodes (company characteristics, situations they're in)

**What to identify:**
Different **contexts** or **situations** in their work where they need this solution:

**Context types:**
1. **Survival/Crisis contexts** → Urgent, high-stakes situations
2. **Growth/Opportunity contexts** → Ambitious, forward-looking situations
3. **Efficiency/Optimization contexts** → Operational improvement situations
4. **Strategic/Positioning contexts** → Competitive advantage situations
5. **Career/Personal contexts** → Individual success/safety situations

**Jobs-to-be-done in each context:**
- What are they trying to accomplish?
- What would success look like?
- What are they afraid of?
- What would make them a hero?

**Example:**
```
Base Offer: "Capital lending for founders"

Context 1: Survival/Crisis
- Situation: Running out of runway, payroll in 60 days
- Job-to-be-done: Survive, avoid layoffs, don't lose team
- Fear: Having to shut down, letting team down
- Success: Bridge to next milestone

Context 2: Growth/Opportunity
- Situation: Market opportunity appearing, competitors moving fast
- Job-to-be-done: Scale quickly, capture market share
- Fear: Missing opportunity, competitors winning
- Success: Dominate market before others catch up

Context 3: Strategic/Positioning
- Situation: Competitor available for acquisition
- Job-to-be-done: Consolidate market, strategic positioning
- Fear: Competitor getting acquired by someone else
- Success: Own competitor, control market
```

---

### Step 3: Reframe the Offer for Each Context

**For each context, create a reframed angle:**

**Components of a reframe:**
1. **Situation description** → Paint the specific scenario
2. **Reframed offer name** → Position the same offer differently
3. **Value proposition** → What outcome they get in THIS context
4. **Emotional trigger** → What emotion does this tap into?
5. **Why it resonates** → Why this angle works for this context

**Example reframes:**

**Context 1: Survival/Crisis**
```
Situation: Founder running out of runway, payroll in 60 days
Reframed offer: "Emergency capital to avoid layoffs"
Value prop: "Bridge funding to survive until next milestone"
Emotional trigger: Fear, urgency, preservation, loyalty to team
Why it resonates:
- Taps into fear of failure
- Appeals to founder's sense of responsibility to team
- Frames capital as rescue, not growth tool
- Urgent language matches urgent situation
```

**Context 2: Growth/Opportunity**
```
Situation: Market opportunity appearing, need to move fast
Reframed offer: "Growth capital to scale without waiting for profit"
Value prop: "Capture market share before competitors, scale now"
Emotional trigger: Ambition, FOMO, competitive advantage
Why it resonates:
- Taps into ambition and competitive drive
- Frames capital as opportunity enabler, not rescue
- Appeals to founder's vision and growth mindset
- Creates urgency through competition framing
```

**Context 3: Strategic/Positioning**
```
Situation: Competitor available for acquisition
Reframed offer: "Acquisition capital to consolidate market"
Value prop: "Own your competitor, control the market"
Emotional trigger: Strategic thinking, market dominance, vision
Why it resonates:
- Taps into strategic/visionary identity
- Frames capital as power move, not necessity
- Appeals to founder's long-term thinking
- Creates urgency through scarcity (someone else might buy)
```

---

### Step 4: Map Reframes to Specific Personas

**Different personas respond to different contexts:**

**Founder persona:**
- Responds to: Growth, opportunity, vision, strategic contexts
- Motivated by: Building something big, competitive advantage
- Fears: Missing opportunities, getting outmaneuvered
- Reframes work: Growth capital, acquisition capital, competitive advantage

**CFO persona:**
- Responds to: Efficiency, optimization, risk mitigation contexts
- Motivated by: Financial prudence, cash flow management
- Fears: Running out of cash, making bad bets
- Reframes work: Bridge funding, cash flow management, risk mitigation

**CMO persona:**
- Responds to: Career safety, proving ROI, efficiency contexts
- Motivated by: Proving marketing works, career advancement
- Fears: Getting blamed, budget cuts, looking bad
- Reframes work: Prove ROI, career safety, board presentation ammo

**Implementation:**
For each reframe, note which persona(s) it's most relevant for based on their motivations, fears, and jobs-to-be-done.

---

## Input Specification

**What this skill receives:**

1. **Base offer(s):**
   - From `00_foundation/messaging/front-end-offers.md`
   - Or extracted from service/product nodes
   - Core value propositions

2. **Pain point nodes:**
   - From `knowledge_base/business/pain-point-*.md`
   - Specific problems prospects face
   - Context about when/why they experience pain

3. **Persona nodes:**
   - From `knowledge_base/business/persona-*.md`
   - Roles, responsibilities, motivations, fears
   - Decision-making authority and priorities

4. **ICP nodes:**
   - From `knowledge_base/business/icp-*.md`
   - Company situations and characteristics
   - Behavioral signals and qualification criteria

5. **Domain expertise:**
   - Cold email best practices
   - Proven reframing patterns
   - Psychological triggers that work

---

## Output Specification

**What this skill returns:**

Array of reframed offer objects, each containing:

```javascript
{
  base_offer: "Original offer name",
  reframed_offer: "Contextualized offer name",
  context_type: "Survival | Growth | Efficiency | Strategic | Career",
  situation: "Specific scenario description",
  value_proposition: "What they get in this context",
  emotional_trigger: "Fear | Ambition | FOMO | Safety | etc.",
  why_it_resonates: "Reasoning for why this works",
  best_for_personas: ["persona-slug-1", "persona-slug-2"],
  best_for_icps: ["icp-slug-1", "icp-slug-2"],
  angle: "Strategic narrative/hook for this reframe",
  knowledge_links: {
    pain_points: ["pain-point-slug"],
    personas: ["persona-slug"],
    icps: ["icp-slug"],
    value_props: ["value-prop-slug"]
  }
}
```

---

## Reframing Patterns & Examples

### Pattern 1: Crisis → Rescue Reframe

**When to use:** Pain point involves urgent problem, high stakes
**How it works:** Position offer as emergency solution, rescue operation

**Example:**
- Base: "FB ads management"
- Crisis context: "ROAS dropped 40% in last 30 days, CEO questioning budget"
- Reframe: "Emergency ROAS recovery audit"
- Trigger: Fear of budget cuts, career safety
- Persona: CMO under pressure

---

### Pattern 2: Opportunity → Enabler Reframe

**When to use:** ICP is in growth mode, market opportunity exists
**How it works:** Position offer as opportunity enabler, growth accelerator

**Example:**
- Base: "FB ads management"
- Growth context: "Launching 3 new products this quarter, need to scale fast"
- Reframe: "Rapid-launch creative supply for high-velocity brands"
- Trigger: Ambition, FOMO, competitive advantage
- Persona: Founder, Head of Growth

---

### Pattern 3: Problem → Prevention Reframe

**When to use:** Pain point is predictable, happens repeatedly
**How it works:** Position offer as preventing future pain, not just fixing current

**Example:**
- Base: "FB ads management"
- Prevention context: "Every product launch, creative fatigues in 2-3 weeks"
- Reframe: "Systematic creative testing to prevent fatigue"
- Trigger: Frustration with repeated pattern, desire for control
- Persona: Founder (hands-on), CMO

---

### Pattern 4: Generic → Specific Industry Reframe

**When to use:** ICP is industry-specific with unique pain points
**How it works:** Take general offer, make industry-specific

**Example:**
- Base: "FB ads management"
- Industry: Supplement brands
- Reframe: "FDA-compliant creative testing for supplement brands"
- Trigger: Industry-specific fear (compliance), expertise signal
- Persona: Founder, CMO at supplement brands

---

### Pattern 5: Full Service → Diagnostic Reframe

**When to use:** Cold outreach, need low-commitment entry
**How it works:** Position offer as audit/diagnosis before full service

**Example:**
- Base: "Full-service FB ads management"
- Diagnostic context: "Not sure what's broken, just know ROAS is declining"
- Reframe: "Free creative fatigue audit (we'll show you what's dying)"
- Trigger: Curiosity, low-commitment, proof before pitch
- Persona: Founder, CMO (cautious)

---

### Pattern 6: Competitor → Differentiation Reframe

**When to use:** Competitor nodes show how others fail at this
**How it works:** Position offer as solving what competitors miss

**Example:**
- Base: "FB ads management"
- Competitor gap: "Other agencies just run ads, no creative strategy"
- Reframe: "Creative-first FB ads (60% of results come from creative, not buying)"
- Trigger: Frustration with current vendors, desire for better
- Persona: Brands who churned from other agencies

---

## Quality Standards for Reframes

**Good reframe has:**
- ✅ Specific situation/context (not vague)
- ✅ Clear emotional trigger (fear, ambition, FOMO, etc.)
- ✅ Mapped to specific persona(s)
- ✅ Connected to actual pain point from knowledge base
- ✅ Distinct from other reframes (not just word swapping)
- ✅ Believable and authentic (not overhyped)

**Bad reframe has:**
- ❌ Generic context ("businesses that need help")
- ❌ No emotional layer (just feature description)
- ❌ Not specific to any persona
- ❌ Made-up pain point (not in knowledge base)
- ❌ Too similar to another reframe
- ❌ Overpromising or unbelievable

---

## How Many Reframes to Generate?

**Guidelines:**
- **Minimum:** 3 reframes per base offer (different contexts)
- **Optimal:** 5-7 reframes per base offer (diverse contexts)
- **Maximum:** Don't exceed 10 reframes (diminishing returns)

**Prioritize:**
- Reframes that map to primary personas
- Reframes that address documented pain points
- Reframes that differentiate from competitors
- Reframes that span different emotional triggers

---

## Usage in Campaign Idea Generation

**This skill is called by `/generate-campaign-ideas` command:**

1. Command reads client knowledge base
2. Command identifies base offers
3. Command calls this skill: "Reframe these offers given this context"
4. This skill returns array of reframed offers
5. Command combines reframes with ICP/persona mapping
6. Command formats as complete campaign ideas

**This skill focuses on:** Strategic offer positioning
**Command handles:** Full idea formatting, presentation, queue management

---

## Examples: Full Reframing Process

### Example 1: FB Ads Agency (ScaleWorks Media)

**Base Offer:** "Full-service Meta ads management"

**Input Context:**
- ICP: Supplement brands ($2M-$15M, $30K+ ad spend)
- Persona: Founder (hands-on with marketing)
- Pain point: Creative fatigue (ads die after 2-3 weeks)
- Pain point: Attribution broken post-iOS 14
- Pain point: Stuck at $50K/month spend ceiling

**Generated Reframes:**

**Reframe 1:**
```
Reframed Offer: "Creative Fatigue Audit for Supplement Brands"
Context: Diagnostic/Prevention
Situation: Launching 2+ supplements/year, creative dies in 3 weeks
Value Prop: Free audit showing which creatives are fatigued + when
Emotional Trigger: Fear of wasted spend + Curiosity (proof before pitch)
Best For: Founder persona at supplement brands
Angle: "Your [product] launch creative died 2 weeks ago. Want to see the data?"
```

**Reframe 2:**
```
Reframed Offer: "Attribution Fix for Scaling DTC Brands"
Context: Efficiency/Optimization
Situation: Don't trust Meta's ROAS numbers, can't scale confidently
Value Prop: Incrementality testing setup to know true ROAS
Emotional Trigger: Frustration with broken attribution + Desire for control
Best For: Founder persona at supplement/skincare brands
Angle: "Your 2.5 ROAS might actually be 4.2. Or 1.8. Want to know for sure?"
```

**Reframe 3:**
```
Reframed Offer: "Rapid-Launch Creative Supply"
Context: Growth/Opportunity
Situation: Launching products quickly, need fresh creatives constantly
Value Prop: 4 new creative concepts tested every week
Emotional Trigger: Ambition (scale fast) + FOMO (competitors moving)
Best For: Founder persona at high-velocity brands
Angle: "Launching 2+ products a month? Your creative can't keep up. We can."
```

---

### Example 2: Capital Lending for Founders

**Base Offer:** "Non-dilutive capital for founders"

**Input Context:**
- ICP: B2B SaaS founders (Series A-B, $2M-$10M revenue)
- Persona: Founder/CEO
- Pain point: Running out of runway before profitability
- Pain point: Don't want to dilute equity with another round
- Pain point: Missing growth opportunities due to cash constraints

**Generated Reframes:**

**Reframe 1:**
```
Reframed Offer: "Bridge Capital to Avoid Down Round"
Context: Crisis/Rescue
Situation: 4 months of runway left, not ready for Series B, options are layoffs or down round
Value Prop: Bridge to profitability without dilution or layoffs
Emotional Trigger: Fear of failure + Responsibility to team + Ego (avoid down round)
Best For: Founder/CEO at Series A companies
Angle: "You're 6 months from profitable. Don't fire your team or take a down round. Bridge it."
```

**Reframe 2:**
```
Reframed Offer: "Growth Capital Without Board Drama"
Context: Growth/Opportunity
Situation: See market opportunity, want to scale fast, don't want new investors/board seats
Value Prop: Capital to scale without adding board members or diluting control
Emotional Trigger: Ambition + Control/autonomy + Competitive advantage
Best For: Founder/CEO who values control
Angle: "Scale to $20M ARR without adding another board member. Keep control."
```

**Reframe 3:**
```
Reframed Offer: "Acquisition Capital to Consolidate Market"
Context: Strategic/Positioning
Situation: Competitor is struggling, available for acquisition, would give market dominance
Value Prop: Capital to acquire competitor, consolidate market share
Emotional Trigger: Strategic vision + Market dominance + Urgency (before someone else buys)
Best For: Founder/CEO with strategic mindset
Angle: "That competitor you're worried about? You could own them in 90 days."
```

---

## Anti-Patterns to Avoid

**❌ Don't just swap words:**
Bad: "FB ads management" → "FB ads services" → "FB ads solutions"
These aren't reframes, just synonyms. No new context, no new emotional angle.

**❌ Don't make up pain points:**
Bad: Creating reframe for "Founders struggling with employee retention via ads"
If this pain point doesn't exist in knowledge base, don't invent it.

**❌ Don't create generic reframes:**
Bad: "For businesses that want better results"
Good: "For supplement brands launching 2+ products/quarter who need systematic creative supply"

**❌ Don't ignore persona differences:**
Bad: Using same reframe for Founder and CFO
Founders and CFOs have different motivations, fears, language - tailor accordingly.

**❌ Don't over-promise:**
Bad: "We'll 10X your ROAS in 30 days guaranteed"
Stay believable, authentic, grounded in what client actually delivers.

---

## Success Criteria

**A successful reframe:**
1. Creates a distinct angle from same base offer
2. Maps to specific context/situation from knowledge base
3. Triggers clear emotion (fear, ambition, FOMO, etc.)
4. Resonates with specific persona(s)
5. Solves actual pain point documented in knowledge base
6. Feels authentic and believable
7. Different enough from other reframes to be worth testing

---

**This skill is one component of the campaign idea generation system. It provides the strategic reframing layer. The main command orchestrates the full process.**
