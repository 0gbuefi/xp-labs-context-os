---
name: TEN_THINGS_WRONG_WITH_LIST
description: Exercise to find 10 flaws in every list before sending - if you can't find 10, you didn't look hard enough
scope: agency
domain: list-building
node_type: pattern
status: emergent
created: 2026-01-15
last_updated: 2026-01-15
tags:
  - list-building
topics:
  - list-hygiene
  - data-sourcing
  - segmentation-strategy
related_concepts:
  - "[[account-to-contact-research]]"
  - "[[list-quality-over-quantity]]"
  - "[[apollo-linkedin-data-limitations]]"
source: "GEX Wrapped 2024 by Eric Nowoslawski"
source_url: ""
date_accessed: 2026-01-15
---

# The "10 Things I Hate About You" Rule for Lists

Before sending to any list, **find 10 things wrong with it**. If you can't find 10 flaws, you didn't look hard enough. This exercise prevents wasted sends and reveals targeting gaps.

## Core Principles

- Every list has data quality issues (self-reported data, scraping errors, stale info)
- Finding problems is research, not pessimism
- Account-level filters often have more issues than contact-level filters
- Data providers can't solve for every use case perfectly
- Better to fix before sending than discover via poor results

## When to Use

Run this exercise:
- Before launching any new campaign
- After pulling list from Apollo, ZoomInfo, or Clay
- When response rates are mysteriously low
- Training team on list quality standards
- Explaining to stakeholders why targeting matters

## How to Apply

**The Exercise:**

Pull list based on initial targeting criteria. Then systematically find 10 flaws.

**Example: "Marketing Leaders at Banks"**

Initial filter: Director+ marketing titles, banking industry

**10 Things Wrong:**
1. **Sales & Marketing confusion:** Some titles include "Sales and Marketing" - do you want sales people?
2. **Self-selected industry:** Banking industry filter relies on company's LinkedIn self-selection - trust an intern's choice?
3. **Fintech contamination:** Fintech companies tagged as "banking"
4. **Consulting firms included:** Marketing consultants who serve banks, not bank employees
5. **Agencies in results:** Marketing agencies that specialize in banking vertical
6. **Executive assistants:** "Assistant to CMO" titles included in Director+ filter
7. **Company size variance:** 100-person bank ≠ 10,000-person bank (wildly different needs)
8. **No headcount filter:** Missing crucial size segmentation
9. **Keyword data errors:** Expect some companies have incorrect keywords/tags
10. **Geographic irrelevance:** May include international banks if no location filter

**You found 10. Now fix them:**
- Add negative keywords (consultant, agency, assistant)
- Add employee headcount range (1,000-10,000)
- Add geography filter (US only)
- Add keyword verification (scrape website to confirm banking vs fintech)
- Split by company size for different messaging

**Process:**
1. Pull initial list
2. Export sample (100 contacts)
3. Manually review 20 contacts
4. Document every flaw found
5. Keep going until you hit 10
6. Add filters to address each flaw
7. Re-pull list
8. Repeat exercise (find 10 more things)

**Team Training Version:**

Origin story: "Before you decide to marry someone, write down 10 things you don't like about them and ask yourself if you can live with these things long term. If you can't think of 10 things you don't like, you don't know them well enough."

**Note:** Don't tell your spouse the 10 things (a friend tried this - it didn't go well). But DO tell your team the 10 things wrong with the list.

## Evidence

[VERIFIED: GEX Wrapped 2024] "One of the best pieces of advice I was ever given was, 'Before you decide to marry someone, write down 10 things you don't like about them and ask yourself if you can live with these things long term. If you can't think of 10 things you don't like, you don't know them well enough.' What does this have to do with list building? I tell my team all the time to find 10 things wrong with a list, if you can't find 10, you didn't look hard enough."

[DATA: Marketing leaders at banks example] Listed 8 common flaws in what seems like simple targeting - proves the point.

[VERIFIED: Data provider limitations] "This is just an issue that can't really be solved by any single company so I don't blame them or any other list building company. The data is scraped directly from a source the company self-reports their data on or companies like Apollo and Zoominfo try to add more data to make their filters better but might miss the mark for just your use case."

## Related Concepts

- [[account-to-contact-research]] - Start with account filters, then move to contacts
- [[list-quality-over-quantity]] - Why fixing list quality beats increasing volume
- [[apollo-linkedin-data-limitations]] - Understanding limitations of LinkedIn-based data
