# Minimum Viable Offer (MVO) Slicer

**Purpose:** Break down full services or products into atomic, standalone value propositions that each solve ONE specific problem and can be offered independently in cold email campaigns.

---

## What This Skill Does

This skill implements **Framework 2: Minimum Viable Offer (MVO) Slicing**.

**Core concept:** Most clients sell a "full service" or complete product with multiple components. But in cold email, offering everything at once is overwhelming and vague. By slicing the full offering into minimum viable offers, we create specific, concrete, easy-to-understand hooks that are less intimidating and more actionable.

---

## The MVO Slicing Process

### Step 1: Understand the Full Offering

**What you receive:**
- Full service/product description
- All components that make up the complete offering
- Technical capabilities and features
- Value propositions for the full package

**What to extract:**
- What are ALL the things this service/product does?
- What are the distinct components or modules?
- What problems does each component solve?
- Which components could stand alone as valuable?

**Example:**
```
Full Service: "Full-service Facebook ads management"

Components:
- Strategy & planning
- Creative strategy and art direction
- Creative testing (4+ concepts per week)
- Media buying and optimization
- Attribution tracking and setup
- Incrementality testing
- Weekly reporting and analysis
- Monthly strategy calls
- Competitor creative analysis
```

---

### Step 2: Identify Atomic Value Units

**For each component, ask:**
1. Does this solve a SPECIFIC problem?
2. Could this be valuable even if they don't buy the full service?
3. Is this concrete and easy to understand?
4. Does this address a pain point in the knowledge base?

**Atomic value unit criteria:**
- ✅ Solves ONE specific problem
- ✅ Stands alone as valuable
- ✅ Easy to explain in 1-2 sentences
- ✅ Has clear deliverable/outcome
- ✅ Not dependent on other components
- ✅ Addresses documented pain point

**Example extraction:**
```
Component: "Creative testing (4+ concepts per week)"

Is this atomic? YES
- Solves ONE problem: Need for fresh creative supply
- Stands alone: Can test creatives without full account management
- Easy to explain: "We'll test 4 new creative concepts every week"
- Clear deliverable: 4 tested concepts per week
- Independent: Don't need full service to do this
- Addresses pain: Creative fatigue (documented in knowledge base)

MVO: "Rapid Creative Testing Supply"
```

---

### Step 3: Define Each MVO

**For each atomic value unit, create an MVO with:**

1. **MVO Name** → Specific, concrete name
2. **Problem it solves** → ONE specific problem
3. **What you get** → Clear deliverable
4. **Who it's for** → Specific ICP/persona
5. **Why standalone** → Why valuable without full service
6. **Pain point link** → Which pain point from KB this addresses

**MVO Template:**
```
MVO: [Name]
Solves: [Specific problem in one sentence]
Deliverable: [What they actually get]
Best for: [Specific ICP/persona characteristics]
Why standalone: [Why valuable even without full service]
Links to: [[pain-point-node]]
```

**Example:**
```
MVO: Rapid Creative Testing Supply
Solves: DTC brands launching products frequently need constant fresh creatives to avoid fatigue
Deliverable: 4 new creative concepts tested every week with performance data
Best for: Supplement/skincare brands launching 2+ products per quarter
Why standalone: Even if they manage their own ads, they need creative supply
Links to: [[pain-point-creative-fatigue]]
```

---

### Step 4: Map MVOs to Pain Points & ICPs

**Each MVO should map to:**
- Specific pain point from knowledge base
- Specific ICP characteristics
- Specific use case or scenario

**Mapping logic:**

**Pain point → MVO connection:**
```
Pain Point: "Attribution is broken post-iOS 14, don't trust Meta's numbers"
↓
Component: "Attribution tracking and incrementality testing"
↓
MVO: "iOS Attribution Fix"
Solves: Brands spending $50K+ don't know their true ROAS
Deliverable: Incrementality testing setup + true ROAS dashboard
Best for: Brands spending $50K+ monthly who need accurate metrics
```

**ICP characteristics → MVO connection:**
```
ICP: Supplement brands launching 2+ products/quarter
↓
Pain: Need constant fresh creatives for each launch
↓
Component: Creative testing
↓
MVO: "High-Velocity Launch Creative Supply"
Solves: Brands shipping products quickly can't keep up with creative demand
Deliverable: 4 weekly concepts + launch playbook
Best for: Brands launching 2+ products per quarter
```

---

## Input Specification

**What this skill receives:**

1. **Service/product descriptions:**
   - From `knowledge_base/technical/service-*.md`
   - Full offering descriptions
   - Component breakdowns

2. **Pain point nodes:**
   - From `knowledge_base/business/pain-point-*.md`
   - Specific problems MVOs can solve
   - Context about when pain occurs

3. **ICP nodes:**
   - From `knowledge_base/business/icp-*.md`
   - Characteristics that make certain MVOs relevant
   - Behavioral signals and use cases

4. **Value proposition nodes:**
   - From `knowledge_base/business/value-prop-*.md`
   - How client solves problems
   - Differentiators

---

## Output Specification

**What this skill returns:**

Array of MVO objects, each containing:

```javascript
{
  mvo_name: "Specific MVO name",
  base_component: "Which component of full service this comes from",
  problem_solved: "ONE specific problem this solves",
  deliverable: "What they actually get",
  best_for_icps: ["icp-slug-1", "icp-slug-2"],
  best_for_personas: ["persona-slug-1"],
  why_standalone: "Why valuable without full service",
  pain_point_links: ["pain-point-slug-1"],
  value_prop_links: ["value-prop-slug-1"],
  offer_type: "Diagnostic | Implementation | Ongoing | Tool/Resource",
  entry_point: "What makes this low-commitment for cold outreach"
}
```

---

## MVO Patterns & Examples

### Pattern 1: Diagnostic MVO

**When to use:** Prospect doesn't know what's wrong, needs assessment
**Structure:** Audit, analysis, assessment, diagnosis
**Entry point:** Free or low-cost, low-commitment

**Examples:**

```
MVO: "Creative Fatigue Audit"
From: Creative testing component
Solves: Don't know which creatives are fatigued or when
Deliverable: Analysis showing which ads are dying + when they hit fatigue
Best for: Brands spending $30K+ monthly on Meta
Offer type: Diagnostic
Entry point: Free using public ad data
```

```
MVO: "Attribution Health Check"
From: Attribution setup component
Solves: Don't know if attribution tracking is set up correctly
Deliverable: Report showing what's tracked vs what's missing
Best for: Brands spending $50K+ who don't trust their numbers
Offer type: Diagnostic
Entry point: Free 30-minute assessment
```

---

### Pattern 2: Implementation MVO

**When to use:** Prospect knows problem, needs specific fix
**Structure:** Setup, implementation, fix, installation
**Entry point:** Fixed-price project, not ongoing retainer

**Examples:**

```
MVO: "iOS Attribution Setup"
From: Attribution tracking component
Solves: Post-iOS 14, server-side tracking isn't set up
Deliverable: Server-side tracking implemented + incrementality framework
Best for: Brands spending $50K+ who need accurate ROAS
Offer type: Implementation (one-time)
Entry point: Fixed project vs ongoing retainer
```

```
MVO: "Systematic Creative Testing Framework"
From: Creative strategy component
Solves: No process for testing creatives, just throwing stuff at wall
Deliverable: Creative testing framework + first 4 concepts tested
Best for: Brands ready to scale but need systematic approach
Offer type: Implementation
Entry point: One-month pilot
```

---

### Pattern 3: Ongoing Service MVO

**When to use:** Prospect needs specific ongoing support, not full service
**Structure:** Subscription, retainer, ongoing delivery
**Entry point:** Smaller scope than full service

**Examples:**

```
MVO: "Weekly Creative Supply"
From: Creative testing component
Solves: Need constant fresh creatives but don't want full account management
Deliverable: 4 new concepts tested every week
Best for: Brands who manage their own ads but need creative help
Offer type: Ongoing (monthly subscription)
Entry point: Half the cost of full service, focused scope
```

```
MVO: "Monthly Competitor Creative Analysis"
From: Competitor analysis component
Solves: Don't know what competitors are doing with their ads
Deliverable: Monthly report of competitor creative strategies + what's working
Best for: Brands who want competitive intel without full service
Offer type: Ongoing (monthly)
Entry point: Standalone service, lower commitment
```

---

### Pattern 4: Tool/Resource MVO

**When to use:** Prospect needs self-service solution, not done-for-you
**Structure:** Calculator, template, tool, framework, resource
**Entry point:** Lead magnet, low/no cost

**Examples:**

```
MVO: "Creative Fatigue Calculator"
From: Creative testing component
Solves: Don't know if they have creative supply problem
Deliverable: Spreadsheet tool to calculate if creative is fatiguing
Best for: Any DTC brand running Meta ads
Offer type: Tool/resource
Entry point: Free download in exchange for meeting
```

```
MVO: "Ad Spend Payback Period Calculator"
From: Attribution and scaling component
Solves: Don't know how much they can scale without burning cash
Deliverable: Calculator showing exact payback period for their metrics
Best for: Brands ready to scale but worried about cash flow
Offer type: Tool/resource
Entry point: Free tool that demonstrates expertise
```

---

## Slicing Strategies by Service Type

### For Agency Services (e.g., FB Ads, SEO, Content)

**Full service typically includes:**
- Strategy & planning
- Execution & delivery
- Optimization & testing
- Reporting & analysis

**MVO slicing approach:**
1. **Diagnostic MVOs:** Audits, assessments, health checks
2. **Implementation MVOs:** Setup, framework installation, process design
3. **Ongoing MVOs:** Specific ongoing deliverable (creative supply, reporting, etc.)
4. **Tool MVOs:** Calculators, frameworks, templates

**Example - FB Ads Agency:**
```
Full Service: "Full FB ads management"

MVOs:
1. Creative Fatigue Audit (diagnostic)
2. iOS Attribution Setup (implementation)
3. Weekly Creative Supply (ongoing)
4. Competitor Creative Report (ongoing)
5. Creative Testing Framework (implementation)
6. Scaling Calculator (tool)
```

---

### For SaaS Products

**Full product typically includes:**
- Core features (multiple)
- Integrations
- Support & training
- Analytics & reporting

**MVO slicing approach:**
1. **Feature-specific MVOs:** Each major feature as standalone value
2. **Use-case MVOs:** Specific workflow or job-to-be-done
3. **Integration MVOs:** Integration with specific tool
4. **Vertical MVOs:** Product positioned for specific industry

**Example - Sales Enablement SaaS:**
```
Full Product: "Sales enablement platform"

MVOs:
1. CRM Data Unification (feature-specific)
2. Automated Email Sequences (feature-specific)
3. Sales Call Intelligence (feature-specific)
4. Salesforce Integration (integration)
5. Outbound Sales Workflow (use-case)
6. Sales Enablement for SaaS Companies (vertical)
```

---

### For Consulting/Service Businesses

**Full service typically includes:**
- Discovery/assessment phase
- Strategy development
- Implementation support
- Ongoing advisory

**MVO slicing approach:**
1. **Assessment MVOs:** Discovery, audit, diagnostic
2. **Strategy MVOs:** Strategic plan, roadmap, framework
3. **Implementation MVOs:** Specific deliverable or project
4. **Advisory MVOs:** Ongoing advisory on specific topic

**Example - GTM Consulting:**
```
Full Service: "Complete GTM strategy and execution"

MVOs:
1. GTM Readiness Audit (assessment)
2. ICP & Positioning Workshop (strategy)
3. Messaging Framework (strategy)
4. Sales Playbook (implementation)
5. Ongoing GTM Advisory (advisory)
```

---

## Quality Standards for MVOs

**Good MVO has:**
- ✅ Solves ONE specific problem (not multiple)
- ✅ Has clear, concrete deliverable (not vague)
- ✅ Easy to explain in 1-2 sentences
- ✅ Valuable even without full service
- ✅ Maps to documented pain point
- ✅ Appropriate for specific ICP/persona
- ✅ Has clear entry point for cold outreach

**Bad MVO has:**
- ❌ Tries to solve multiple problems at once
- ❌ Vague deliverable ("help you improve")
- ❌ Requires long explanation
- ❌ Only makes sense with full service
- ❌ Solves made-up problem (not in knowledge base)
- ❌ Generic ("for all businesses")
- ❌ No clear offer (just description of service)

---

## How Many MVOs to Generate?

**Guidelines:**
- **Minimum:** 3 MVOs per full service/product
- **Optimal:** 5-8 MVOs per full service/product
- **Maximum:** Don't exceed 12 MVOs (too fragmented)

**Prioritize:**
- MVOs that map to primary pain points
- MVOs that are easy to deliver standalone
- MVOs with low-commitment entry points
- MVOs that differentiate from competitors

---

## MVOs vs Full Service: When to Use Each

**Use MVOs for cold email when:**
- ✅ Prospect doesn't know you yet (low commitment needed)
- ✅ Full service is expensive/intimidating (MVO lowers barrier)
- ✅ Prospect has specific pain point (MVO addresses it precisely)
- ✅ Want to demonstrate expertise (MVO shows you understand their problem)
- ✅ Prospect might not need full service (MVO is right-sized)

**Use full service positioning when:**
- ❌ Warm lead (referral, inbound)
- ❌ Prospect already knows they need comprehensive solution
- ❌ MVO would underposition the value
- ❌ Relationship-based sale (not cold outreach)

**For cold email campaigns:** MVOs almost always perform better than full service offers.

---

## Examples: Full Slicing Process

### Example 1: ScaleWorks Media (FB Ads Agency)

**Full Service:** "Full-service Meta ads management - strategy, creative, buying, attribution, reporting"

**Components identified:**
1. Strategy & account structure
2. Creative strategy and art direction
3. Systematic creative testing (4+ per week)
4. Media buying and optimization
5. Attribution tracking & incrementality testing
6. Weekly reporting & analysis
7. Monthly strategy calls
8. Competitor creative analysis

**MVOs Generated:**

```
MVO 1: "Creative Fatigue Audit for Supplement Brands"
From: Creative testing component
Solves: Don't know which creatives are fatiguing or when they hit decay
Deliverable: Analysis of their account showing fatigued creatives + timeline
Best for: Supplement brands launching 2+ products/quarter
Why standalone: Valuable diagnosis even if they don't hire for full service
Pain point: [[pain-point-creative-fatigue]]
Offer type: Diagnostic
Entry point: Free using public ad data
```

```
MVO 2: "iOS Attribution Setup & Incrementality Testing"
From: Attribution component
Solves: Post-iOS 14, don't trust Meta's ROAS numbers, can't scale confidently
Deliverable: Server-side tracking setup + incrementality test framework + true ROAS dashboard
Best for: Brands spending $50K+ monthly who need accurate attribution
Why standalone: One-time setup project, don't need ongoing management
Pain point: [[pain-point-attribution-mess]]
Offer type: Implementation
Entry point: Fixed-price project vs ongoing retainer
```

```
MVO 3: "High-Velocity Creative Supply"
From: Creative testing component
Solves: Launching products constantly, creative team can't keep up
Deliverable: 4 new creative concepts tested every week
Best for: Brands launching 2+ products per quarter (high SKU velocity)
Why standalone: Can manage own ads, just need creative supply
Pain point: [[pain-point-creative-fatigue]]
Offer type: Ongoing
Entry point: Lower cost than full service, focused scope
```

```
MVO 4: "Ad Spend Scaling Calculator"
From: Attribution & scaling component
Solves: Don't know how much they can scale without burning cash
Deliverable: Calculator showing exact payback period based on their metrics
Best for: Brands at $30K-$50K monthly spend ready to scale
Why standalone: Self-service tool that demonstrates expertise
Pain point: [[pain-point-stuck-at-spend-level]]
Offer type: Tool/resource
Entry point: Free tool in exchange for meeting
```

```
MVO 5: "Competitor Creative Intelligence Report"
From: Competitor analysis component
Solves: Don't know what competitors are doing with their Meta ads
Deliverable: Monthly report of competitor creatives + what's working in their vertical
Best for: Brands in competitive verticals (supplements, skincare)
Why standalone: Standalone intel service, valuable even without full account management
Pain point: [[pain-point-no-strategic-oversight]] (lack of market intelligence)
Offer type: Ongoing
Entry point: Lower commitment than full service
```

---

### Example 2: Sales Enablement SaaS

**Full Product:** "All-in-one sales enablement platform - CRM integration, email sequences, call intelligence, analytics"

**Components identified:**
1. CRM data unification
2. Automated email sequences
3. Sales call recording & intelligence
4. Pipeline analytics & forecasting
5. Content management
6. Salesforce integration

**MVOs Generated:**

```
MVO 1: "CRM Data Cleanup & Unification"
From: CRM integration component
Solves: Sales data is scattered across CRM, support tickets, product usage - reps waste 15 hrs/week reconciling
Deliverable: Unified sales dashboard with all data sources integrated
Best for: Sales teams with 10+ reps using 3+ data sources
Why standalone: Solves specific pain without needing full platform
Pain point: [[pain-point-data-silos]]
Offer type: Implementation
Entry point: Fixed project to prove value before full platform
```

```
MVO 2: "Sales Call Win/Loss Analysis"
From: Call intelligence component
Solves: Don't know why deals are won or lost, no systematic learning
Deliverable: AI analysis of sales calls showing patterns in wins vs losses
Best for: B2B sales teams with 5+ reps making 20+ calls/week
Why standalone: Specific insight that drives immediate improvement
Pain point: [[pain-point-inconsistent-sales-process]]
Offer type: Diagnostic
Entry point: Free analysis of 10 calls
```

```
MVO 3: "Salesforce → Full Context Integration"
From: Salesforce integration component
Solves: Reps only see CRM data in Salesforce, miss product usage & support context
Deliverable: Full prospect context visible in Salesforce
Best for: Sales teams already on Salesforce who need enriched data
Why standalone: Solves specific integration problem without platform migration
Pain point: [[pain-point-incomplete-context]]
Offer type: Implementation
Entry point: Salesforce users don't want to switch, this enhances existing tool
```

---

## Anti-Patterns to Avoid

**❌ Don't create "mini full service" MVOs:**
Bad: "Starter FB ads package - strategy, creative, buying, reporting"
This is just a smaller version of full service, not an MVO. Not atomic enough.

**❌ Don't make MVOs too narrow:**
Bad: "We'll analyze your top 3 ad creatives"
This is too small, not enough value. MVO should be substantial.

**❌ Don't create MVOs that require full service:**
Bad: "Ongoing optimization" (requires access to account, media buying, etc.)
MVO should stand alone, not depend on other services.

**❌ Don't make up problems MVOs solve:**
Bad: MVO for "Solving ad fraud on Meta" if this isn't in knowledge base
Only create MVOs for documented pain points.

**❌ Don't create overlapping MVOs:**
Bad: "Creative Testing" + "Creative Supply" + "Creative Strategy"
These are too similar. Each MVO should be distinct.

---

## Success Criteria

**A successful MVO:**
1. Solves ONE specific problem from knowledge base
2. Has clear, concrete deliverable
3. Stands alone as valuable (doesn't require full service)
4. Maps to specific ICP/persona
5. Has low-commitment entry point for cold outreach
6. Easy to explain in 1-2 sentences
7. Distinct from other MVOs (not overlapping)
8. Addresses real pain point (not made up)

---

**This skill is one component of the campaign idea generation system. It provides the MVO slicing layer. The main command orchestrates the full process.**
