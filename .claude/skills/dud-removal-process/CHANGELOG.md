# Dud Removal Process — Changelog

## v3.2.0 — 2026-03-24

### Two-Layer Title Qualification Architecture

- **Restructured title qualification into two explicit layers** that always apply together:
  - **Layer 1 — Universal instant-disqualify (this skill):** Patterns that are always wrong regardless of client, ICP, or campaign. Acts as a floor.
  - **Layer 2 — Client rulebook:** Persona definitions, seniority floors, keyword rules, and ICP-specific exclusions. Acts as the authority on what qualifies.
- **Clarified the OR → AND relationship.** Previously "either the rulebook OR the ICP brief" implied Claude could skip the universal patterns when a rulebook was provided. Now: rulebook governs what qualifies; universal patterns govern what is always disqualified. Both apply simultaneously.
- **Expanded Layer 1 instant-disqualify** with patterns that are universally wrong but weren't previously listed:
  - `Emeritus` — retired/honorary designation, equivalent to "Former [Title]"
  - `[Any role] Business Partner to [Executive]` — admin/support serving an exec (e.g., "Administrative Business Partner to VP of Engineering")
  - `Chief of Staff to [Executive]` — explicit compound form, the executive listed doesn't save it
- **Added "Office of the [Executive]" as a standalone universal rule** with its own table. Previously implied but not explicitly codified. Covers:
  - `[C-Level] Office` (e.g., "CTO Office - SVP - Head Of Operations") — FAIL unless own title qualifies independently
  - `[C-Level] Team` (e.g., "CTO Team - Software Technical Leader") — FAIL
  - Exception: if the person's own role outside the office/team label qualifies independently, PASS on their own merits
- **Updated Claude's vetting inputs** to list the universal patterns as input #4, always present alongside the rulebook. Removed ambiguous "either/or" framing.

**Why this matters:** The vetting errors found in the Wispr AI & tech-forward run (CTO Office, CTO Team, Admin Business Partner, CTO Emeritus) were patterns the client rulebook already partially covered but the universal layer didn't enforce explicitly. With both layers clearly defined, Claude has no ambiguity about which authority applies to which type of decision.

---

## v3.1.0 — 2026-03-24

### Bug Fix: Pipe-in-Title Lookup Parsing

- **BUG FIX (critical):** The lookup parser in Script 2 assumed positional fields (`parts[0]` = title, `parts[1]` = vet). When Claude outputs a title containing `|` (e.g., `"CIO | CISO | PASS | Engineering | ..."`), the parser truncated the title at the first pipe and used the second segment as the vet value — which is never PASS/FAIL/REVIEW, causing the real title lookup to return None → REVIEW
- **Fix:** Parser now scans left-to-right for the first `PASS`/`FAIL`/`REVIEW` token; everything before it is reassembled as the title with ` | ` joins. Robust to any number of pipes in the title
- **Impact:** 48 contacts were stuck in REVIEW with "title not found in vet lookup" — all now resolved correctly
- Secondary impact: pipe-title entries were overwriting earlier entries at the same pre-pipe key with invalid vet values; fixed by same change

### Bug Fix: None Skip Reason in WHY Column

- **BUG FIX:** When multiple operating roles existed and one was chosen by recency, the skipped operating roles had `_skip_reason = None` (Python NoneType), producing WHY entries like `skipped: Left-side (VP of AI Engineering) — None`
- **Fix:** Null skip reason now replaced with `"operating role, not chosen (lower priority than selected experience)"`
- Applied to both Script 1 (extract) and Script 2 (apply)

### Title Lookup Corrections (9 entries)

QA pass identified 9 entries requiring correction. All changes made to `title_vet_lookup.txt` before re-run:

| Title | Before | After | Reason |
|---|---|---|---|
| `Administrative Business Partner to VP of Engineering and VP of Infrastructure` | PASS | FAIL | "Business Partner to" follows the "assistant to" instant-disqualify pattern |
| `CTO Office - SVP - Head Of Operations` | PASS | FAIL | "CTO Office" = department context — works in the CTO's office, not the CTO |
| `Technical Staff, CTO Office` | PASS | FAIL | Same "Office of the CTO" = department context rule |
| `CTO Team - Software Technical Leader` | PASS | FAIL | "CTO Team" = member of the CTO's team, not the CTO |
| `CTO Emeritus` | PASS | FAIL | Emeritus = retired/honorary — equivalent to "Former CTO" |
| `CIO Representative` | PASS | FAIL | Liaison/ambassador role — representing the CIO ≠ being the CIO |
| `Global Head HR – Product & Technology \| India HR Head \| Head of Global Talent Acquisition` | PASS | FAIL | HR/talent acquisition role; "Technology" in org context only |
| `Acting Chief Information Security Officer` | FAIL (wrong reason) | FAIL (corrected reason) | Reason updated: CISO = security function, excluded per P1 rulebook (not "no seniority detected") |
| `Chief Business Technology Officer` | FAIL (wrong reason) | REVIEW | "Chief" is a valid seniority; plausible CTO-equivalent — moved to REVIEW for manual resolution |

### Results (AI & Tech Forward Companies — 3,390 rows)

- Before: 2,866 qualified · 444 duds · 80 REVIEW
- After: **2,895 qualified · 458 duds · 37 REVIEW**
- 43 REVIEWs resolved (48 pipe-title fixes → net 43 after accounting for title corrections)
- 29 contacts rescued from REVIEW → qualified
- 14 contacts moved from REVIEW → dud (PASS title but not on account list, or FAIL title after correction)

---

## v3.0.0 — 2026-03-24

### Claude-Based Title Vetting (replaces Python regex title matching)

- BREAKING: Title qualification is no longer done by Python pattern matching
- New architecture: two-script workflow with a Claude vetting step in between
  - **Script 1** (`[client]_extract_titles.py`) — operating role selection only; writes unique REAL titles to `unique_real_titles.txt`
  - **Claude vetting step** — reads unique titles, vets each against ICP brief or client rulebook, outputs pipe-delimited lookup to `title_vet_lookup.txt`
  - **Script 2** (`[client]_apply_dud_removal.py`) — reads lookup, re-runs operating role selection, applies title vet result, fuzzy-matches company, composes WHY, writes output columns
- Claude outputs `PASS`, `FAIL`, or `REVIEW` per title — never guesses
- `REVIEW` titles get `[final] Title = REVIEW`, `[final] Domain = REVIEW`, and a WHY explaining the ambiguity for human resolution
- New optional input #7: **title vetting rulebook** — path to client-specific rulebook (e.g., Wispr's `software-dev-leaders.md`). If provided, Claude uses the full rulebook. If not, Claude uses the plain English ICP brief.
- WHY column now merges three sources: operating role note (Python) + title reason (Claude) + company match result (Python)
- Unique-titles pattern: Claude vets each unique title once, Python applies to all rows — avoids sending thousands of rows to Claude
- Motivation: regex-based title matching misses compound titles, abbreviated titles, and nuanced disqualification patterns (e.g., AI GTM vs AI leadership) that require contextual judgment

---

## v2.1.0 — 2026-03-19

### Broadened "Head of" Title Matching
- BUG FIX: Previous regex `\bhead of (keyword)\b` required the ICP keyword to immediately follow "Head of", missing titles where a subdomain qualifier sits between them (e.g. "Head of Finance Digital Transformation", "Head of GTM & Commercial Digital Transformation", "Global IT Head - Process Development, Digital Transformation")
- Fix: split into two patterns — a loose `.{0,70}` pattern for long-form keywords (digital transformation, artificial intelligence, machine learning) and a strict pattern for short keywords (ai, data, digital, analytics)
- VP/Director distance limit increased from `.{0,40}` to `.{0,45}` to catch compound titles like "SVP, Treasury Management, Client Experience & Digital Transformation"
- NOTE: Operating role scan logic was NOT the issue — it already correctly scans all experiences; Exp 1 appeared in WHY messages simply because Exp 1 genuinely was the best operating role in those cases

### Expanded Company Name Alias Map
- BUG FIX: Many Fortune 1000 companies were failing fuzzy match because LinkedIn/database records use informal or abbreviated names
- Added aliases for two rounds of discovered mismatches: JPMorganChase, Citi (incl. 花旗), BNY, Synchrony, Broadridge, AMD, Dell EMC, onsemi, IFF, lululemon, elanco, BD, Verizon, Meta, Wabtec Corporation, Ally, U.S. Bank, ADM, Abbott, Emerson, ICE, Hershey (The Hershey Company), Ardent Health, Regeneron, Cognizant, Graybar, Kelly, Paramount, GuideWell, Raymond James, Capital One, Old National Bank
- WHY column includes `[alias resolved: 'X' → 'Y']` note when an alias was applied
- Key discovery: Cognizant, Graybar Electric, Ardent Health Partners, Kelly Services are on the Fortune 1000 — contacts at these firms with qualifying titles now correctly qualify

### Tested On
- AI-and-DT-Default-view-export-1773922238879.csv (347 rows)
- Three iterative patch runs on progressively resolved dud sets
- 92 contacts total rescued across all patches (139 duds → 47 duds)
- Final: 300 qualified, 47 duds

---

## v2.0.0 — 2026-03-17

### Best Operating Role Selection (replaces "Exp 1 wins" logic)
- BREAKING: No longer blindly trusts LinkedIn Exp 1 as the REAL role
- New logic scans ALL experiences (Exp 1, 2, 3, left-side) and tags each as "operating" or "non-operating"
- Non-operating patterns deprioritized: Volunteer, Board Member, Advisor, Mentor, Angel Investor, Adjunct/Guest/Visiting Professor, Fractional (when another role exists), Independent Consultant (when another role exists)
- Among operating roles, most recent (lowest exp number) wins
- Left-side data used as cross-validation/confirmation, not as fallback
- Fractional/Consultant treated as operating if no other operating role exists (it's their primary gig)
- WHY column now explains which experience was chosen and why others were skipped
- Prevents false duds where a person's real operating role (e.g., CTO at BigCorp in Exp 3) was hidden behind a volunteer/board role in Exp 1

---

## v1.1.0 — 2026-03-17

### Expanded-Scope Title Variants
- Added recognition of CDIO, CIDO, CITO, and other expanded-scope CIO variants as qualifying titles
- "Chief Digital and Information Officer", "Chief Information and Technology Officer", etc. now qualify as same buyer persona as CIO
- Explicitly excludes false friends: Chief Information Risk Officer, Chief Information Assurance Officer, Chief Investment Officer

### Title-in-Department-Name Detection
- Added new instant-disqualify pattern for ICP keywords used as market-segment labels
- Catches Gartner-style practice employees: "Managing VP, CIO & AI Practice" is someone who sells to CIOs, not a CIO
- Detects segment words: Practice, Portfolio, Communities, Events, Conferences, Marketing, Product Management, Research, Leaders Group, Team Manager
- Only fires at consulting/research/analyst firms (Gartner, Forrester, McKinsey, IDC, Deloitte)
- Preserves actual CIO roles at those firms (e.g., Gartner's own EVP & CIO still qualifies)

### Tested On
- CIO-Default-view-export-1773741581002.csv (1,288 rows)
- 24 CDIO/CITO contacts upgraded from dud → qualified
- 13 Gartner practice employees downgraded from qualified → dud
- Final: 1,197 qualified, 91 duds

---

## v1.0.0 — 2026-03-17

### Initial Release

- Created the dud-removal-process skill for system-wide contact qualification
- Core concept: left-side (database) vs right-side (LinkedIn enrichment) data reconciliation
- Right-side LinkedIn data is ground truth when left and right disagree
- Title qualification with instant-disqualify patterns (EA, assistant, chief of staff, retired, former, intern, advisory/governing body, secretary, analyst)
- Company qualification via fuzzy matching (`thefuzz` / `token_sort_ratio`) against a reference list or plain English brief
- Three output columns added in-place: `[final] Domain`, `[final] Title`, `WHY`
- Step-by-step process: gather config, inspect CSV, confirm, write Python script, test run, full run
- Windows encoding handling (`sys.stdout.reconfigure(encoding='utf-8')`)
- Idempotent — re-running overwrites existing output columns instead of duplicating
- Test-before-full-run workflow with user approval gate
