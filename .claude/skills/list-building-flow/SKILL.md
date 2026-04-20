---
name: list-building-flow
description: End-to-end list-building pipeline from sourcing contacts to delivery-ready export. Covers pull, email enrichment/validation, name normalization, LinkedIn enrichment, dud removal, and final formatting.
model: inherit
---

# List-Building Flow

## Purpose

The standard end-to-end pipeline for building a lead list from initial sourcing through delivery-ready export. Every list build follows these six steps in order. No step is skipped.

---

## Pipeline Overview

```
Step 1: Pull Contacts
    │
    ▼
Step 2: Email Enrichment + Validation
    │
    ▼
Step 3: First Name & Company Name Normalization
    │
    ▼
Step 4: LinkedIn Enrichment
    │
    ▼
Step 5: Dud Removal + Activity Flagging
    │
    ▼
Step 6: List Export Formatting
    │
    ▼
Step 7: Coverage Check
    │
    ▼
(Round 2 if gaps found)
```

---

## Step 1: Pull Contacts

### What Happens

Source the raw contact list. There are two entry points — choose based on the brief:

**Option A — Pull from database:**
Query a lead database (Apollo, ZoomInfo, etc.) directly using the ICP criteria from the brief (titles, industries, company size, location, etc.).

**Option B — Start with a target account list, then pull people:**
The brief provides a specific list of companies. Pull contacts from those companies using the target titles/personas from the brief.

### Output

A raw CSV/XLSX with contacts — names, titles, companies, domains, and whatever email/contact data the database provides.

---

## Step 2: Email Enrichment + Validation

### What Happens

Turn raw contact data into deliverable, validated email addresses.

**2a. Enrich missing emails:**
- Contacts that already have emails from the database — skip enrichment (keep the database email as-is)
- Contacts with blank/missing emails — enrich using an email finder (e.g., Apollo, Hunter, Dropcontact, etc.)

**2b. Merge into `[final] Emails`:**
- Create a single column called `[final] Emails`
- Merge all emails into this column — both the ones from the database (Step 1) and the ones found in enrichment (Step 2a)
- Every contact should now have an email in `[final] Emails` (if one was found)

**2c. Validate the `[final] Emails` column:**
- Run the entire `[final] Emails` column through an email validation provider (e.g., ZeroBounce, NeverBounce, Millionverifier, etc.)
- Based on validation results, create two new columns:
  - **`valid_emails`** — copy the email from `[final] Emails` into this column if the validation result is "valid"
  - **`catch_all_valid_emails`** — copy the email from `[final] Emails` into this column if the validation result is "catch-all" (accept-all server)
  - If the email is invalid/unknown/undeliverable, leave both columns blank for that row

**2d. Collect SMTP provider:**
- Create a new column: **`SMTP Provider`**
- Record the SMTP provider / mail server for each email (e.g., Google Workspace, Microsoft 365, Outlook, Proofpoint, Mimecast, Barracuda, etc.)
- This is typically returned by the validation provider alongside the validation result

### Output Columns After Step 2

| Column | Description |
|--------|-------------|
| `[final] Emails` | The merged email — one per contact (from database or enrichment) |
| `valid_emails` | Same email, only if validation = valid |
| `catch_all_valid_emails` | Same email, only if validation = catch-all |
| `SMTP Provider` | The mail server handling that email domain |

---

## Step 3: First Name & Company Name Normalization

### What Happens

Clean up formatting inconsistencies in first names and company names so the list looks professional and mail merge works correctly.

**First name normalization:**
- Proper case: `JOHN` → `John`, `jane` → `Jane`
- Handle edge cases: `MARY-JANE` → `Mary-Jane`, `O'BRIEN` → `O'Brien`, `McDONALD` → `McDonald`
- Strip leading/trailing whitespace
- Remove titles/prefixes that snuck into the name field (e.g., `Mr. John` → `John`, `Dr. Jane` → `Jane`)

**Company name normalization:**
- Consistent casing and formatting
- Standardize suffixes: `Inc`, `Inc.`, `Incorporated` → pick one consistent format
- Strip extra whitespace, fix encoding artifacts
- Create a `Normalized Company Name` column if the brief requires grouping or deduplication by company

---

## Step 4: LinkedIn Enrichment

### What Happens

Enrich each contact with their LinkedIn profile data. Output the **3 most recent active experiences** from their LinkedIn profile.

**What to capture per experience:**
- Title
- Company
- Company domain (if available)

**Output columns:**
- `Recent Experience 1 Title`, `Recent Experience 1 Company`, `Recent Experience 1 Domain`
- `Recent Experience 2 Title`, `Recent Experience 2 Company`, `Recent Experience 2 Domain`
- `Recent Experience 3 Title`, `Recent Experience 3 Company`, `Recent Experience 3 Domain`

**Why this matters:**
This data powers Step 5 (dud removal). The dud removal process cross-references the database record (left-side) against LinkedIn enrichment (right-side) to determine each contact's REAL title and REAL company. Without this enrichment, dud removal cannot function.

---

## Step 5: Dud Removal + Activity Flagging

### What Happens

Two things happen in this step:

**5a. Dud removal:**
Run the full dud removal process as defined in the **dud-removal-process** skill (`/.claude/skills/dud-removal-process/SKILL.md`).

This process:
1. Cross-references left-side (database) data with right-side (LinkedIn) data
2. Determines each contact's REAL title and REAL company
3. Vets titles through Claude (not Python) — using the client's title vetting rulebook if one exists, or the ICP brief if not
4. Fuzzy-matches companies against the target account list (if applicable)
5. Produces three output columns: `[final] Domain`, `[final] Title`, and `WHY`

Contacts that fail title vetting or company matching are marked as duds (`NONE`). Ambiguous cases are marked `REVIEW`.

**5b. Activity flagging:**
After dud removal, flag contacts with low LinkedIn activity:
- Create a new column: **`activity`**
- For contacts that passed dud removal (not duds): if their LinkedIn profile shows **under 150 connections**, mark them as `inactive` in the `activity` column
- Contacts with 150+ connections (or where connection count is unavailable): leave the `activity` column blank
- Duds are not flagged for activity — they're already removed

**Why flag inactives?**
Contacts with very few LinkedIn connections are often inactive profiles — the person may have moved on, rarely uses LinkedIn, or the profile is a shell. They're not duds (the title and company may be correct), but they're lower-quality targets for outbound that relies on LinkedIn signals.

---

## Step 6: List Export Formatting

### What Happens

Format the final list for delivery using the **list-export-formatter** skill (`/.claude/skills/list-export-formatter/SKILL.md`).

This process:
1. Maps all columns to the standard schema (15 standard columns)
2. Renames, reorders, and strips non-standard columns
3. Audits LinkedIn URLs for duds (Sales Navigator URLs, company pages, malformed URLs)
4. Creates a **Main** tab with all contacts
5. Creates **persona-grouped tabs** — one tab per persona group (grouping defined per run)
6. Outputs a delivery-ready `.xlsx` file

---

## Step 7: Coverage Check

### What Happens

Analyze the final list to identify **gaps** — which companies are missing which personas. Small TAMs mean every account matters, so this step ensures we know exactly where coverage is incomplete and can run targeted Round 2 pulls to fill gaps.

**7a. Build the coverage matrix:**
- Extract all unique domains (companies) from the list
- Cross-reference against the original target account list from the brief
- For each domain, check which personas have at least one qualified contact

**7b. Identify gaps:**
- For each domain, flag which personas are **missing** (no qualified contact found)
- Flag domains with **zero contacts** across all personas (complete misses)
- Flag domains that only have 1 persona covered (low coverage)

**7c. Output the gap report:**
Create a new tab (in the formatted `.xlsx`) or a separate CSV with the gap analysis:

| Column | Description |
|--------|-------------|
| `Domain` | The company domain |
| `Company Name` | The company name |
| `Personas Found` | Comma-separated list of personas with at least one contact |
| `Personas Missing` | Comma-separated list of personas with zero contacts |
| `Total Contacts` | Count of qualified contacts at this company |
| `Coverage %` | Personas found / total personas targeted (e.g., 3/4 = 75%) |

**Sort by:** Coverage % ascending (worst coverage first), so the most urgent gaps are at the top.

**7d. Summary stats:**
Report overall coverage metrics:

```
Coverage Summary:
  Total target accounts: [X]
  Accounts with full coverage (all personas): [X] ([%])
  Accounts with partial coverage: [X] ([%])
  Accounts with zero coverage: [X] ([%])

  Per-persona coverage:
    Servicing: [X]/[total] accounts ([%])
    Contact Center / CX: [X]/[total] accounts ([%])
    COO / Operations: [X]/[total] accounts ([%])
    CFO / Finance: [X]/[total] accounts ([%])

  Gap list exported to: [file path]
```

**Why this matters:**
The gap report becomes the input for Round 2 list building. Instead of re-pulling the entire list, you target only the missing persona × company combinations — more efficient and ensures maximum TAM coverage.

---

## Summary: Inputs and Outputs

| Step | Input | Output |
|------|-------|--------|
| 1. Pull | Brief (ICP + accounts) | Raw contact CSV/XLSX |
| 2. Email | Raw contacts | `[final] Emails`, `valid_emails`, `catch_all_valid_emails`, `SMTP Provider` |
| 3. Normalize | Names + companies | Clean `First Name`, `Normalized Company Name` |
| 4. LinkedIn | Contact list | 3 most recent experiences (title, company, domain) |
| 5. Duds | Enriched list + rulebook | `[final] Domain`, `[final] Title`, `WHY`, `activity` |
| 6. Format | Vetted list | Delivery-ready `.xlsx` with persona tabs |
| 7. Coverage | Formatted list + brief | Gap report (missing personas per company) for Round 2 |
