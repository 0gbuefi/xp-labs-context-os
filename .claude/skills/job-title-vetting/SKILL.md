---
name: job-title-vetting
description: Vet job titles in prospect CSVs using contextual governance reading, compound title decomposition, and target role matching for cold email targeting
model: inherit
---

# Job Title Vetting

## Purpose

Target role classification system that vets prospect job titles for cold email targeting. Reads compound titles contextually — understanding what each person actually leads, what seniority governs what domain, and whether a keyword represents a governed responsibility or just organizational context. Produces three new columns — `seniority_answer`, `persona_answer`, and `WHY` — so you can quickly filter to qualified leads.

---

## When to Use

- User provides a prospect CSV and asks to "vet", "classify", "filter", or "prioritize" by job title
- Before launching a cold email campaign to ensure the list matches the target audience
- After scraping a directory or buying a list that needs title-based qualification

---

## Inputs (Gather From User Each Run)

### Required

1. **CSV file path**
2. **Target roles** — the user defines (seniority + persona) pairs. Ask:
   - "What roles are we targeting? (e.g., CTO, VP of Engineering, Head of AI)"
   - Each role implies both a seniority level AND a persona domain
3. **Persona keywords** — derived from target roles, with match types:
   - STANDALONE: matches anywhere as a word boundary (e.g., "engineering")
   - PHRASE: full phrase must appear (e.g., "digital transformation")
   - CONTEXTUAL: only valid inside a specific title pattern (e.g., "information" only inside "Chief Information Officer")

### Optional (Use Defaults If Not Specified)

4. **Per-run forbidden patterns** — scenario-specific exclusions (e.g., "Associate Director", "Coach")
5. **Extra noise phrases** — beyond defaults (e.g., "with a focus on")

---

## Core Concept: Governance-Based Matching

### The Fundamental Question

For every title, ask: **does this seniority PRESIDE OVER this persona domain?**

Not co-presence. Not adjacency. **Governance.** The seniority and the persona keyword must be in a direct authority relationship — the person must actually lead, own, or be responsible for that domain.

### Target Roles

Each run defines a set of **target roles** — (seniority, persona) pairs. A title is FIT if the person's governed domain matches any target role.

```
Example target roles:
- (C-Level, Information)     → CIO
- (C-Level, Technology)      → CTO
- (VP, Engineering)          → VP of Engineering
- (Head, Engineering)        → Head of Engineering
- (Chief, AI)                → Chief AI Officer
- (Head, AI)                 → Head of AI
- (Director, AI)             → Director of AI
- (VP, Digital Transformation)
- (Head, Digital Transformation)
- (Chief, Digital Transformation)
```

The seniority level is NOT global — it's per-persona. "Director" is allowed for AI but not for Engineering in this example.

---

## The 14 Principles of Contextual Title Reading

### 1. Governance Is the Core Question

Every classification decision reduces to: does this seniority **govern** this persona domain? The seniority and persona must be in a direct authority relationship.

```
"Head of SAP Java Solutions / Software Engineering Manager II"
→ Head governs SAP Java Solutions, NOT Engineering
→ Manager governs Software Engineering
→ Two separate governance relationships
```

A persona keyword merely appearing somewhere in the title is NOT enough. It must be in the domain that the seniority presides over.

### 2. "What They Lead" vs "Where They Sit"

The deepest distinction in compound titles. Some parts describe what the person **leads** (their governed domain). Other parts describe where they **sit** (their department, org, team, rank context).

```
"Managing Director & Global Head of AI Agents and Search (Engineering & Applied Research)"
→ LEADS: AI Agents and Search
→ SITS IN: Engineering & Applied Research department
→ Match: Head of AI (not Head of Engineering)

"Head - Systems Design | Digital Platform Engineering (eCommerce, IoT and Cloud)"
→ LEADS: Systems Design
→ SITS IN: Digital Platform Engineering area
→ UNFIT for Engineering (Engineering is context, not governed domain)

"Head of Sponsored Ads (Senior Director, Engineering)"
→ LEADS: Sponsored Ads
→ SITS IN: Engineering org at Senior Director rank
→ UNFIT for Engineering
```

**The rule:** Persona keywords only count when they appear in what the person **leads** — their governed domain. Keywords that appear in organizational context (where they sit, their department, their rank clarification) do not create a match.

### 3. Parenthetical Content Is Contextual by Default

Parentheticals in titles almost always clarify organizational context — rank, department, acronyms, geographic scope. They rarely define a second governed role.

**Context (ignore for persona matching):**
```
"(Senior Director, Engineering)" → rank + department
"(Engineering & Applied Research)" → department name
"(eCommerce, IoT and Cloud)" → focus area / product scope
"(Europe)" → geographic scope
```

**Part of the role name (keep):**
```
"(AICoE)" → acronym clarifier for "AI Center of Excellence"
"(EA)" → acronym clarifier for "Enterprise Architecture"
"(COE)" → acronym clarifier for "Center of Excellence"
```

**The test:** Does the parenthetical describe a domain this person has authority over, or does it describe the organizational box they sit in? If it contains a seniority keyword alongside a domain word (like "Senior Director, Engineering"), it's almost certainly a rank/department clarifier.

### 4. Separator Meaning Depends on Context, Not the Character

No rigid rules about what `,` or `|` or `/` or `-` "always means." Each separator can serve different purposes depending on what comes before and after it. Instead of mechanical separator rules, evaluate what each separated piece IS:

- Does it have its own seniority keyword? → It may be a self-governed role
- Does it look like a department, team, or product name? → It's likely context
- Does it contain a persona keyword that the title's seniority logically governs? → It may be a governed domain
- Is it a standalone domain word after a titled role? → It may inherit seniority (if the structure implies shared governance)

**Examples of the same separator meaning different things:**

```
Comma as role separator:
"Managing Director, Head of Engineering" → two roles

Comma as domain separator:
"VP of Finance, Digital Transformation" → one seniority, two domains

Pipe as context separator:
"Head - Systems Design | Digital Platform Engineering" → title | department

Slash as role separator:
"Head of SAP Java Solutions / Software Engineering Manager II" → two distinct roles
```

### 5. Seniority Modifier vs Standalone Seniority

When a higher and lower seniority appear in the **same continuous phrase**, the lower one is a modifier describing the role shape, not the governing rank:

```
"Senior Vice President Digital Transformation Lead"
→ SVP is the governing seniority
→ "Lead" is a modifier (same phrase, after SVP)
→ Evaluate as: (SVP, Digital Transformation) → FIT
```

When seniorities are in **separate segments** (after a comma, dash, etc.), each stands on its own:

```
"Vice President II, Digital Transformation Lead"
→ Segment 1: VP (no persona)
→ Segment 2: Lead governs DT (standalone seniority)
→ (Lead, DT) → Lead not accepted for DT → UNFIT
```

### 6. Noise Filtering — Skills vs Responsibilities

Phrases that describe expertise, experience, or background are NOT role responsibilities. Strip them before evaluating:

```
Default noise phrases:
- "with expertise in ..."
- "with experience in ..."
- "with a background in ..."
- "with a focus on ..."
- "specializing in ..."
- "focused on ..."
- "within the [X] sector/industry/space"
- "at [Company Name] ..." (company reference at end of title)
- "Office of the Chief [X] Officer" / "Office of the CIO/CTO/..." (department context)
```

```
"SVP Lead Architect with expertise in Digital Transformation within the banking technology sector"
→ After stripping: "SVP Lead Architect"
→ DT was a skill mention, not a governed domain → UNFIT
```

### 7. Support Roles Are Always UNFIT

People who serve executives are not executives. The word "to" connecting a support role to an executive title is the key signal:

```
"Executive Assistant To Chief Information Officer" → serves CIO, is not CIO
"Executive Administrative Assistant to SVP & Chief Information Officer" → serves CIO
"Sr. Executive Assistant to the EVP, Chief Technology Officer" → serves CTO
"Secretary to the VP of Engineering" → serves VP
```

This is permanently in the global forbidden list — not configurable per run.

### 8. Seniority Inheritance Only When Governance Extends

Seniority can inherit from a titled segment to a domain-only segment — but only when the title structure implies the seniority **covers** that domain:

**Inheritance works:**
```
"Vice President of Finance, Digital Transformation"
→ VP covers both Finance and DT → DT inherits VP

"Vice President - Production Support, Change Management & Digital Transformation"
→ VP covers all three domains → DT inherits VP
```

**Inheritance should NOT happen when:**
- The domain-only segment is organizational context (department, team name)
- The segment appears after a pipe or inside parentheses as a "where they sit" label
- The relationship between segments doesn't imply shared governance

### 9. Per-Run Configurability

The skill framework (governance reading, decomposition principles, modifier rules, global forbidden) is **permanent**. These don't change between runs.

What changes each run:
- Target roles (which seniority + persona pairs to match)
- Persona keywords and match types
- Per-run forbidden patterns (e.g., "Associate Director" excluded this run, valid next run)
- Extra noise phrases

### 10. Governed Zone — Dashes Within a Segment

When a segment contains a dash (`-` or `–`), determine what's before and after it. If seniority + a substantive non-persona domain appears BEFORE the dash, content after the dash is organizational context — not a governed domain.

```
"Head of Design - IBM Ecosystem Engineering EMEA"
→ Pre-dash: "Head of Design" — seniority + domain (Design)
→ Post-dash: "IBM Ecosystem Engineering EMEA" — org/company context
→ Only match persona keywords in "Head of Design" → no engineering match → UNFIT

"Senior Director - Artificial Intelligence & Automation"
→ Pre-dash: "Senior Director" — seniority only, no domain
→ Post-dash IS the governed domain → AI matches → FIT

"Section Head - Reliability Engineering"
→ Pre-dash: "Section Head" — "Section" is a scope modifier, not a domain
→ Whole segment is governed → engineering matches → FIT
```

**Scope modifiers** that don't count as governed domains: sub, chapter, sub-chapter, section, systems, functional, regional, global, deputy, associate, assistant, acting, interim, co, joint, dual.

### 11. Seniority-Already-Governs — Context Blocking for Inheritance

When a single titled segment already governs a **non-persona domain** (from its pre-dash content), ALL subsequent domain-only inheriting segments are treated as organizational context (where they sit), NOT additional governed domains.

```
"Head of Technical Support Services, Corporate Engineering"
→ Head governs "Technical Support Services" (non-persona domain)
→ "Corporate Engineering" is WHERE they sit → blocked → UNFIT

"Head of Finance - Product Engineering Hardware, Meta Reality Labs"
→ Head governs "Finance" (non-persona domain)
→ "Product Engineering Hardware" is post-dash context (Principle 10)
→ Even if it weren't, Finance governance blocks further inheritance

"Director, Software Development, Artificial Intelligence Group"
→ Director is STANDALONE (no domain in its segment)
→ All subsequent segments are governed domains → AI matches → FIT
```

**Exception — multiple titled segments:** When there are multiple segments with their own seniority, the person holds multiple senior roles and governs broadly. Don't block inheritance.

```
"Director, Head of Health and Observability, Quality Engineering"
→ 2 titled segments (Director, Head) → broad governance
→ "Quality Engineering" inherits → FIT
```

**Exception — list continuations:** Segments starting with "and" are continuations of a comma-separated list, not context.

```
"Senior Principal Research Scientist/Head of Cell, Gene, and Protein Engineering"
→ "and Protein Engineering" continues the list "Cell, Gene, and Protein Engineering"
→ Inherits Head → FIT
```

### 12. Org Unit Words Are Always Context

Segments ending with organizational structure words — Department, Lab, Team, Center, Unit, Division, Office, Practice, Function, Hub, Studio — are ALWAYS naming an organizational unit. Block inheritance into these regardless of other context.

```
"Systems Section Head, Engineering Management Department"
→ "Department" = org unit word → ALWAYS context → UNFIT

"Director of Data Science & Engineering, Artificial Intelligence Lab"
→ "Lab" = org unit word → context → UNFIT
```

**Exception — "Group":** The word "Group" is ambiguous — it can mean an org unit OR a governed domain. "Group" is only blocked when seniority already governs a domain (Principle 11), not unconditionally.

```
"Director, Software Development, Artificial Intelligence Group"
→ Director is standalone → "Group" not unconditionally blocked → FIT
```

### 13. "Office of the [C-Level]" Is Department Context

"Office of the Chief Information Officer" is a department name, not a role claim. Strip it as noise. The person works IN that office, they are NOT that executive.

```
"Director of Operations - Office of the Chief Information Officer"
→ Strip "Office of the Chief Information Officer" → "Director of Operations" → UNFIT

"IT Strategy Partner, Office of the Chief Information Officer (OCIO)"
→ Strip → "IT Strategy Partner" → UNFIT
```

### 14. Company Names and Non-Seniority Compounds

**Company names in titles:** "at [Company Name]" at the end of a title refers to the employer, not the domain. Strip before evaluation.

```
"Head - Administration & Facility at Jacobs Engineering Delhi (Gurgaon) Office"
→ "Jacobs Engineering" is the company name → strip "at Jacobs Engineering..."
→ "Head - Administration & Facility" → no engineering match → UNFIT
```

**Non-seniority "Head" compounds:** Some technical terms use "Head" in a non-seniority way. These should not be detected as seniority:
- "Cylinder Head" (engine part)
- "Write Head" (disk drive component)
- "Overhead" (not "Over" + "Head")

```
"Engineering Group Manager - Cylinder Head & Block Design"
→ "Cylinder Head" is not seniority → only Manager detected
→ Manager not accepted for Engineering → UNFIT
```

---

## Step-by-Step Process

### Step 1: Gather Scenario Configuration

Ask the user for:

```
1. Which CSV are we vetting?
2. What target roles? (list of seniority + persona pairs)
3. For each persona keyword, what's the matching rule? (STANDALONE, PHRASE, CONTEXTUAL)
4. Any per-run forbidden patterns? (e.g., "Associate Director", "Coach")
5. Any extra noise phrases to filter?
```

### Step 2: Confirm Configuration

Present the full config back to the user:

```
TARGET ROLES:
  1. C-Level + Information (CIO)
  2. C-Level + Technology (CTO)
  3. VP + Engineering
  ...

PERSONA KEYWORDS:
  - "engineering" (STANDALONE)
  - "digital transformation" (PHRASE)
  - "artificial intelligence" (PHRASE)
  ...

GLOBAL FORBIDDEN (permanent):
  [see Global Forbidden section]

PER-RUN FORBIDDEN:
  - Associate Director
  - [any user additions]

NOISE PHRASES:
  - "with expertise in", "with experience in", ...

CSV: [path]
```

Get confirmation before proceeding.

### Step 3: Test Run

- Sample N random rows (user specifies, default 30)
- Run the full pipeline on the sample
- Output results as a JSON file for the user to review
- Print a summary: `Sample: N rows | FIT: X | UNFIT: Y`
- Ask the user to vet the results before proceeding

### Step 4: Full Run

After user approves the test:
- Run on ALL rows in the CSV
- Add three new columns: `seniority_answer`, `persona_answer`, `WHY`
- Place columns immediately after the `Job title` column
- Print a full summary table and FIT/UNFIT counts
- Delete the test JSON file

### Step 5: Idempotency Check

If `seniority_answer`, `persona_answer`, or `WHY` columns already exist, overwrite them rather than duplicating.

---

## Seniority Detection

### Seniority Keywords (Ranked)

Detected within each segment independently. Ranked from highest to lowest:

| Rank | Pattern | Match Logic |
|------|---------|-------------|
| 1 | C-Level Acronyms | CTO, CIO, CEO, CFO, COO, CMO, CPO, CISO, CLO, CHRO, CDO, CAO, CAIO |
| 2 | Chief + Officer | "Chief" AND "Officer" in same segment |
| 3 | Chief (standalone) | "Chief" without "Officer" (e.g., "Chief of AI") |
| 4 | President | Only if NOT preceded by "Vice", "Assistant", "Associate" |
| 5 | EVP / Executive Vice President | |
| 6 | SVP / Senior Vice President | |
| 7 | VP / Vice President | Including "Vice President II", "VP2", etc. |
| 8 | Executive Director | Context-dependent — can be VP-equivalent or Director-equivalent |
| 9 | Head / Global Head / Section Head / Deputy Head / Sub-Chapter Head | Excludes non-seniority compounds: Cylinder Head, Write Head |
| 10 | Senior Director | |
| 11 | Managing Director | Context-dependent — VP-equivalent in finance, Director-level elsewhere |
| 12 | Director | |
| 13 | Lead | Only when standalone seniority (see Principle 5) |
| 14 | Manager | |

### Global Forbidden (Permanent — Every Run)

These override everything — if found anywhere in the title, the entire title is UNFIT. These represent roles that are **never valid targets** for any cold email campaign:

| Pattern | Reason |
|---------|--------|
| Executive Assistant, Administrative Assistant, Personal Assistant | Admin/support role |
| Assistant to, Secretary to, Aide to | Support role serving an executive (see Principle 7) |
| Chief of Staff | Support role, not decision-maker |
| Intern, Trainee, Apprentice | Too junior |
| Former, Ex-, Retired | No longer in role |

**Important:** These are permanent and NOT configurable per-run. Per-run exclusions (like "Associate Director" or "Coach") go in the per-run forbidden list.

### Per-Run Forbidden

Configured by the user each run. Seniority levels or title patterns excluded for this specific campaign but potentially valid in other campaigns.

```
Example per-run forbidden:
- "Associate Director" (too junior for this campaign)
- "Coach" (irrelevant for this persona)
- "AVP" (too junior)
```

---

## Persona Matching

### Keyword Types

**STANDALONE** — word boundary match anywhere in the governed domain:
```
"engineering" → matches "Head of Engineering", "VP Engineering Operations"
```

**PHRASE** — full phrase must appear. Auto-handles "and"/"&" variants:
```
"digital transformation" → matches "VP, Digital Transformation"
"artificial intelligence" → matches "Head of Artificial Intelligence and Machine Learning"
```

**CONTEXTUAL** — only valid inside a specific pattern:
```
"information" only inside "Chief Information Officer" / "CIO"
"technology" only inside "Chief Technology Officer" / "CTO"
```

### The Governance Check

A persona keyword match is only valid when:
1. The keyword appears in a segment where the seniority **governs** that domain
2. The keyword is NOT in organizational context (department label, parenthetical rank+dept, "where they sit")
3. The keyword is NOT in a noise phrase (expertise, experience mention)

---

## Evaluation Algorithm

For each title:

```
1.  Check global forbidden → if match, UNFIT immediately
2.  Check per-run forbidden → if match, UNFIT immediately
3.  Strip noise phrases (expertise mentions, "at [Company]", "Office of the CIO", etc.)
4.  Analyze parenthetical content:
    - C-Level acronyms in parens (CDO, CTO) → strip (if real, full title confirms)
    - Rank + department patterns → strip as context
    - Multi-word dept context without seniority → strip
    - Short acronyms (EA, AICoE) → keep as part of role name
5.  Split into segments (on commas, semicolons, pipes, spaced-slashes)
    - Protect commas inside parentheses from splitting
    - Track which segments came after a pipe (likely context)
6.  Expand segments:
    - Split on & when BOTH sides have seniority → separate governance chains
    - Split on no-space / when at least ONE side has seniority → separate roles
7.  For each segment:
    a. Strip trailing rank clarifiers ("- Snr. Director" at end)
    b. Detect seniority (highest wins within a segment — modifier rule)
    c. Determine governed zone (Principle 10 — dash logic)
    d. Detect persona keywords in the governed zone only
8.  Match self-titled segments first:
    - Skip post-pipe segments that lack their own seniority
    - If segment has seniority + persona keyword → check target roles → FIT if matched
9.  Inheritance for domain-only segments:
    a. Block if seniority already governs a non-persona domain (Principle 11)
    b. Block if segment ends with org unit word (Principle 12)
    c. Allow if segment starts with "and" (list continuation)
    d. Otherwise, inherit highest seniority → check target roles
10. If ANY governed segment matches a target role → FIT
    If NO governed segment matches → UNFIT with specific reason
```

### Output Decision

- **seniority_answer**: the matched seniority level from the winning segment (e.g., "Head", "VP", "C-Level (CTO)")
- **persona_answer**: the matched target role label (e.g., "Head of Engineering", "CTO", "Director of AI")
- **WHY**: explanation of governance — which segment matched, what seniority governs what domain

For UNFIT:
- **seniority_answer**: the highest seniority found, or the forbidden pattern matched, or "No seniority found"
- **persona_answer**: "UNFIT"
- **WHY**: specific reason citing the principle that applies (e.g., "Engineering appears in parenthetical dept context, not governed domain", "Support role: Executive Assistant to CIO", "Seniority 'Lead' not accepted for DT persona")

---

## Worked Examples

### Example 1: Compound with hidden persona match
```
Title: "Head of Employee Learning and Development, Artificial Intelligence and Machine Learning"
Reading: Head governs two domains — L&D and AI/ML (comma separates co-equal domains)
Segment 2 "AI and ML" inherits Head seniority
Check: (Head, AI) → matches target role → FIT
```

### Example 2: Multiple titled roles — governance is per-segment
```
Title: "Managing Director, Head of Securities Lending Engineering, Aladdin"
Reading: MD is one role, Head of Engineering is another (self-titled segment)
Head governs "Securities Lending Engineering"
Check: (Head, Engineering) → FIT
```

### Example 3: VP covering multiple domains
```
Title: "Vice President - Production Support, Change Management & Digital Transformation"
Reading: VP governs all three domains (Production Support, Change Mgmt, DT)
DT inherits VP
Check: (VP, Digital Transformation) → FIT
```

### Example 4: Expertise mention — not a governed domain (UNFIT)
```
Title: "SVP Lead Architect with expertise in Digital Transformation within the banking technology sector"
After noise stripping: "SVP Lead Architect"
DT was mentioned as a skill, not a governed domain → UNFIT
```

### Example 5: SVP with Lead modifier
```
Title: "Senior Vice President Digital Transformation Lead - Data Analytics and Reporting"
Reading: SVP is governing seniority. "Lead" is a modifier in the same phrase (Principle 5).
Check: (SVP, Digital Transformation) → FIT
```

### Example 6: VP + Lead in separate segments (UNFIT)
```
Title: "Vice President II, Digital Transformation Lead"
Reading: VP governs segment 1 (no persona). "Lead" is standalone in segment 2 (Principle 5).
Lead governs DT. Lead not accepted for DT.
→ UNFIT
```

### Example 7: Support role serving an executive (UNFIT)
```
Title: "Executive Administrative Assistant to SVP & Chief Information Officer"
Reading: "Assistant to" → serves the CIO, is not the CIO (Principle 7)
Global forbidden → UNFIT
```

### Example 8: Parenthetical is department context (UNFIT)
```
Title: "Head of Sponsored Ads (Senior Director, Engineering)"
Reading: Leads Sponsored Ads. "(Senior Director, Engineering)" = rank + dept (Principle 3)
Engineering is where they sit, not what they lead (Principle 2) → UNFIT
```

### Example 9: Parenthetical is department — match the governed domain instead
```
Title: "Managing Director & Global Head of AI Agents and Search (Engineering & Applied Research)"
Reading: Head governs "AI Agents and Search". "(Engineering & Applied Research)" = department (Principle 3)
AI is in the governed domain. Engineering is in the "where they sit" context.
Check: (Head, AI) → FIT as Head of AI (not Head of Engineering)
```

### Example 10: Dual role with slash — separate governance (UNFIT)
```
Title: "Head of SAP Java Solutions / Software Engineering Manager II"
Reading: Two distinct roles separated by slash.
Head governs SAP Java Solutions (no target persona).
Manager governs Software Engineering (Manager not accepted for Engineering).
→ UNFIT
```

### Example 11: Section Head pattern (FIT)
```
Title: "IT Operations & Systems Engineering Section Head"
Reading: "Section Head" of "IT Operations & Systems Engineering"
Head governs a domain containing "engineering"
Check: (Head, Engineering) → FIT
```

### Example 12: Pipe separates title from focus area (UNFIT)
```
Title: "Head - Systems Design | Digital Platform Engineering (eCommerce, IoT and Cloud)"
Reading: Leads Systems Design. "Digital Platform Engineering" after pipe = focus area/department (Principle 2)
Engineering is where they sit, not what they lead → UNFIT
```

### Example 13: Deputy Head (FIT when accepted)
```
Title: "Deputy Head of Geospatial Engineering"
Reading: "Deputy Head" — still a Head-level role
Head governs "Geospatial Engineering"
Check: (Head, Engineering) → FIT (if Deputy is accepted for this run)
```

### Example 14: CTO with domain inheritance
```
Title: "CTO, Digital Transformation"
Reading: CTO (C-Level) governs DT domain
Check: (C-Level, Technology) → matches CTO → FIT
Also: (C-Level, Digital Transformation) → FIT
```

### Example 15: & separates two governance chains (UNFIT)
```
Title: "Director Software Engineering & Head Salesforce COE"
Reading: & splits because both sides have seniority (Director, Head).
  Chain 1: Director governs Software Engineering (Director not accepted for Eng)
  Chain 2: Head governs Salesforce COE (no target persona)
→ UNFIT
```

### Example 16: Governed zone blocks post-dash Engineering (UNFIT)
```
Title: "Head of Finance - Product Engineering Hardware, Meta Reality Labs"
Reading: "Head of Finance" — seniority + domain (Finance) before dash
  Post-dash "Product Engineering Hardware" is org context (Principle 10)
  "Meta Reality Labs" is company context
→ UNFIT (Head of Finance, not Head of Engineering)
```

### Example 17: Seniority-already-governs blocks inheritance (UNFIT)
```
Title: "Head of Technical Support Services, Corporate Engineering"
Reading: Head governs "Technical Support Services" (non-persona domain)
  "Corporate Engineering" is WHERE they sit (Principle 11)
→ UNFIT (Head of Support, not Head of Engineering)
```

### Example 18: Standalone seniority — all segments governed (FIT)
```
Title: "Director, Software Development, Artificial Intelligence Group"
Reading: Director is standalone (no domain in its segment)
  All comma segments are governed domains: Software Dev, AI Group
  (Director, AI) matches Director of AI
→ FIT
```

### Example 19: No-space slash separates dual role (FIT)
```
Title: "Senior Principal Research Scientist/Head of Cell, Gene, and Protein Engineering"
Reading: Slash separates two roles (Head has seniority → expand)
  Role 1: Senior Principal Research Scientist (no target match)
  Role 2: Head of Cell, Gene, and Protein Engineering
  "and Protein Engineering" is a list continuation → inherits Head
  (Head, Engineering) → FIT
```

### Example 20: Office of the CIO is department context (UNFIT)
```
Title: "Director of Operations - Office of the Chief Information Officer"
Reading: "Office of the Chief Information Officer" stripped as dept context
  Remaining: "Director of Operations"
  No target persona match → UNFIT
```

### Example 21: Company name in title (UNFIT)
```
Title: "Head - Administration & Facility at Jacobs Engineering Delhi (Gurgaon) Office"
Reading: "at Jacobs Engineering Delhi Office" stripped (company name)
  "(Gurgaon)" stripped (location context)
  Remaining: "Head - Administration & Facility"
  No target persona match → UNFIT
```

### Example 22: Post-pipe segment with own seniority (FIT)
```
Title: "Senior Director | Head of Engineering for Rocket Growth"
Reading: Post-pipe segment "Head of Engineering for Rocket Growth" has its own seniority (Head)
  Self-titled segments with own seniority are evaluated independently
  (Head, Engineering) → FIT
```

### Example 23: Company/division after dash doesn't block inheritance (FIT)
```
Title: "Senior Director - Pfizer Digital; Artificial Intelligence, Data, and Analytics"
Reading: Pre-dash "Senior Director" has no domain → standalone seniority
  "Pfizer Digital" after dash is company/division context (not a governed domain)
  Semicolon splits: "AI" inherits Senior Director
  (Senior Director, AI) → FIT as Director of AI
```

---

## Important Notes

- **Governance over co-presence.** The seniority must preside over the persona domain — not just appear in the same title.
- **"What they lead" over "where they sit."** Always distinguish governed domain from organizational context.
- **Parentheticals are context by default.** Unless they're acronym clarifiers, treat them as org context.
- **No rigid separator rules.** Read what each part of the title means contextually.
- **Test before full run.** Sample N rows as JSON → user vets → iterate → then full CSV.
- **Target roles are defined per run.** The skill doesn't assume which seniority+persona pairs are valid.
- **Noise phrases are stripped first.** Expertise/experience mentions are not governed domains.
- **Modifier rule is segment-scoped.** Lower seniority is a modifier only when in the same phrase as a higher seniority.
- **Support roles are always UNFIT.** "Assistant to CIO" is not CIO. Permanently forbidden.
- **No inference.** If the keyword isn't there, it's UNFIT. Don't map related terms.
- **Never lose data.** Original columns preserved. Vetting columns are additions.
- **Idempotent.** Safe to re-run — existing vetting columns get overwritten, not duplicated.
- **Global forbidden is permanent.** Per-run forbidden is configured each run.
