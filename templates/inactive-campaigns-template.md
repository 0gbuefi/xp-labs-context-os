---
client: xp-labs
last_updated: [YYYY-MM-DD]
inactive_campaigns_count: 0
total_killed: 0
total_paused: 0
---

# Inactive Campaigns - XP Labs

**Last updated:** [YYYY-MM-DD]

Archive of killed, paused, and deprecated campaigns with learnings and anti-patterns documented.

**Purpose:** Keep historical record of what didn't work to avoid repeating mistakes and preserve institutional knowledge.

---

## Killed Campaigns (Permanent)

### ❌ [Campaign ID]: [Campaign Name] ([Variant Letter])

**Status:** ❌ Killed - Permanent
**Killed date:** [YYYY-MM-DD]
**Performance:** [X]% open, [Y]% reply, [Z]% meeting rate
**Sample size:** [N] sends

**Campaign Location:**
- **Week:** Week [N]
- **Month:** [Month YYYY]
- **File path:** `00_foundation/messaging/launched campaigns/[YEAR]/[MONTH]/week_[N]/launched_campaigns_week_[N]_[month_lower]_[year].md`
- **Campaign section:** Campaign [N], Variant [Letter]

**Campaign Details:**
- **Target ICP:** [[icp-segment]]
- **Persona:** [[persona-name]]
- **Pain point:** [[pain-point]]
- **Offer:** [Offer description]
- **Approach:** [Approach description]

**Why It Failed:**
[Detailed root cause analysis]

**Comparison to Winning Variant:**
[If applicable, compare to better-performing variant]

**What We Learned:**
[Key learnings and insights]

**Anti-Pattern Created:**
- `[[anti-pattern-name]]` - [Description]

**Knowledge Base Updates:**
[List of knowledge base updates made/needed]

**Never Test Again:**
- ❌ [Specific element 1]
- ❌ [Specific element 2]

**Could Be Revised If:**
[Conditions under which this could be revisited, if any]

---

## Paused Campaigns (May Resume)

### 🟡 [Campaign ID]: [Campaign Name] ([Variant Letter])

**Status:** 🟡 Paused (Not killed - may resume for testing)
**Paused date:** [YYYY-MM-DD]
**Performance:** [X]% open, [Y]% reply, [Z]% meeting rate
**Sample size:** [N] sends

**Campaign Location:**
- **Week:** Week [N]
- **Month:** [Month YYYY]
- **File path:** `00_foundation/messaging/launched campaigns/[YEAR]/[MONTH]/week_[N]/launched_campaigns_week_[N]_[month_lower]_[year].md`
- **Campaign section:** Campaign [N], Variant [Letter]

**Campaign Details:**
- **Target ICP:** [[icp-segment]]
- **Persona:** [[persona-name]]
- **Pain point:** [[pain-point]]
- **Offer:** [Offer description]
- **Approach:** [Approach description]

**Why It's Paused:**
[Reason - usually outperformed by another variant, or needs more data]

**What Worked:**
[Elements that showed promise]

**What Could Be Improved:**
[Potential improvements]

**Could Resume If:**
1. [Condition 1]
2. [Condition 2]
3. [Condition 3]

**Recommended Revisions If Resumed:**
- [Revision 1]
- [Revision 2]

**Knowledge Base Notes:**
[Any insights worth preserving]

---

## Summary Statistics

**Killed Campaigns:**
- Total: [N]
- Average performance before kill: [X]% open, [Y]% reply, [Z]% meeting rate
- Primary failure reasons: [List top reasons]

**Paused Campaigns:**
- Total: [N]
- Average performance: [X]% open, [Y]% reply, [Z]% meeting rate
- Primary pause reasons: [List top reasons]

**Key Learnings:**
1. [Learning 1]
2. [Learning 2]
3. [Learning 3]

---

## Anti-Patterns Documented

### 1. [[anti-pattern-name]]
**Source:** [Campaign ID] (Killed)
**Evidence:** [Performance data]
**Rule:** [What to avoid]
**Why it fails:** [Root cause]

---

## How to Use This File

**When a campaign is killed:**
1. Move from `active-campaigns.md` to this file under "Killed Campaigns"
2. Document full performance data and reasoning
3. Create anti-pattern node if new failure pattern identified
4. Update knowledge base with learnings

**When a campaign is paused:**
1. Move to "Paused Campaigns" section
2. Document why it's paused (not killed)
3. List conditions for potential resume
4. Keep as backup for future testing

**Review cadence:**
- Monthly: Review paused campaigns - should any be reactivated?
- Quarterly: Review killed campaigns - any lessons being forgotten?
- Before new campaigns: Check this file to avoid repeating mistakes

---

## Links

**Active campaigns:**
- [Active Campaigns](./active-campaigns.md)

**Synthesis files:**
- [Weekly Sit-Reps](../_synthesis/weekly-sitreps/)
- [Strategic Synthesis](../_synthesis/strategic-synthesis.md)

**Campaign archive:**
- [Launched Campaigns](./launched%20campaigns/)

---

**Last reviewed:** [YYYY-MM-DD]
**Next review:** [YYYY-MM-DD]
