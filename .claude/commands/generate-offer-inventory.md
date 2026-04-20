---
name: generate-offer-inventory
description: Generate 10 high-level offer value propositions for XP Labs using MVO Slicer and Offer Reframing Engine
model: inherit
---

# Generate Offer Inventory Command

You are an Offer Generation Specialist for XP Labs's B2B SaaS marketing system. Your job is to generate high-level value propositions (MVOs and reframes) that will be contextualized during campaign ideation.

---

## Purpose

This command creates the **offer inventory** - a master list of 10 high-level value propositions generated from XP Labs's services, value propositions, and pain points.

**Key principle:** Generate generic offers ONCE during onboarding, then contextualize them during campaign ideation. The system tracks which combinations (offer + packaging + ICP + persona) work over time.

**What this command produces:**
- 10 high-level value propositions (the WHAT)
- NO packaging specificity (audit, checklist, etc.)
- NO ICP/persona specificity
- Balanced coverage across ALL XP Labs services

**What /generate-campaign-ideas does:**
- Takes these generic offers
- Adds packaging (audit, checklist, tool, etc.)
- Adds ICP specificity
- Adds persona specificity
- Crafts angles and hooks

---

## When to Use This Command

**Run once during initial setup:**
- After knowledge base is populated with services, ICPs, personas, pain points
- When XP Labs is ready to start cold email campaigns

**Run again (refresh) when:**
- New services or capabilities added
- New pain points discovered that warrant new offer angles
- Major strategic pivot requires rethinking offers

**Do NOT run this command:**
- Before knowledge base is populated
- Every time you generate campaign ideas (that's `/generate-campaign-ideas`)

---

## Usage

```bash
/generate-offer-inventory
```

---

## Step 1: Validate Knowledge Base Sufficiency

### 1.1: Check for Required Knowledge Nodes

**Services/Technical capabilities** (required for MVO Slicer):
```
Glob: knowledge_base/technical/service-*.md
Glob: knowledge_base/technical/capability-*.md
```

**Minimum:** At least 1 service documented

**ICPs** (context for offer generation):
```
Glob: knowledge_base/business/icp-*.md
```

**Minimum:** At least 2 ICPs documented

**Personas** (context for offer generation):
```
Glob: knowledge_base/business/persona-*.md
```

**Minimum:** At least 1 persona documented

**Pain points** (required for Offer Reframing):
```
Glob: knowledge_base/business/pain-point-*.md
```

**Minimum:** At least 2 pain points documented

### 1.2: Validate Sufficiency

**If insufficient knowledge:**
```
⚠️  Insufficient knowledge base for XP Labs

Found:
- Services: [N] (need at least 1)
- ICPs: [N] (need at least 2)
- Personas: [N] (need at least 1)
- Pain points: [N] (need at least 2)

Cannot generate quality offers without this foundational knowledge.

Recommendation:
1. Complete onboarding first
2. Process onboarding materials into the knowledge base
3. Verify nodes exist in knowledge_base/
4. Then run this command again

Stop or proceed anyway? (Type 'proceed' to continue with limited data)
```

If user types 'proceed', continue with caveat. Otherwise, stop.

---

## Step 2: Read XP Labs Knowledge Base

### 2.1: Read ALL Services/Capabilities

**CRITICAL:** Read EVERY service node to ensure balanced coverage.

```
Glob: knowledge_base/technical/service-*.md
Glob: knowledge_base/technical/capability-*.md
Glob: knowledge_base/technical/framework-*.md
```

**Extract from each:**
- Service name
- What it delivers
- Components (if broken down)
- Core value proposition

**Build service inventory:**
```javascript
services = [
  {slug: "service-1", name: "Pinterest Management", components: [...]},
  {slug: "service-2", name: "Meta Ads Management", components: [...]},
  {slug: "service-3", name: "Creative Strategy", components: [...]}
]
```

### 2.2: Read All ICPs

```
Glob: knowledge_base/business/icp-*.md
```

**Extract from each:**
- ICP name and slug
- Characteristics
- Pain points they experience

### 2.3: Read All Personas

```
Glob: knowledge_base/business/persona-*.md
```

**Extract from each:**
- Persona title/role
- Motivations and fears

### 2.4: Read All Pain Points

```
Glob: knowledge_base/business/pain-point-*.md
```

**Extract from each:**
- Pain point description
- Who experiences it
- Severity and impact

### 2.5: Read All Value Props

```
Glob: knowledge_base/business/value-prop-*.md
```

**Extract from each:**
- How client solves problems
- Differentiators

### 2.6: Build Context Object

Synthesize all gathered information:

```javascript
ClientContext = {
  name: "XP Labs",
  slug: "xp-labs",

  services: [
    {slug: "service-1", name: "Service Name", components: [...], value: "..."}
  ],

  icps: [
    {slug: "icp-1", name: "ICP Name", pain_points: [...]}
  ],

  personas: [
    {slug: "persona-1", title: "Title"}
  ],

  pain_points: [
    {slug: "pain-1", problem: "Description", who: [...], severity: "..."}
  ],

  value_props: [
    {slug: "value-1", how_we_solve: "Description", differentiator: "..."}
  ]
}
```

---

## Step 3: Generate Offers Using MVO Slicer

### 3.1: Call MVO Slicer Skill

**Skill location:**
```
.claude/skills/offer-generation/mvo-slicer/SKILL.md
```

**CRITICAL INSTRUCTION TO SKILL:**
"Generate ~5 generic, high-level MVOs covering ALL services in the knowledge base. Do NOT add packaging (audit, checklist, etc.), do NOT specify ICPs, do NOT specify personas. Just produce the core value propositions - the WHAT, not the HOW or WHO."

**Inputs:**
- ALL services from knowledge base (ensure every service is represented)
- Components of each service
- Pain points (for context)

**Process:**
1. Take each service
2. Break into atomic components
3. Identify which components solve standalone problems
4. Create generic MVOs for each
5. Ensure balanced coverage across all services

**Expected output:** ~5 generic MVOs

**MVO format (simplified):**
```javascript
{
  mvo_name: "Attribution tracking optimization",
  base_service: "Ad management",
  value: "Improve tracking accuracy and ROAS measurement",
  why_standalone: "Can be implemented independently of full service"
}
```

**Key: No packaging, no ICP specificity, no persona specificity**

### 3.2: Validate Service Coverage

After MVO generation, check:
```
Services in knowledge base: [Service 1, Service 2, Service 3]
MVOs generated:
- [Service 1]: X MVOs
- [Service 2]: Y MVOs
- [Service 3]: Z MVOs
```

**If imbalanced** (e.g., Service 1 has 4 MVOs, Service 2 has 1 MVO):
- Regenerate with explicit instruction: "Generate more MVOs for [Service 2] to balance coverage"
- Target: Roughly equal distribution across all major services

---

## Step 4: Generate Offers Using Offer Reframing Engine

### 4.1: Call Offer Reframing Engine Skill

**Skill location:**
```
.claude/skills/offer-generation/offer-reframing-engine/SKILL.md
```

**CRITICAL INSTRUCTION TO SKILL:**
"Generate ~5 generic, high-level reframes covering ALL services. Do NOT add packaging (audit, checklist, etc.), do NOT specify ICPs, do NOT specify personas. Just produce the core value propositions reframed for different contexts (survival, growth, efficiency, strategic). Keep them generic."

**Inputs:**
- ALL services from knowledge base
- Pain points (for emotional reframing)
- Value props (for differentiation)

**Process:**
1. Take services
2. Identify different contexts (survival, growth, efficiency, strategic, career)
3. Reframe for each context
4. Keep generic (no packaging, no ICP/persona specificity)
5. Ensure balanced coverage across all services

**Expected output:** ~5 generic reframes

**Reframe format (simplified):**
```javascript
{
  base_service: "Social media management",
  reframed_value: "Creative performance optimization",
  context: "Efficiency (reduce waste)",
  generic_situation: "Creative fatigue causing declining ROAS"
}
```

**Key: No packaging, no ICP specificity, no persona specificity**

### 4.2: Validate Service Coverage

After reframe generation, check:
```
Services in knowledge base: [Service 1, Service 2, Service 3]
Reframes generated:
- [Service 1]: X reframes
- [Service 2]: Y reframes
- [Service 3]: Z reframes
```

**If imbalanced:**
- Regenerate with explicit instruction to balance coverage
- Target: Roughly equal distribution across all major services

---

## Step 5: Service Coverage Validation

### 5.1: Analyze Coverage Across Generated Offers

Combine MVOs + Reframes = ~10 offers

**Coverage analysis:**
```
Services in knowledge base: [N services]

Offer distribution:
- [Service 1]: X offers (X%)
- [Service 2]: Y offers (Y%)
- [Service 3]: Z offers (Z%)
- Cross-service: W offers (W%)
```

**Quality thresholds:**
- ✅ GOOD: Each major service has 2+ offers
- ⚠️  ACCEPTABLE: Each major service has 1+ offer
- ❌ BAD: Any major service has 0 offers

### 5.2: Rebalance If Needed

**If coverage is BAD:**
- Identify underrepresented service
- Regenerate 1-2 offers specifically for that service
- Replace weakest offers from overrepresented service

**Example:**
```
Before rebalance:
- Pinterest: 7 offers
- Meta Ads: 2 offers
- Creative Strategy: 1 offer

After rebalance:
- Pinterest: 4 offers
- Meta Ads: 3 offers
- Creative Strategy: 3 offers
```

---

## Step 6: Present Offers to User for Approval

### 6.1: Format Offers for Review

Present generated offers to user:

```
═══════════════════════════════════════════════════════════
OFFER INVENTORY - XP Labs
Generated: [YYYY-MM-DD]
═══════════════════════════════════════════════════════════

I've generated 10 high-level offers across your service portfolio.

These are generic value propositions (the WHAT) that will be
contextualized during campaign ideation with packaging, ICPs,
and personas.

📊 SERVICE COVERAGE:
───────────────────────────────────────────────────────────
[Service 1]: [N] offers ([X]%)
[Service 2]: [N] offers ([X]%)
[Service 3]: [N] offers ([X]%)
Cross-service: [N] offers ([X]%)
───────────────────────────────────────────────────────────

📋 GENERATED OFFERS:

[SERVICE 1] - [N] OFFERS:
───────────────────────────────────────────────────────────
1. [Offer Name]
   Value: [Core value proposition - keep generic, no packaging/ICP]
   Framework: [MVO Slicer | Offer Reframing Engine]

2. [Offer Name]
   Value: [Core value proposition]
   Framework: [MVO Slicer | Offer Reframing Engine]

[SERVICE 2] - [N] OFFERS:
───────────────────────────────────────────────────────────
3. [Offer Name]
   Value: [Core value proposition]
   Framework: [MVO Slicer | Offer Reframing Engine]

4. [Offer Name]
   Value: [Core value proposition]
   Framework: [MVO Slicer | Offer Reframing Engine]

[SERVICE 3] - [N] OFFERS:
───────────────────────────────────────────────────────────
5. [Offer Name]
   Value: [Core value proposition]
   Framework: [MVO Slicer | Offer Reframing Engine]

[Continue for all 10 offers...]

═══════════════════════════════════════════════════════════
REVIEW & APPROVAL
═══════════════════════════════════════════════════════════

Please review these offers and let me know:

OPTIONS:
1. Approve all offers
   → Type: 'all'

2. Approve specific offers by number
   → Type: '1,2,3,5,7,9' (comma-separated)

3. Edit an offer before approving
   → Type: 'edit [number]'
   → Example: 'edit 5'

4. Regenerate all offers
   → Type: 'regenerate'

What would you like to do?
```

Wait for user response.

---

## Step 7: Handle User Feedback

### 7.1: If User Types 'all'

Approve all 10 offers and proceed to Step 8 (Create Inventory Files).

### 7.2: If User Types Specific Numbers (e.g., '1,2,3,5,7')

Parse numbers:
```javascript
approved = [1, 2, 3, 5, 7]
declined = [4, 6, 8, 9, 10]
```

Show declined offers and ask:
```
You've approved [N] offers and declined [N] offers.

Declined offers:
- Offer #4: [Name]
- Offer #6: [Name]
- Offer #8: [Name]
- Offer #9: [Name]
- Offer #10: [Name]

Would you like to:
1. Proceed with [N] approved offers only
   → Type: 'proceed'

2. Generate [N] new offers to replace declined ones
   → Type: 'replace'

3. Go back and review again
   → Type: 'review'
```

**If 'proceed':** Use only approved offers, proceed to Step 8

**If 'replace':**
- Identify which services the declined offers covered
- Generate new offers for those services
- Present new offers for approval
- Repeat Step 6-7 until approved

**If 'review':** Return to Step 6.1

### 7.3: If User Types 'edit [number]'

Parse number (e.g., 'edit 5'):

```
You want to edit Offer #5:

Current:
Name: [Current name]
Value: [Current value proposition]
Framework: [Framework]

What would you like to change?

1. Edit the name
   → Type: 'name: [new name]'

2. Edit the value proposition
   → Type: 'value: [new value prop]'

3. Edit both
   → Type: 'name: [new name] | value: [new value prop]'

4. Cancel edit
   → Type: 'cancel'
```

Wait for user response.

**After edit:**
- Update the offer with new details
- Show updated offer list
- Return to Step 6.1 (re-present for approval)

**User can edit multiple offers:**
- After one edit completes, they can type 'edit [number]' again

### 7.4: If User Types 'regenerate'

```
Regenerating all 10 offers from scratch...

This will discard the current batch and start over.

Confirm regeneration? (Type 'yes' to confirm, 'no' to cancel)
```

**If 'yes':** Return to Step 3 (Generate Offers Using MVO Slicer)

**If 'no':** Return to Step 6.1 (re-present current offers)

---

## Step 8: Create Offer Inventory Files

### 8.1: Create Folder

Create directory:
```
00_foundation/messaging/offer-inventory/
```

### 8.2: Create offer-inventory.md

Read template:
```
templates/offer-inventory-template.md
```

Customize with:
- Client slug and name
- Generated date
- Total offers count (only approved offers)
- All approved offers (numbered sequentially)

### 8.3: Populate Each Offer Entry

For each approved offer, create entry:

```markdown
## Offer #[N]: [Descriptive Name]

**Value Proposition:** [High-level value - the WHAT, not the HOW]

**Framework:** [MVO Slicer | Offer Reframing Engine]

**Generated:** [YYYY-MM-DD]

**Description:**
[1-3 sentence description of the core value proposition. Keep it generic - no specific packaging, ICP, or persona mentioned.]

**Status:** Untested

**Test History:**
(None yet)

**Performance Summary:**
- Times tested: 0
- Success rate: N/A
- Avg reply rate: N/A
- Meetings booked: 0

**Learnings:**
(None yet - will be populated after campaigns test this offer with different packaging/ICP/persona combinations)
```

### 8.4: Update Summary Statistics

At bottom of offer-inventory.md:

```markdown
## Summary Statistics

**By Framework:**
- MVO Slicer offers: [N]
- Offer Reframing offers: [N]

**Service Coverage:**
- [Service 1]: [N] offers
- [Service 2]: [N] offers
- [Service 3]: [N] offers
- Cross-service: [N] offers

**Top Performers:**
(None yet - need test data)

**Bottom Performers:**
(None yet - need test data)

**Recommended Next Tests:**
(Will be populated after analyzing campaign patterns)
```

---

## Step 9: Create Offer Performance Log

### 9.1: Create offer-performance-log.md

Read template:
```
templates/offer-performance-log-template.md
```

Customize with:
- Client slug and name
- Created date
- Empty entries (will be populated after campaigns)

**This file starts empty** - entries added during `/cold-email-review`.

---

## Step 10: Present Summary to User

### 10.1: Show What Was Generated

```
✅ Offer Inventory Generated for XP Labs

═══════════════════════════════════════════════════════════
INVENTORY SUMMARY
═══════════════════════════════════════════════════════════

📊 Offers Created: [N]
- MVO Slicer offers: [N]
- Offer Reframing offers: [N]

📊 Service Coverage:
- [Service 1]: [N] offers ([X]%)
- [Service 2]: [N] offers ([X]%)
- [Service 3]: [N] offers ([X]%)

📁 Files Created:
1. 00_foundation/messaging/offer-inventory/offer-inventory.md
2. 00_foundation/messaging/offer-inventory/offer-performance-log.md

═══════════════════════════════════════════════════════════
SAMPLE OFFERS
═══════════════════════════════════════════════════════════

Offer #1: [Name]
Value: [Value proposition]

Offer #2: [Name]
Value: [Value proposition]

Offer #3: [Name]
Value: [Value proposition]

[Show all offers...]

═══════════════════════════════════════════════════════════
NEXT STEPS
═══════════════════════════════════════════════════════════

1. Review your offer inventory:
   00_foundation/messaging/offer-inventory/offer-inventory.md

2. Generate campaign ideas:
   /generate-campaign-ideas

   This will:
   - Analyze your offer inventory
   - Take these generic offers and contextualize them
   - Add packaging (audit, checklist, tool, etc.)
   - Add ICP specificity
   - Add persona specificity
   - Craft campaign angles

3. After campaigns complete:
   /cold-email-review

   This will update offer performance tracking with the specific
   combination tested (offer + packaging + ICP + persona).

═══════════════════════════════════════════════════════════

📈 The system will now track which COMBINATIONS work:
   - Which offers work universally
   - Which packaging formats resonate with which ICPs
   - Which persona combinations respond better
   - Multi-dimensional pattern recognition

Your institutional knowledge will compound over time.
```

---

## Error Handling

### If knowledge base is empty:
```
❌ No knowledge base found for XP Labs

No knowledge nodes found:
- 0 services found
- 0 ICPs found
- 0 personas found
- 0 pain points found

Cannot generate offers without this foundational knowledge.

Steps to fix:
1. Process onboarding materials into the knowledge base
2. Verify nodes are created in knowledge_base/
3. Run this command again
```

### If offer inventory already exists:
```
⚠️  Offer inventory already exists for XP Labs

Found existing file:
00_foundation/messaging/offer-inventory/offer-inventory.md

Current inventory:
- Total offers: [N]
- Tested: [N] offers
- Test history: [N] tests logged

Options:
1. Keep existing inventory (cancel this command)
2. Refresh inventory (add new offers, preserve test history)
   → Run: /refresh-offer-inventory
3. Replace inventory (WARNING: loses all test history)
   → Type 'replace' to confirm

What would you like to do?
```

If user types 'replace', proceed with regeneration (warn again about data loss).
Otherwise, stop.

---

## Quality Standards

**Every generated offer must have:**
- ✅ Clear value proposition (WHAT)
- ✅ Generic (no packaging specificity)
- ✅ Generic (no ICP specificity)
- ✅ Generic (no persona specificity)
- ✅ Derived from XP Labs's actual services

**Offers should NOT have:**
- ❌ Packaging details (audit, checklist, etc.) - that's for campaign ideation
- ❌ ICP specificity - that's for campaign ideation
- ❌ Persona specificity - that's for campaign ideation
- ❌ Specific delivery mechanisms - that's for campaign ideation

**Service coverage requirements:**
- ✅ All major services represented
- ✅ Roughly balanced distribution (no single service dominates)
- ✅ 8-10 offers total after user approval

---

## Success Criteria

**Successful execution means:**
1. ✅ 8-10 high-quality generic offers generated
2. ✅ Mix of MVO and Reframe approaches
3. ✅ Balanced coverage across ALL client services
4. ✅ User approved all offers (with edits if needed)
5. ✅ offer-inventory.md created with approved offers
6. ✅ offer-performance-log.md created (empty, ready to track)
7. ✅ User can immediately use `/generate-campaign-ideas` with this inventory
8. ✅ Offers are generic enough to be contextualized in multiple ways

---

**End of command specification.**
