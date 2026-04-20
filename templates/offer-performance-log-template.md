---
client: xp-labs
created: [YYYY-MM-DD]
last_updated: [YYYY-MM-DD]
total_tests: 0
---

# Offer Performance Log - XP Labs

**Purpose:** Chronological record of all offer tests across campaigns. Tracks multi-dimensional performance: Offer + Packaging + ICP + Persona combinations.

**Total tests logged:** 0
**Last updated:** [YYYY-MM-DD]

---

## How to Use This File

This file is a **chronological log** (newest first) that records:
- Which **offer** was used (from offer inventory)
- How it was **packaged** (audit, checklist, tool, guide, etc.)
- Which **ICP** was targeted
- Which **persona** was addressed
- **Performance results** (open rate, reply rate, meetings)
- **Outcome** (success/failure/inconclusive)
- **Key learnings**

**Multi-dimensional tracking enables pattern recognition:**
- Which offers work universally
- Which packaging formats resonate with specific ICPs
- Which persona combinations respond better
- Which offer + packaging + ICP combinations are winners

**After each campaign review**, add an entry linking the campaign to the specific combination tested.

**Cross-reference with:**
- `offer-inventory.md` - Master list of all offers with aggregated performance
- `launched-campaigns/[year]/[month]/week_N/` - Detailed campaign execution
- `weekly-sitreps/` - Strategic analysis and decisions

---

## Test Entry Template

Use this format when adding a new test:

```markdown
## [YYYY-MM-DD]: Offer #[N] + [Packaging] for [ICP] - [Campaign Name]

**Campaign ID:** [C-XXX]
**Offer used:** #[N] - [Offer Name from inventory]
**Packaged as:** [Audit | Checklist | Calculator | 1-pager | Direct booking | Template | Loom recording]
**ICP:** [[icp-slug]]
**Persona:** [[persona-slug]]

**Combination:** Offer #[N] AS [Packaging] FOR [[icp-slug]] + [[persona-slug]]

**Performance:**
- Emails sent: [N]
- Open rate: [X]%
- Reply rate: [X]%
- Meetings booked: [N]
- Meeting rate: [X]%

**Outcome:** ✅ Success (>5% reply) | ❌ Failed (<3% reply) | 🟡 Inconclusive (3-5% reply or low sample)

**What worked:**
- [Element 1]
- [Element 2]

**What didn't work:**
- [Element 1]
- [Element 2]

**Learning:**
[1-2 sentence summary of what we learned about this COMBINATION]

**Packaging insight:**
[Did this packaging format work well for this ICP/persona? Would a different format work better?]

**Campaign location:**
`00_foundation/messaging/launched campaigns/[YEAR]/[MONTH]/week_[N]/launched_campaigns_week_[N]_[month]_[year].md`

---
```

---

## [Entries will be added here after campaigns complete]

(No tests logged yet. After first campaign review, entries will appear here in reverse chronological order.)

---

## Summary Statistics (Auto-calculated)

**Most Tested Offers:**
(Will populate after multiple tests)

**Highest Success Rate Offers:**
(Will populate after multiple tests)

**Most Effective Packaging Formats:**
(Will populate - e.g., "Audits: 12% avg reply | Checklists: 8% avg reply | Calculators: 10% avg reply | 1-pagers: 7% avg reply | Direct booking: 5% avg reply | Templates: 9% avg reply | Loom recordings: 11% avg reply")

**Best Performing ICP Combinations:**
(Will populate - e.g., "[[pet-brands]] + [[founder]]: 15% avg reply")

**Best Performing Persona Combinations:**
(Will populate)

**Winning Combinations:**
(Will populate - e.g., "Offer #3 AS Audit FOR [[pet-brands]] + [[founder]]: 15% reply (3 tests)")

---

## Pattern Recognition

**Offer Patterns:**
(Which offers work universally across packaging/ICPs)
- Example: "Offer #5 validated across 3 different ICP combinations"

**Packaging Patterns:**
(Which formats resonate with which audiences)
- Example: "Audits outperform checklists for founder persona (12% vs 6%)"

**ICP Patterns:**
(Which ICPs respond to what)
- Example: "[[pet-brands]] respond well to diagnostic offers (11% avg)"

**Persona Patterns:**
(Which personas respond better)
- Example: "Founders respond 2x better than VPs (10% vs 5%)"

**Anti-Patterns Identified:**
(Combinations that consistently fail)
- Example: "Offer #7 as checklist fails consistently (<3% reply across 3 tests)"

**Strategic Insights:**
(High-level learnings about what works for this client)

---

## Notes

- This log tracks multi-dimensional combinations: Offer + Packaging + ICP + Persona
- Performance isn't just about the offer - it's about the entire combination
- Pattern recognition identifies what works at each dimension (offer, packaging, ICP, persona)
- This log is maintained automatically when running `/cold-email-review`
- Each entry links back to the campaign file for full details
- Aggregated performance is tracked in `offer-inventory.md` per offer
- Use this log to identify cross-campaign patterns and make strategic decisions
