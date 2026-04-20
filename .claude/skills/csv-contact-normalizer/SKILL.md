---
name: csv-contact-normalizer
description: Normalize first names and company names in prospect CSVs for cold email personalization
model: inherit
---

# CSV Contact Normalizer

## Purpose

Clean scraped prospect CSVs so first names and company names are ready for personalized cold email outreach. Produces two new columns — **Normalized First Name** and **Normalized Company Name** — inserted immediately after their source columns.

---

## When to Use

- User provides a CSV of scraped contacts and asks to "normalize", "clean", or "prep" names/companies
- Before importing contacts into a cold email sending tool
- After merging/appending multiple prospect CSVs

---

## Inputs

- **CSV file path** (required)
- **Column names** — auto-detect with fallback. Look for columns matching:
  - First name: `First name`, `First Name`, `first_name`, `FirstName`
  - Company name: `Company name`, `Company Name`, `company_name`, `CompanyName`
  - Company website: `Company website`, `Company Website`, `company_website`, `Website`, `Domain` (optional, used as a hint for company normalization)
- If columns can't be found, ask the user to confirm which columns to use.

---

## Step-by-Step Process

### Step 1: Preview the Data

Read the CSV and print a numbered list of all unique first names and company names + websites. This lets you and the user spot edge cases before processing.

```
1. First: "Paula J." | Company: "The Hanover Insurance Group" | Website: "https://hanover.com"
2. First: "Jo Ann"   | Company: "Combined, a Chubb Company"   | Website: "https://combinedinsurance.com"
...
```

### Step 2: Identify Edge Cases

Flag items that need judgment calls:
- **Compound first names** that should be preserved (Jo Ann, Mary Kate, etc.)
- **Company names** that need manual mapping (e.g., "Combined, a Chubb Company" → what friendly name?)
- **Acronym companies** that should stay uppercase (FM, IBM, USAA, etc.)

Present these to the user and ask for confirmation before proceeding.

### Step 3: Normalize with Python

Run a Python script against the CSV that applies the rules below.

### Step 4: Print Before/After Table

Show a comparison table so the user can verify:

```
Original First     Normalized First   Original Company                    Normalized Company
--------------------------------------------------------------------------------------------------------------
Paula J.           Paula              The Hanover Insurance Group         Hanover
Jo Ann             Jo Ann             Combined, a Chubb Company          Combined Insurance
```

### Step 5: Confirm Column Placement

Ensure:
- `Normalized First Name` is the column immediately after the source first name column
- `Normalized Company Name` is the column immediately after the source company name column

### Step 6: Idempotency Check

If `Normalized First Name` or `Normalized Company Name` columns already exist in the CSV, **overwrite them** rather than creating duplicates.

---

## First Name Normalization Rules

**Goal:** Clean the name so it works in a greeting like "Hi [Name],"

1. **Strip middle initials.** Remove single-letter tokens with or without a trailing period.
   - "Paula J." → "Paula"
   - "Brandy M" → "Brandy"

2. **Remove middle names.** If there are two+ names and it's NOT a known compound name, keep only the first.
   - "James Patrick" → "James"

3. **Preserve compound first names.** Maintain a curated list. These stay as-is:
   - Jo Ann, Jo Anne, Mary Ann, Mary Anne, Mary Kate, Mary Beth, Mary Ellen, Mary Jane
   - Anna Marie, Anne Marie, Betty Jo, Billie Jean, Bobby Joe, Lee Ann, Lee Anne

4. **Fix casing.** Proper Case all names.
   - "vincenT" → "Vincent"
   - "DEBBIE" → "Debbie"

5. **Clean punctuation.** Remove trailing periods, commas, extra spaces.

6. **Strip symbols and non-letter characters.** Remove anything that isn't a letter, space, hyphen, or apostrophe. This catches arrows (→, ►, ▶), bullets (•, ▪, ■), emojis, stars (★, ☆), checkmarks (✓, ✔), copyright/trademark (©, ™, ®), pipes (|), and any other Unicode junk from scraped data. Apply this BEFORE all other rules so downstream steps work on clean input.
   - "►Sarah" → "Sarah"
   - "Mike →" → "Mike"
   - "•Amanda•" → "Amanda"
   - "David ✓" → "David"
   - Preserve: hyphens (Jean-Pierre), apostrophes (O'Brien), spaces (Jo Ann)

---

## Company Name Normalization Rules

**Goal:** Make the name sound natural in "I've been following the work at [Company]."

1. **Strip legal suffixes.** Remove: Inc., LLC, Corp, Corporation, Ltd, Limited, L.P., Co., Group, Holdings, Enterprises, Services (only when it's a generic suffix, not part of the core brand).

2. **Remove "The" prefix.** "The Hanover Insurance Group" → "Hanover"

3. **Remove generic descriptors.** Strip trailing words like "Insurance Group", "Insurance Services", "Insurance Company", "Financial Services" — BUT only when the core brand is recognizable without them.
   - "The Hanover Insurance Group" → "Hanover" (hanover.com confirms the brand)
   - "Erie Insurance Group" → "Erie Insurance" (erieinsurance.com suggests "Erie Insurance" is the brand)
   - "Liberty Mutual Insurance" → "Liberty Mutual"

4. **Handle subsidiary/parent labels.** Simplify "X, a Y Company" patterns.
   - "Combined, a Chubb Company" → "Combined Insurance" (guided by combinedinsurance.com)

5. **Preserve acronyms.** Keep uppercase if the name is an acronym.
   - "FM" stays "FM"
   - "IBM" stays "IBM"
   - "USAA" stays "USAA"

6. **Fix casing.** ALLCAPS becomes Proper Case, unless it's an acronym.
   - "NETFLIX" → "Netflix"
   - "MetLife" stays "MetLife" (mixed case is intentional branding)

7. **Use the website as a guide.** The domain often reveals the real brand name:
   - `ajg.com` → "Gallagher"
   - `hanover.com` → "Hanover"
   - `combinedinsurance.com` → "Combined Insurance"

8. **Clean punctuation.** Remove commas, periods, extra spaces.

---

## Python Reference Pattern

```python
import csv
import re

# --- Compound first names to preserve (extend as needed) ---
COMPOUND_NAMES = {
    "jo ann", "jo anne", "mary ann", "mary anne", "mary kate",
    "mary beth", "mary ellen", "mary jane", "anna marie",
    "anne marie", "betty jo", "billie jean", "bobby joe",
    "lee ann", "lee anne"
}

def normalize_first_name(name):
    # Strip symbols/non-letter chars first (keep letters, spaces, hyphens, apostrophes)
    name = re.sub(r"[^\w\s'\-]", '', name, flags=re.UNICODE)
    name = re.sub(r'[\d_]', '', name)  # also remove digits and underscores
    name = re.sub(r'\s+', ' ', name)   # collapse multiple spaces
    name = name.strip().rstrip('.,')
    lower = name.lower()
    for compound in COMPOUND_NAMES:
        if lower == compound:
            return ' '.join(w.capitalize() for w in compound.split())
    parts = name.split()
    if len(parts) > 1:
        second = parts[1].rstrip('.')
        if len(second) == 1:  # middle initial
            name = parts[0]
        else:
            name = parts[0]  # middle name — keep first only
    name = name.strip().rstrip('.,').capitalize()
    return name

# --- Company overrides (build per-CSV as needed) ---
COMPANY_MAP = {
    # "Legal Name": "Friendly Name",
}

LEGAL_SUFFIXES = re.compile(
    r',?\s*(Inc\.?|LLC|Corp\.?|Corporation|Ltd\.?|Limited|L\.?P\.?|'
    r'Holdings|Enterprises|Co\.?)$', re.IGNORECASE
)

def normalize_company(name, website=''):
    name = name.strip()
    if name in COMPANY_MAP:
        return COMPANY_MAP[name]
    cleaned = LEGAL_SUFFIXES.sub('', name).strip()
    cleaned = re.sub(r'^The\s+', '', cleaned).strip()
    return cleaned if cleaned else name
```

---

## Important Notes

- **Always preview before writing.** Show the user the before/after table and get confirmation before modifying the CSV.
- **Extend COMPOUND_NAMES** when you encounter new compound first names — ask the user if unsure.
- **Build COMPANY_MAP per CSV** — inspect unique company names, check websites, and create the override map before processing.
- **Never lose data.** The original columns are preserved. Normalized columns are additions.
- **Idempotent.** Safe to re-run — existing normalized columns get overwritten, not duplicated.
