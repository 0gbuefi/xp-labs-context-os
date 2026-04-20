---
name: list-export-formatter
description: Reformat finalized lead lists into delivery-ready xlsx with standardized columns, persona-grouped tabs. Renames, reorders, and strips columns to a fixed standard schema. Works across all clients — persona context is discovered at runtime, not hardcoded.
model: inherit
---

# List Export Formatter

## Purpose

Takes a finalized lead list (xlsx or csv) and restructures it into a delivery-ready xlsx with:
- **Standardized columns** — renamed, reordered, and stripped to a fixed schema (non-standard columns are deleted)
- A **Main** tab containing all contacts
- **Persona-grouped tabs** — one tab per persona group (grouping defined by user each run)

This skill is client-agnostic. It discovers column mappings and personas from the data, confirms with the user, then generates the formatted output.

---

## When to Use

- After list building and title vetting are complete
- When the user says "format this list for delivery", "export this list", "create the persona tabs", or "split this into tabs"
- Before handing a list off to a client or posting in Slack

---

## What This Skill Does NOT Do

- Does not vet or classify job titles (use `job-title-vetting` skill)
- Does not scrape, enrich, or source contacts
- Does not deduplicate or QA (should be done before this skill runs)

---

## Standard Column Schema

Every formatted list outputs **only** these columns, in this exact order. Non-standard columns are deleted.

| # | Standard Column Name | Required? | Notes |
|---|----------------------|-----------|-------|
| 1 | `First Name` | Yes | |
| 2 | `Last Name` | Yes | |
| 3 | `Full Name` | Yes | |
| 4 | `Job Title` | Yes | |
| 5 | `Person LinkedIn URL` | Yes | |
| 6 | `Company Name` | Yes | |
| 7 | `Normalized Company Name` | If available | Omit column entirely if not in source |
| 8 | `Company Website` | Yes | |
| 9 | `Company LinkedIn URL` | Yes | |
| 10 | `Company Location` | If available | Omit column entirely if not in source |
| 11 | `Person Location` | If available | Omit column entirely if not in source |
| 12 | `[final] Emails` | Yes | The main/total email column |
| 13 | `valid_emails` | Yes | |
| 14 | `catch_all_valid_emails` | Yes | |
| 15 | `SMTP Provider` | Yes | |

**"If available" columns:** If the source data has no column that maps to `Normalized Company Name`, `Company Location`, or `Person Location`, that column is omitted entirely from the output (no empty column created). All other standard columns are required — if a required column can't be found, ask the user to identify it.

---

## Column Name Variants (Source → Standard)

The skill must recognize these common source column names and map them to the standard names:

| Standard Name | Possible Source Names |
|---|---|
| `First Name` | `first_name`, `firstName`, `First`, `contact_first_name`, `First Name` |
| `Last Name` | `last_name`, `lastName`, `Last`, `contact_last_name`, `Last Name` |
| `Full Name` | `full_name`, `fullName`, `name`, `contact_name`, `Full Name` |
| `Job Title` | `title`, `job_title`, `jobTitle`, `Title`, `position`, `Job Title` |
| `Person LinkedIn URL` | `linkedin_url`, `LinkedIn URL`, `linkedin_profile_url`, `LinkedIn Profile URL`, `profile_url`, `linkedin` (exclude company LinkedIn columns) |
| `Company Name` | `company`, `company_name`, `companyName`, `organization`, `Company Name` |
| `Normalized Company Name` | `normalized_company_name`, `clean_company_name`, `Normalized Company Name` |
| `Company Website` | `website`, `company_website`, `domain`, `company_domain`, `Company Website` |
| `Company LinkedIn URL` | `company_linkedin_url`, `company_linkedin`, `Company LinkedIn URL` |
| `Company Location` | `company_location`, `hq_location`, `company_city`, `company_country`, `Company Location` |
| `Person Location` | `person_location`, `location`, `city`, `state`, `country`, `Person Location` |
| `[final] Emails` | `work email`, `Work Email`, `[final] email`, `email` (the main/total email column) |
| `valid_emails` | `valid emails`, `Valid Emails`, `valid_email` |
| `catch_all_valid_emails` | `catch all valid emails`, `catch_all_emails`, `catchall_valid_emails`, `catch_all_valid_emails` |
| `SMTP Provider` | `smtp_provider`, `SMTP`, `email_provider`, `SMTP Provider` |

**Disambiguation rules:**
- `linkedin` or `LinkedIn URL` without `company` in the name → `Person LinkedIn URL`
- `company_linkedin`, `Company LinkedIn URL` → `Company LinkedIn URL`
- `email` (standalone) → `[final] Emails` (the main email column), NOT `valid_emails`
- `location` (standalone, without `company` prefix) → `Person Location`

---

## Inputs

### Required

1. **Input file path** — xlsx or csv containing the finalized lead list

### Discovered From Data (confirmed with user)

2. **Column mapping** — which source columns map to which standard columns
3. **LinkedIn URL column** — audited for dud URLs before proceeding
4. **Persona column** — which column contains persona classifications (used for tab grouping, then deleted from output)
5. **Persona grouping** — how to group unique persona values into tabs

---

## Step-by-Step Process

### Step 1: Read the Input File

Read the xlsx or csv. If xlsx, identify which sheet contains the main lead list (usually the first sheet, or a sheet named "Main List", "Main", or "Sheet1"). Report to the user:

```
Found: [filename]
Sheet: [sheet name] (if xlsx)
Rows: [count] (excluding header)
Columns: [count]
```

### Step 2: Column Mapping

Scan all source column headers and auto-map them to standard column names using the variant table above. Present the mapping to the user for confirmation:

```
Column mapping (source → standard):

  ✅ Mapped:
    "first_name" → First Name
    "last_name" → Last Name
    "full_name" → Full Name
    "title" → Job Title
    "linkedin_profile_url" → Person LinkedIn URL
    "company_name" → Company Name
    "company_website" → Company Website
    "company_linkedin_url" → Company LinkedIn URL
    "company_location" → Company Location
    "person_location" → Person Location
    "work email" → [final] Emails
    "valid emails" → valid_emails
    "catch_all_emails" → catch_all_valid_emails
    "smtp_provider" → SMTP Provider

  ⚠️ Not found (optional — will be omitted):
    Normalized Company Name

  ❌ Not found (required — please identify):
    (none)

  🗑️ Will be deleted (not in standard schema):
    "persona_type" (used for tab grouping only)
    "email_verification_status"
    "other_work_emails"
    "company_revenue"
    "employee_count"
    ... [list all non-standard columns]

Does this mapping look right? (Or tell me which columns to reclassify)
```

**If a required column can't be auto-mapped:** List all unmapped source columns and ask the user to identify it.

**If a source column could map to multiple standard columns:** Ask the user to disambiguate.

**Wait for user confirmation before proceeding.**

### Step 3: LinkedIn URL Audit

Before proceeding, scan the Person LinkedIn URL column for dud URLs that will cause problems in outreach tools (Smartlead, Instantly, etc.) or make the list look unvetted.

**Scan every row and flag duds.** A dud is any value that is NOT a clean `https://www.linkedin.com/in/...` profile URL. Categories:

| Category | Pattern | Example |
|----------|---------|---------|
| Sales Navigator URL | Contains `/sales/` or `/lead/` | `https://www.linkedin.com/sales/people/ACwAAA...` |
| Company page URL | Contains `/company/` | `https://www.linkedin.com/company/acme-corp` |
| Malformed URL | Missing `/in/`, has fragments, double slashes | `https://www.linkedin.com/pub/john-doe` |
| Non-LinkedIn URL | Doesn't contain `linkedin.com` | `https://twitter.com/johndoe` |
| Non-URL string | No `http` prefix | `john doe`, `N/A`, `#REF!` |
| Blank | Empty or null | |

**Report to user:**

```
LinkedIn URL audit:
  Clean profiles (/in/): [X] rows
  Sales Navigator URLs: [X] rows
  Company page URLs: [X] rows
  Malformed URLs: [X] rows
  Non-LinkedIn URLs: [X] rows
  Non-URL strings: [X] rows
  Blank: [X] rows
```

**If all clean:** Report and proceed to Step 4.

**If duds found — STOP and send user to Clay:**

```
Found [X] dud LinkedIn URLs that need fixing before export.

  Sales Navigator URLs: [X] — these contain /sales/people/ instead of /in/
  [other categories if applicable]

Take this list back to Clay and clean these up:
  1. Filter the LinkedIn URL column for URLs containing "/sales/" or other dud patterns
  2. Use Clay's LinkedIn enrichment to resolve them to proper /in/ profile URLs
  3. Re-export the cleaned file from Clay
  4. Run this skill again on the cleaned file

Showing duds so you know what to look for:
  [table of dud rows: row number, name, company, current URL, category]

Ready to proceed after you've cleaned the file? (y/n)
```

**Wait for user confirmation.** The user will either:
- Go fix the duds in Clay and come back with a cleaned file (restart the skill on the new file)
- Say "proceed anyway" if they've decided the duds are acceptable for this delivery

**Do NOT offer to fix duds programmatically.** Clay has the enrichment tools to resolve Sales Nav URLs to proper profile URLs. This skill only detects and reports — Clay does the fixing.

**Sales Navigator URLs specifically:** These are the most common dud. They look like real LinkedIn URLs but contain `/sales/people/ACwAAA...` instead of `/in/username`. They break when pasted into a browser without Sales Nav access and look unprofessional in a delivered list. Always flag these.

### Step 4: Find the Persona Column

Scan all source column headers for persona-related names. Look for (case-insensitive):
- `persona type`
- `persona_type`
- `persona_answer`
- `persona`

**If exactly one match:** Use it. Show the user.
**If zero matches:** List all column headers and ask: "Which column contains the persona classification?"
**If multiple matches:** Show the candidates and ask the user to pick one.

**Note:** The persona column is used for tab grouping only. It is NOT included in the output columns (it's not in the standard schema).

### Step 5: Discover Persona Values and Get Grouping Instructions

Extract all unique non-empty values from the persona column. Present them with counts:

```
Persona values found in [column name]:
  1. Tech / Product — 103 rows
  2. Lending Ops — 83 rows
  3. CEO / President — 60 rows
  4. Consumer Direct / Sales — 27 rows
  5. CX / Call Center — 23 rows
  6. Servicing — 5 rows
  [blank/UNFIT] — 357 rows (will stay in Main only)

How do you want these grouped into tabs?

Options:
  a) One tab per persona (6 tabs)
  b) Custom grouping — tell me which personas to combine into each tab
  c) Suggest a grouping based on the brief (if a brief file is provided)
```

**If user picks (b):** Collect the grouping. Example:
```
Tab "Servicing": Servicing
Tab "Lending": Lending Ops
Tab "CX, Tech & Others": CX / Call Center, Tech / Product, Consumer Direct / Sales, CEO / President
```

**If user picks (c):** Read the brief file to understand the persona strategy and suggest logical groupings. Present for confirmation before proceeding.

**UNFIT and blank persona rows:** These stay in the Main tab only. They are never copied to persona tabs. Confirm this with the user.

### Step 6: Confirm Full Configuration

Present the complete configuration before generating:

```
INPUT: [file path]
SHEET: [sheet name]
TOTAL ROWS: [count]

COLUMN MAPPING (source → standard):
  "first_name" → First Name
  "last_name" → Last Name
  "full_name" → Full Name
  "title" → Job Title
  "linkedin_profile_url" → Person LinkedIn URL
  "company_name" → Company Name
  "company_website" → Company Website
  "company_linkedin_url" → Company LinkedIn URL
  "company_location" → Company Location
  "person_location" → Person Location
  "work email" → [final] Emails
  "valid emails" → valid_emails
  "catch_all_emails" → catch_all_valid_emails
  "smtp_provider" → SMTP Provider

COLUMNS DELETED: [X] non-standard columns removed

PERSONA COLUMN: [column name] (used for tabs, not in output)
PERSONA TAB GROUPING:
  Tab "Servicing" — Servicing (5 rows)
  Tab "Lending" — Lending Ops (83 rows)
  Tab "CX, Tech & Others" — CX / Call Center, Tech / Product, Consumer Direct / Sales, CEO / President (113 rows)
  [Main only] — UNFIT / blank (357 rows)

OUTPUT: [input filename]_formatted.xlsx (same directory as input)

Proceed? (y/n)
```

### Step 7: Generate the Output XLSX

Use Python with `openpyxl` to build the output file.

#### Column Transformation

1. **Rename** all mapped source columns to their standard names
2. **Reorder** columns to match the standard schema order (see Standard Column Schema table)
3. **Delete** all columns not in the standard schema (including the persona column)
4. **Omit** optional columns (`Normalized Company Name`, `Company Location`, `Person Location`) if not present in source

#### Tab Generation

**"Main" tab:**
- ALL rows from the input (including UNFIT/blank persona)
- Standard columns only, in standard order
- Header row frozen (row 1)
- Auto-filter enabled on all columns

**Persona tabs (one per group):**
- Filtered subset of Main — only rows where persona value is in that tab's group
- Same standard columns as Main
- Header row frozen
- Auto-filter enabled
- Tab name = the group label (e.g., "Servicing", "Lending", "CX, Tech & Others")
- Tab names truncated to 31 characters if needed (xlsx sheet name limit)

**CRITICAL — Auto-filter range must cover all data rows:**
```python
last_row = len(data) + 1  # +1 for header
ws.auto_filter.ref = f'A1:{get_column_letter(len(cols))}{last_row}'
```
Do NOT set auto_filter.ref to just the header row (`A1:XX1`). That causes Excel filter dropdowns to show no values. The ref must span from row 1 to the last data row.

#### Formatting

- Header row: bold, light gray background (#D9D9D9)
- Column widths: auto-fit based on header length (minimum 12 characters, maximum 40)
- No colored rows or conditional formatting beyond headers (keep it clean)

### Step 8: Report Output

After generating:

```
Output: [output file path]

Standard columns: [X] columns (of 15 possible)
Columns deleted: [X] non-standard columns removed

Tabs created:
  Main — [X] rows
  Servicing — [X] rows
  Lending — [X] rows
  CX, Tech & Others — [X] rows

Ready for delivery.
```

---

## Edge Cases

### No Persona Column Exists
If the input file has no persona column at all (e.g., a raw scraped list that hasn't been vetted):
- Inform the user: "No persona column found. This list may not have been through title vetting yet. Do you want to: (a) create Main tab only with standard columns, (b) provide a persona column name to look for?"
- If user picks (a), generate Main tab only with standard columns. Skip persona tabs.

### UNFIT Rows
Rows with `UNFIT` as the persona value are included in the Main tab but excluded from all persona tabs. If the user wants an UNFIT tab (e.g., for review), they can request it during the grouping step.

### Blank Rows
Rows with blank persona are treated the same as UNFIT — Main tab only.

### xlsx With Multiple Sheets
If the input xlsx has multiple sheets (e.g., "Main List", "Company Research", "Flags & Issues"), only the main data sheet is processed. Other sheets are preserved as-is in the output file and appear after all generated tabs.

### Missing Required Columns
If a required standard column cannot be found in the source data and the user cannot identify it, halt and explain which column is missing. Do not generate a partial output with missing required columns unless the user explicitly approves.

### Ambiguous Column Matches
If a source column name could match multiple standard columns (e.g., `email` could be `[final] Emails` or something else), present the ambiguity and ask the user to resolve it before proceeding.

---

## Example Run

```
> Format this list for delivery: Kastle_MortgageLenders_NetNew100.xlsx

Found: Kastle_MortgageLenders_NetNew100.xlsx
Sheet: Main List
Rows: 658 (excluding header)
Columns: 42

Column mapping (source → standard):

  ✅ Mapped:
    "First Name" → First Name
    "Last Name" → Last Name
    "Full Name" → Full Name
    "Title" → Job Title
    "LinkedIn URL" → Person LinkedIn URL
    "Company" → Company Name
    "Company Website" → Company Website
    "Company LinkedIn URL" → Company LinkedIn URL
    "HQ Location" → Company Location
    "Location" → Person Location
    "Work Email" → [final] Emails
    "Valid Emails" → valid_emails
    "Catch All Emails" → catch_all_valid_emails
    "SMTP Provider" → SMTP Provider

  ⚠️ Not found (optional — will be omitted):
    Normalized Company Name

  🗑️ Will be deleted (28 columns):
    "Persona Type", "Email Verification Status", "other_work_emails",
    "company_revenue", "employee_count", "industry", "seniority",
    "department", "phone", ...

Does this mapping look right? (y/n)

> y

LinkedIn URL audit:
  Clean profiles (/in/): 612 rows
  Sales Navigator URLs: 3 rows
  Blank: 43 rows

Found 3 dud LinkedIn URLs. [shows details, sends to Clay]

> proceed anyway

Persona column: "Persona Type" (used for tabs, deleted from output)
Persona values:
  1. Tech / Product — 103
  2. Lending Ops — 83
  3. CEO / President — 60
  4. Consumer Direct / Sales — 27
  5. CX / Call Center — 23
  6. Servicing — 5
  [blank] — 357

> Tab "Servicing": Servicing
> Tab "Lending": Lending Ops
> Tab "CX, Tech & Others": CX / Call Center, Tech / Product, Consumer Direct / Sales, CEO / President

Proceed? (y/n)

> y

Output: Kastle_MortgageLenders_NetNew100_formatted.xlsx

Standard columns: 14 columns (Normalized Company Name omitted)
Columns deleted: 28 non-standard columns removed

Tabs created:
  Main — 658 rows
  Servicing — 5 rows
  Lending — 83 rows
  CX, Tech & Others — 113 rows

Ready for delivery.
```

---

## Technical Notes

### Python Dependencies
- `openpyxl` — for xlsx read/write
- `csv` — for csv read (stdlib)
- `sys` — for encoding (stdlib)
- `re` — for illegal character stripping (stdlib)

Always set `sys.stdout.reconfigure(encoding='utf-8')` on Windows.

### Illegal Character Stripping

Some source CSVs contain control characters (e.g. `\ufffd` replacement chars, `\x00`–`\x1f` control codes) in description fields that cause `openpyxl.utils.exceptions.IllegalCharacterError` at write time. Always strip these before writing any cell value:

```python
import re
ILLEGAL_CHARS = re.compile(r'[\x00-\x08\x0b\x0c\x0e-\x1f\x7f-\x9f\ufffd]')

def clean(val):
    if isinstance(val, str):
        return ILLEGAL_CHARS.sub('', val)
    return val
```

Apply `clean()` to every cell value when writing data rows. Header values do not need cleaning.

### File Naming
Output file = `[input_name]_formatted.xlsx`
- If input is `Kastle_MortgageLenders.xlsx` → output is `Kastle_MortgageLenders_formatted.xlsx`
- If input is `pipeline_operators_merged.csv` → output is `pipeline_operators_merged_formatted.xlsx`
- Output goes in the same directory as the input file.

### Sheet Name Limits
xlsx sheet names max 31 characters. If a persona group label exceeds 31 chars, truncate intelligently:
- "CX, Tech & Others" → fine (18 chars)
- "P3-QA/Regulatory Compliance" → fine (27 chars)
- "Pipeline Integrity / Engineering" → truncate to "Pipeline Integrity / Eng." (25 chars)

### Performance
For large files (2000+ rows), use `write_only` mode in openpyxl for output to avoid memory issues. Read the entire input into memory first, then write tabs sequentially.

### Preserved Sheets
If the input xlsx has non-data sheets (Company Research, Flags & Issues, Delivery Summary), copy them to the output file after all generated tabs. This preserves the full context of the original deliverable.
