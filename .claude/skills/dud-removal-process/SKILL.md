---
name: dud-removal-process
description: Skill for removing wrong contacts (duds) from pulled lead lists by cross-referencing left-side database data with right-side LinkedIn enrichment data, then qualifying by title (Claude-vetted) and company (fuzzy-matched)
model: inherit
---

# Dud Removal Process

## Purpose

Contact qualification system that removes "duds" — wrong contacts — from pulled lead lists. Builds a full picture of each contact by reconciling left-side data (from the lead database) with right-side data (LinkedIn enrichment), determines the person's REAL title and REAL company, then qualifies both against the campaign brief. Produces three new columns — `[final] Domain`, `[final] Title`, and `WHY` — so you can immediately filter to valid contacts.

**Title vetting is done by Claude, not Python.** Python handles file I/O, operating role selection, and company fuzzy-matching. Claude reads the unique titles and makes the qualification judgment — handling compound titles, abbreviated titles, unusual framings, and edge cases that regex cannot reliably catch.

---

## When to Use

- After pulling a lead list from any database (Apollo, ZoomInfo, etc.) that has been enriched with LinkedIn data
- When a list has known data quality issues — stale titles, wrong companies, mismatched records
- Before launching any cold email campaign to strip out contacts who don't actually hold the right title at the right company
- Works for any XP Labs prospect list

---

## Inputs (Gather From User Each Run)

### Required

1. **CSV file path** — the lead list to process
2. **Context** — plain English description of what this list is (e.g., "Fortune 1000 CIOs", "Series B+ VP Engineering")
3. **ICP titles** — the job titles we're looking for (e.g., "CIO, Chief Information Officer, VP of IT")
4. **Company brief** — what companies qualify (e.g., "must be on the Fortune 1000 list", "must be a SaaS company with 200+ employees")

### Optional

5. **Reference list file path** — if the company brief references a specific list (e.g., a Fortune 1000 CSV, a target account list), provide the file so the script can fuzzy-match against it
6. **Additional disqualify titles** — beyond the default instant-disqualify list, any extra title patterns to reject for this run
7. **Title vetting rulebook** — path to a title vetting rulebook (e.g., `software-dev-leaders.md`). If provided, Claude vets titles against the full rulebook. If not provided, Claude vets against the ICP titles brief (input #3) using general judgment.

---

## Core Concept: Left Side vs Right Side

### The Data Layout

Lead list CSVs from enriched databases typically have two zones of data per contact:

**Left-side data** (from the lead database):
- Title
- Company
- Domain (website)
- Other database fields (location, industry, etc.)

**Right-side data** (enriched from LinkedIn):
- Recent Experience 1: Title, Company, Domain
- Recent Experience 2: Title, Company, Domain
- Recent Experience 3: Title, Company, Domain

### The Reconciliation Rule

**Left-side data can be wrong or stale.** Databases lag behind reality. A person may have changed jobs, been promoted, or the record may simply be incorrect.

**Right-side LinkedIn enrichment is ground truth.** It reflects what the person's LinkedIn profile actually says — their current and recent roles.

**If left and right agree** — easy confirmation. The database record matches LinkedIn. High confidence.

**If left and right disagree** — right side (LinkedIn) wins. That's their actual current role. The left-side data is stale or wrong.

### Determining the REAL Title and REAL Company — Vet All Operating Roles

LinkedIn experiences are ordered by start date, **not by importance.** A person's most recent entry (Exp 1) may be a volunteer role, career break, advisory board seat, or academic side gig — while their actual full-time operating role sits in Exp 2 or 3. **The script does not bet on a single title.** It collects ALL operating titles + the left-side title, sends them all for vetting, and qualifies the lead if ANY of them pass.

**Why vet-all instead of pick-one:** Picking a single "best" operating role means one wrong guess kills the lead. If Exp 1 is a career break and Exp 2 is CTO, the old logic would either (a) miss that career break is non-operating and fail the lead, or (b) require an ever-growing list of non-operating patterns to stay correct. Vet-all is failsafe — every operating title gets a chance, and the enrichment data you paid for (Exp 2, Exp 3) actually gets used.

#### Step A: Collect All Experiences

Gather every available data point into a list:

| Source | Title | Company | Domain |
|--------|-------|---------|--------|
| Exp 1 | from LinkedIn | from LinkedIn | from LinkedIn |
| Exp 2 | from LinkedIn | from LinkedIn | from LinkedIn |
| Exp 3 | from LinkedIn | from LinkedIn | from LinkedIn |
| Left-side | from database | from database | from database |

#### Step B: Tag Each Experience as "Operating" or "Non-Operating"

**Non-operating patterns** — these titles are excluded from vetting entirely (they can never qualify a lead):

| Pattern | Examples |
|---------|----------|
| Volunteer / Volunteering | "Volunteer CTO", "Volunteering as Tech Lead" |
| Board Member / Board of Directors (non-executive) | "Board Member", "Independent Board Director", "Non-Executive Director" |
| Advisor / Advisory | "Strategic Advisor", "Technical Advisor", "Advisory Board Member" |
| Mentor / Mentoring | "AI Mentor at Great Learning", "Startup Mentor" |
| Angel Investor / Investor (non-fund) | "Angel Investor", "Investor" |
| Adjunct / Guest / Visiting Professor or Lecturer | "Adjunct Professor at MIT", "Guest Lecturer" |
| Career Break / Sabbatical / Leave | "Career Break", "Sabbatical", "Parental Leave", "On Leave" |
| Seeking / Open to / Between Roles | "Seeking New Opportunities", "Open to Work", "Between Roles" |
| Student / Full-time Student (when other exp exists) | "MBA Candidate", "Full-time Student" |
| Retired / Retirement | "Retired CTO", "In Retirement" |

**Conditional non-operating** — deprioritized in selection (Step D) but still sent for vetting:

| Pattern | Examples |
|---------|----------|
| Fractional (when another full-time role exists) | "Fractional CTO" — still vetted, but a full-time PASS wins over it |
| Independent Consultant (when another full-time role exists) | Side consulting gig — still vetted, but a full-time PASS wins over it |

**Important nuances:**
- "Fractional CTO" with no other operating role → treat as operating (it's their primary gig)
- "Independent Consultant" with no other operating role → treat as operating
- "Board Member" is always non-operating regardless — board members don't run daily operations
- "Volunteer" is always non-operating regardless
- "Career Break" is always non-operating regardless — not an active role

#### Step C: Collect ALL Candidate Titles for Vetting

Instead of picking one winner, collect every operating title + the left-side title as **candidates**:

1. **All operating experiences** (Exp 1/2/3 tagged as operating) → candidate titles
2. **All conditional experiences** (fractional, consultant) → candidate titles
3. **Left-side title** → always a candidate (even if it duplicates a right-side title — deduplication happens at the unique-title level)
4. **Non-operating experiences** → excluded, never sent for vetting

Each candidate carries its source (Exp 1, Exp 2, Exp 3, Left-side), title, company, and domain.

#### Step D: After Vetting — Pick the Best Passing Title

Once Claude has vetted all unique titles, apply the results back to each row's candidates:

1. **Among PASS titles** — pick the most recent by source priority: Exp 1 > Exp 2 > Exp 3 > Left-side. Among right-side ties, prefer the one whose company matches the left-side (extra confirmation). Full-time operating roles take priority over conditional (fractional/consultant) roles.
2. **If no PASS but any REVIEW** — pick the most recent REVIEW title by the same priority
3. **If all candidates FAIL** → NONE
4. **If ALL experiences were non-operating** (rare — person between jobs, only board seats) → NONE with note "all experiences non-operating"

#### Example 1: Career Break in Exp 1, CTO in Exp 2

| Source | Title | Company | Tag | Vet |
|--------|-------|---------|-----|-----|
| Exp 1 | Career Break | N/A | Non-operating (break) | *not sent* |
| Exp 2 | Chief Technology Officer | GRI UK | Operating | **PASS** — P1 Engineering, CTO |
| Left-side | Chief Technology Officer | GRI UK | Operating | **PASS** — confirms |

**Result:** Exp 2 wins. REAL title = "Chief Technology Officer", REAL company = "GRI UK". Left-side confirms.

**Old logic picked Exp 1 (Career Break) → FAIL → lead lost. New logic vets Exp 2 and rescues the lead.**

#### Example 2: Board role in Exp 1, academic in Exp 2, real job in Exp 3

| Source | Title | Company | Tag | Vet |
|--------|-------|---------|-----|-----|
| Exp 1 | Independent Board Director | Traxión | Non-operating (board) | *not sent* |
| Exp 2 | Associate Professor | IE Business School | Non-operating (academic) | *not sent* |
| Exp 3 | Head of AI for Digital Natives | Microsoft | Operating | **PASS** — P3 AI |
| Left-side | Head of AI for Digital Natives in EMEA | Microsoft | Operating | **PASS** — confirms |

**Result:** Exp 3 wins (only operating PASS). Left-side confirms. REAL title = "Head of AI for Digital Natives", REAL company = "Microsoft".

#### Example 3: Multiple operating roles, only one fits ICP

| Source | Title | Company | Tag | Vet |
|--------|-------|---------|-----|-----|
| Exp 1 | VP of Sales | Acme Corp | Operating | **FAIL** — sales role |
| Exp 2 | CTO | Acme Corp | Operating | **PASS** — P1 Engineering |
| Left-side | CTO | Acme Corp | Operating | **PASS** — confirms |

**Result:** Exp 1 is operating but fails title vet. Exp 2 passes. REAL title = "CTO", REAL company = "Acme Corp". The lead is rescued even though the most recent operating role didn't fit the ICP.

---

## Title Qualification

### Two Layers of Rules — Both Always Apply

Title vetting has two layers that work together. Neither replaces the other:

**Layer 1 — Universal instant-disqualify (this skill, every run):**
Patterns that are always wrong regardless of client, ICP, or campaign. Defined below. These are the floor — they apply even when a client rulebook is provided.

**Layer 2 — Campaign rulebook (ICP-specific, per run):**
Persona definitions, seniority floors, keyword rules, exclusions, and edge cases specific to this campaign and list. Lives in the knowledge base (input #7). This is the authority on what qualifies — the rulebook defines the target, the universal layer only weeds out obvious non-starters.

**When both layers are present, both apply.** The rulebook does not override the universal patterns, and the universal patterns do not override the rulebook's persona judgments. Read both before vetting any title.

---

### Layer 1 — Universal Instant Disqualify (Permanent — Every Run)

If any of these patterns appear in the person's REAL title, the contact is a dud regardless of company match or client rulebook:

| Pattern | Reason |
|---------|--------|
| Executive Assistant, Administrative Assistant, Personal Assistant | Admin/support role |
| Assistant to, Secretary to, Aide to | Support role serving an executive |
| [Any role] Business Partner to [Executive] | Admin/support role — "Business Partner to VP of Engineering" = serves the VP, not a decision-maker |
| Chief of Staff | Support role, not decision-maker |
| Chief of Staff to [Executive] | The executive they serve does not save it — Chief of Staff is still the primary role |
| EA (when it means Executive Assistant, not Enterprise Architecture) | Admin/support role |
| Retired, Former, Ex- | No longer in role |
| Emeritus | Retired/honorary designation — equivalent to "Former [Title]" |
| Intern, Trainee, Apprentice | Too junior |
| Analyst (without senior/lead/principal prefix) | Too junior for most ICP briefs |
| Advisory Board Member, Board of Directors (non-executive), Governing Board | Not an operating role |

### Office of the [Executive] — Universal Rule

When a title contains "[C-Level] Office", "[C-Level] Team", or "Office of the [C-Level]", the person **works for** that executive — they are not the executive. Disqualify unless their own title outside the office/team label qualifies independently.

| Pattern | Example | Decision |
|---------|---------|----------|
| [C-Level] Office (as role context) | "CTO Office - SVP - Head Of Operations" | FAIL — works in the CTO's office; the "SVP - Head Of Operations" is their own role, not a CTO |
| [C-Level] Team (as role context) | "CTO Team - Software Technical Leader" | FAIL — member of the CTO's team, not the CTO |
| Technical Staff, [C-Level] Office | "Technical Staff, CTO Office" | FAIL — IC-level role within the CTO's org |
| Office of the [C-Level] (explicit) | "Director of Operations - Office of the Chief Information Officer" | FAIL — works in CIO's office; is not the CIO |
| Exception — own title qualifies independently | "Head of Engineering Operations \| Office of the CTO" | PASS — "Head of Engineering Operations" qualifies on its own merits regardless of office context |

**How to evaluate:** Strip the office/team context label. Ask: does the person's own role (what remains) qualify? If yes, PASS on their own merits. If no, FAIL.

### Title-in-Department-Name Pattern (Instant Disqualify)

Some titles contain an ICP keyword (e.g., "CIO") but only as a **department, practice, or market-segment descriptor** — the person works in/around that function, not as its leader. Disqualify these patterns:

| Pattern | Example | Reason |
|---------|---------|--------|
| Practice/portfolio/community + ICP keyword | "Managing VP, CIO & AI Practice" (Gartner) | Sells to CIOs, is not one |
| Marketing/Events/Content + ICP keyword | "Sr Manager, Conferences Marketing - CIO North America" | Marketing role for CIO-focused events |
| Team Manager/Director + ICP keyword segment | "Director Team Manager, CIO and AI Leaders" | Manages a team that serves CIOs |
| Leaders Group + ICP keyword | "Group VP, CIO and AI Leaders Group" | Manages a CIO-focused client group |
| Research/Analyst + ICP keyword | "Research Director, CIO and Industries" | Research about CIOs, not a CIO |

**How to detect:** If the person's company is a consulting, research, or analyst firm (Gartner, Forrester, McKinsey, etc.) AND the ICP keyword appears alongside words like "Practice", "Portfolio", "Communities", "Events", "Conferences", "Marketing", "Product Management", "Research" — the ICP keyword is a market segment label, not a role. Disqualify.

**Important:** This rule only fires when the surrounding context makes it clear the keyword is a segment descriptor. "CIO" in "SVP & CIO" at Gartner would still qualify (that's the actual CIO of Gartner). The tell is words like Practice, Portfolio, Communities, Events, Conferences, Team Manager, Product Management around the ICP keyword.

### Title Vetting — Claude Does This, Not Python

Title qualification is Claude's responsibility. Python does not evaluate titles. After the operating role is determined, the REAL title is passed to Claude for a judgment call.

#### Claude's Vetting Inputs (per run)

Claude receives:
1. The list of unique REAL titles (extracted by Python, deduplicated)
2. The client's title vetting rulebook (input #7) — the authority on ICP personas, seniority floors, keywords, and exclusions
3. If no rulebook: the plain English ICP title brief (input #3) — Claude vets against this using general judgment
4. The universal instant-disqualify patterns from this skill (Layer 1 above) — always applied, even when a rulebook is present
5. Any additional disqualify patterns for this run (input #6)

**When a rulebook is provided, read it fully before vetting any title.** The rulebook governs what qualifies. The universal patterns (Layer 1) govern what is always disqualified. Both apply simultaneously.

#### Claude's Output Format

For each unique title, Claude returns one row in this exact pipe-delimited format:

```
TITLE_VET_START
title | vet | persona | reason
Co-Founder / CTO | PASS | Engineering | CTO is a P1 C-level shortcut; co-founder framing doesn't disqualify
VP of AI GTM | FAIL | NONE | AI GTM is a go-to-market function — AI is the product domain being sold, not a leadership domain
Head of Data | REVIEW | NONE | Ambiguous — could be data engineering, analytics, or data science
TITLE_VET_END
```

Rules for Claude's output:
- **`vet`** is always `PASS`, `FAIL`, or `REVIEW` — nothing else
- **`persona`** is the matched persona label (e.g., `Engineering`, `Product`, `AI`) or `NONE`
- **`reason`** is one concise line — cite the specific rule that governed the decision
- Every unique title gets exactly one row — no skipping
- Titles are matched case-insensitively; output the title exactly as received

#### Python Parses Claude's Output

Python reads the block between `TITLE_VET_START` and `TITLE_VET_END`, builds a lookup table `{ title_normalized: (vet, persona, reason) }`, then applies it to every row in the CSV by matching on the REAL title.

#### REVIEW Handling

- `REVIEW` titles are written to the output with `[final] Title = REVIEW` and `[final] Domain = REVIEW`
- The WHY column records Claude's reason so the user can make a manual call
- REVIEW contacts are not treated as qualified or disqualified until the user resolves them

---

## Company Qualification

### Fuzzy Matching Against the Brief

If the user provides a reference list (e.g., Fortune 1000 CSV, target account list):

1. Extract the person's REAL company name
2. Fuzzy-match it against the reference list
3. Account for common variations:
   - Abbreviations: "Inc.", "Corp.", "Ltd.", "LLC", "Co."
   - Parent vs subsidiary names
   - "The" prefix (e.g., "The Boeing Company" vs "Boeing")
   - Punctuation and spacing differences
   - Common shortenings (e.g., "JPMorgan Chase & Co." vs "JPMorgan" vs "JP Morgan")

**Use Python's `thefuzz` (or `fuzzywuzzy`) library** with `token_sort_ratio` for comparison. A threshold of 80+ is a reasonable starting point — confirm with the user during test run.

If no reference list is provided, company qualification is based on the user's plain English brief (e.g., "must be a SaaS company") and should be evaluated as best as possible from available data.

### Domain Determination

The `[final] Domain` output should be:
- The correct website domain for the person's REAL company, if both title and company qualify
- Pulled from whichever data source (left or right) has the correct company match
- `NONE` if the contact is a dud (title or company doesn't qualify)

---

## Step-by-Step Process

### Step 1: Gather Configuration

Ask the user for:

```
1. Which CSV are we processing?
2. What's the context? (e.g., "Fortune 1000 CIOs")
3. What ICP titles are we looking for? (e.g., "CIO, Chief Information Officer")
4. What's the company brief? (e.g., "must be on the Fortune 1000 list")
5. Is there a reference list file for company matching? (path if yes)
6. Any additional title patterns to disqualify beyond the defaults?
```

### Step 2: Inspect the CSV

Before writing any code:

1. Read the CSV headers to identify:
   - Left-side columns: which column is Title? Company? Domain?
   - Right-side columns: which columns are Recent Experience 1/2/3 Title, Company, Domain?
2. Present the column mapping to the user for confirmation
3. Check for any unexpected column names or formats

### Step 3: Confirm Configuration

Present the full config back to the user:

```
CONTEXT: Fortune 1000 CIOs
ICP TITLES: CIO, Chief Information Officer
TITLE VETTING: Claude (rulebook: /path/to/rulebook.md) [or: Claude (ICP brief only)]
COMPANY BRIEF: Must be on the Fortune 1000 list
REFERENCE LIST: /path/to/fortune1000.csv
FUZZY MATCH THRESHOLD: 80

COLUMN MAPPING:
  Left Title: "Title"
  Left Company: "Company"
  Left Domain: "Website"
  Right Exp 1 Title: "Recent Experience 1 Title"
  Right Exp 1 Company: "Recent Experience 1 Company"
  Right Exp 1 Domain: "Recent Experience 1 Domain"
  ... (etc.)

INSTANT DISQUALIFY TITLES:
  [default list + any user additions]

TOTAL ROWS: N
UNIQUE TITLES: (determined after Script 1 runs)
```

Get confirmation before proceeding.

### Step 4: Two-Script Workflow

Title vetting requires two scripts and a Claude vetting step in the middle. Write both scripts in `temp-work-files/` (use `temp-work-files/xp-labs/` for client-specific work).

#### Script 1 — Extract All Candidate Titles (`[client]_extract_titles.py`)

This script collects all candidate titles per row — no title evaluation, no single-winner selection.

1. **Encoding:** Start with `sys.stdout.reconfigure(encoding='utf-8')`
2. **Read the CSV** with proper encoding handling (`utf-8-sig` fallback to `latin-1`)
3. **For each row:**
   a. Extract left-side data (Title, Company, Domain)
   b. Extract right-side data (Recent Experience 1/2/3 — Title, Company, Domain)
   c. Collect all experiences, tag each as "operating", "conditional", or "non-operating"
   d. Build a **candidates list**: all operating + conditional titles, plus the left-side title. Exclude non-operating.
   e. Store the full candidates list (with source, title, company, domain) alongside the row index for later use
4. **Collect all unique titles** across all candidates from all rows (deduplicated)
5. **Write unique titles** (one per line) to `temp-work-files/xp-labs/unique_real_titles.txt`
6. **Write per-row candidate data** to `temp-work-files/xp-labs/rows.json` (row index → candidates list)
7. **Print:** total rows processed, unique title count, average candidates per row

#### Claude Vetting Step (between scripts)

After Script 1 runs:
1. Claude reads `unique_real_titles.txt`
2. Claude vets each title against the ICP brief / rulebook (see Title Vetting section above)
3. Claude outputs the lookup table in the specified pipe-delimited format
4. The lookup table is saved to `temp-work-files/xp-labs/title_vet_lookup.txt`

#### Script 2 — Apply Results (`[client]_apply_dud_removal.py`)

1. **Encoding:** Start with `sys.stdout.reconfigure(encoding='utf-8')`
2. **Read the CSV**, **read `rows.json`** (per-row candidates), and **read `title_vet_lookup.txt`** — parse lookup into a dict `{ title_normalized: (vet, persona, reason) }`
3. **For each row:**
   a. Load the row's candidates list from `rows.json`
   b. Look up EVERY candidate title in the vet lookup (case-insensitive)
   c. **Selection priority among candidates:**
      - First: pick the most recent PASS (Exp 1 > Exp 2 > Exp 3 > Left-side); full-time operating beats conditional (fractional/consultant)
      - Second: if no PASS, pick the most recent REVIEW by the same priority
      - Third: if all candidates FAIL → NONE
   d. For the winning candidate: run company fuzzy-match against reference list (if applicable)
   e. Determine `[final] Domain` from whichever source (left or right) has the matching company
   f. Compose WHY string showing ALL candidates and their verdicts, plus the winner selection reason and company match result
   g. Set the three output columns
4. **Output columns:**
   - `[final] Domain` — correct domain if qualified; `REVIEW` if title is REVIEW; `NONE` if dud
   - `[final] Title` — winning title if PASS; `REVIEW` if REVIEW; `NONE` if dud
   - `WHY` — merged reasoning (see WHY Composition below)
5. **Use `thefuzz`** for company fuzzy matching (`pip install thefuzz`)
6. **Save the modified CSV** (overwrite in-place or save as a new file — confirm with user)

#### WHY Composition

The WHY column shows all candidates evaluated and the final selection:

```
[candidates: Exp 1: {title} at {company} → {vet}; Exp 2: {title} at {company} → {vet}; Left-side: {title} at {company} → {vet}] [winner: {source} — {title} at {company}] [title: {vet} — {Claude's reason}] [company: {match result}]
```

Non-operating experiences are noted as skipped (not sent for vetting). The winner line explains why that candidate was selected.

Examples:
```
[candidates: Exp 1: Career Break at N/A → skipped (non-operating); Exp 2: Chief Technology Officer at GRI UK → PASS; Left-side: Chief Technology Officer at GRI UK → PASS] [winner: Exp 2 — Chief Technology Officer at GRI UK (most recent PASS; left-side confirms)] [title: PASS — P1 Engineering, CTO C-level shortcut] [company: not checked — no reference list]

[candidates: Exp 1: VP of Sales at Acme Corp → FAIL; Exp 2: CTO at Acme Corp → PASS; Left-side: CTO at Acme Corp → PASS] [winner: Exp 2 — CTO at Acme Corp (Exp 1 failed title vet; left-side confirms)] [title: PASS — P1 Engineering, CTO C-level shortcut] [company: fuzzy match 91% to 'Acme Corporation' on account list]

[candidates: Exp 1: VP of AI GTM at SalesForce → FAIL; Left-side: VP of AI GTM at SalesForce → FAIL] [winner: none — all candidates failed] [title: FAIL — AI GTM is a go-to-market function, not an AI leadership role] [company: not checked — title disqualified]

[candidates: Exp 1: Head of Data at DataCo → REVIEW; Exp 2: Director of Analytics at DataCo → FAIL; Left-side: Head of Data at DataCo → REVIEW] [winner: Exp 1 — Head of Data at DataCo (most recent REVIEW; no PASS available)] [title: REVIEW — ambiguous, could be data engineering or data science] [company: fuzzy match 88% to 'DataCo Inc' on account list]
```

### Step 5: Test Run

- Sample N random rows (user specifies, default 25)
- Run Script 1 on the sample to extract unique REAL titles from the sample
- Claude vets those titles and outputs the lookup
- Run Script 2 on the sample to apply results
- Output results for the user to review — show the three new columns alongside Full Name, Job Title, Company Name
- Print a summary: `Sample: N rows | Qualified: X | Duds: Y | Review: Z`
- Ask the user to check Claude's title judgments and adjust if needed before the full run

### Step 6: Full Run

After user approves the test:
- Run Script 1 on all rows → generate full `unique_real_titles.txt`
- Claude vets all unique titles → save lookup to `title_vet_lookup.txt`
- Run Script 2 on all rows → write final output columns
- Print full summary: total rows, qualified, duds, REVIEW count, breakdown of dud reasons (wrong title / not on account list / both)

### Step 7: Idempotency Check

If `[final] Domain`, `[final] Title`, or `WHY` columns already exist in the CSV, overwrite them rather than duplicating.

---

## Output Columns

### [final] Domain

- The correct website domain for the person's REAL company — if both title and company qualify
- `NONE` if the contact is a dud

### [final] Title

- The person's REAL qualified title (from the best available data source) — if it matches an ICP title
- `NONE` if the contact is a dud

### WHY

Plain English reasoning. Should be concise but specific. Examples:

**Qualified:**
```
"LinkedIn (Exp 1) confirms CIO at Boeing (domain: boeing.com). Left-side data agrees."
"Left-side shows VP of IT at Walmart. LinkedIn Exp 1 shows CIO at Walmart — promoted. Title qualifies, company on Fortune 1000 list."
"LinkedIn Exp 1 title is Chief Information Officer at JPMorgan Chase. Fuzzy match 94% to 'JPMorgan Chase & Co.' on reference list."
```

**Dud — wrong title:**
```
"REAL title is 'Executive Assistant to CIO' (from LinkedIn Exp 1). Support role — instant disqualify."
"REAL title is 'IT Manager' (from LinkedIn Exp 1). Not in ICP titles (looking for CIO/Chief Information Officer)."
"REAL title is 'Former CIO' — no longer in role."
```

**Dud — wrong company:**
```
"REAL title is CIO (qualifies) but REAL company is 'Bob's Auto Shop' — not on Fortune 1000 list. Best fuzzy match: 'Bob Evans Restaurants' at 62% (below 80% threshold)."
"Title qualifies as CIO, but person moved to 'TechStartup Inc' (LinkedIn Exp 1) which is not on the reference list. Left-side company 'Microsoft' is stale."
```

**Dud — both wrong:**
```
"REAL title is 'Sales Manager' (not ICP) at 'Local Consulting LLC' (not on list). Database record completely stale."
```

---

## Important Notes

- **Claude vets titles — Python does not.** Title qualification requires judgment. Python extracts unique REAL titles and applies the lookup; Claude makes the actual PASS/FAIL/REVIEW calls.
- **Unique titles only.** Claude vets each unique title once. Python applies the result to all rows sharing that title. Never send 3,000+ rows to Claude — extract unique titles first.
- **Pipe-safe lookup parsing.** Titles can contain `|` characters (e.g., `"CIO | CISO"`). Never parse the lookup by positional field index. Instead, scan left-to-right for the first `PASS`/`FAIL`/`REVIEW` token — everything before it is the title, everything after is vet/persona/reason. Positional parsing silently corrupts entries and causes pipe-title lookups to return None → false REVIEW.
- **Rulebook vs. ICP brief.** If a title vetting rulebook is provided (input #7), load it before vetting. If not, Claude vets against the plain English ICP titles brief (input #3) using general judgment. The rulebook always takes precedence.
- **Vet all operating roles, not just one.** LinkedIn experiences are ordered by start date, not importance. Collect all operating titles + left-side, send them all for vetting, and qualify the lead if ANY pass. Pick the best passing title by recency. This is failsafe — no single wrong guess can kill a lead that has a qualifying title in Exp 2 or 3.
- **Right side wins over left side.** LinkedIn enrichment is the ground truth. Left-side database data is often stale. But left-side data serves as confirmation when it agrees with the chosen operating role.
- **Build the full picture first.** Don't evaluate any single experience in isolation — always cross-reference all available columns before making a decision.
- **Fuzzy matching is essential for companies.** Company names are messy — abbreviations, parent/subsidiary differences, punctuation. Use `thefuzz` with `token_sort_ratio`.
- **Never lose data.** Original columns are preserved. The three output columns are additions (or overwrites if they already exist).
- **Idempotent.** Safe to re-run — existing output columns get overwritten, not duplicated.
- **Windows encoding.** Always use `sys.stdout.reconfigure(encoding='utf-8')` at the top of every Python script.
- **Temp files go in `[project root]/temp-work-files/`.** Scripts and intermediate files (unique_real_titles.txt, title_vet_lookup.txt) go in `temp-work-files/xp-labs/`, never inside client folders.
- **Confirm column mapping.** CSV column names vary across databases — always inspect and confirm before processing.
- **Test before full run.** Sample rows first, get user approval, then process the full list.
- **The WHY column is critical.** Every decision must be explainable in plain English — merged from operating role selection, Claude's title reason, and company match result.
- **Threshold is adjustable.** The fuzzy match threshold (default 80) should be tuned during the test run based on user feedback.
