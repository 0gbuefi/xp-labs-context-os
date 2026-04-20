# Email Format Writer Skills

This folder contains specialized skills that teach AI agents how to write each of XP Labs's email formats.

## Purpose

When the `/write-campaign` command runs, it invokes the appropriate format-specific skill based on user's choice. Each skill contains:
- Deep knowledge of that format's structure
- Examples and patterns
- Best practices
- Integration with copywriting standards

## Available Format Skills

### 1. write-front-end-offer
**Use when:** Pushing a lead magnet or low-friction offer to cold prospects

**Structure:** Hook → Problem → Solution/Offer → CTA

**Learn more:** `write-front-end-offer/SKILL.md`

---

### 2. write-poke-the-bear
**Use when:** Gauging interest/pain internally before asking for commitment

**Structure:** Surface problem → How you solve it → Soft CTA

**Learn more:** `write-poke-the-bear/SKILL.md`

---

### 3. write-one-liner
**Use when:** Ultra-brief emails that pack USP + mini case study into 32 words max

**Structure:** USP/MVO + mini case study (1-2 sentences max)

**Learn more:** `write-one-liner/SKILL.md`

---

### 4. write-bet-on-yourself
**Use when:** Prospect has made a relevant investment (hiring, tech, strategy) that you can reference and validate

**Structure:** Reference their investment → Validate + position as bridge → Soft CTA

**Learn more:** `write-bet-on-yourself/SKILL.md`

---

## How to Add New Email Formats

As the agency evolves, you may discover new email formats that work. Here's how to add them:

### Step 1: Create New Skill Folder
```
.claude/skills/email-format-writers/write-[format-name]/
```

### Step 2: Create SKILL.md
Follow the template structure from existing skills:
- Format name and description
- When to use this format
- Structure breakdown
- Examples (at least 3)
- Best practices
- Common mistakes to avoid
- Integration with xp-labs-copywriting-standards

### Step 3: Update This README
Add the new format to the "Available Format Skills" section above

### Step 4: Update /write-campaign Command
Add the new format as an option in Process 0 (user selection)

### Step 5: Test
Run `/write-campaign` with the new format on a test client before using in production

---

## Standards Compliance

All format skills must enforce **XP Labs Copywriting Standards**:
- Located: `.claude/skills/cold-email-domain-expert-knowledge-base/knowledge_base/copywriting/xp-labs-copywriting-standards.md`
- Non-negotiable rules that apply across ALL formats
- Skills teach format-specific structure WITHIN these constraints

---

## Related Resources

- **Copywriting Standards:** `.claude/skills/cold-email-domain-expert-knowledge-base/knowledge_base/copywriting/xp-labs-copywriting-standards.md`
- **Domain KB (Copywriting):** `.claude/skills/cold-email-domain-expert-knowledge-base/knowledge_base/copywriting/`
- **Domain KB (Campaign Strategy):** `.claude/skills/cold-email-domain-expert-knowledge-base/knowledge_base/campaign-strategy/`
- **/write-campaign Command:** `.claude/commands/write-campaign.md`

---

**Last Updated:** 2026-01-26
