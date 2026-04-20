# /create-lead-magnet

**Purpose:** Create on-demand lead magnets (usually PDFs) based on cold email correspondence when prospects respond positively to "test offers."

---

## What This Command Does

When you mention a lead magnet in a cold email to gauge interest (before it exists), and a prospect responds positively, this command:

1. Reads the email correspondence to understand what was promised
2. Researches the client's knowledge base for relevant content
3. Supplements with web research if needed
4. Generates the lead magnet content (markdown → HTML → PDF)
5. Creates both simple and branded PDF versions
6. Saves all files to the proper location
7. Updates the client's front-end-offers.md documentation

**This enables the "test first, build later" strategy** for lead magnets.

---

## Usage

```
/create-lead-magnet [correspondence-file] [style]
```

**Parameters:**
- `correspondence-file` (required): Path to file containing email exchange (e.g., "aa_canvas/aa_canvas.md")
- `style` (optional): "simple", "branded", or "both" (default: "simple")

**Examples:**
```
/create-lead-magnet aa_canvas/aa_canvas.md simple
/create-lead-magnet correspondence.md both
/create-lead-magnet aa_canvas.md branded
```

---

## Workflow

### Phase 1: Parse & Extract (Understanding the Promise)
**Agent:** General-purpose agent for parsing

**Task:**
1. Read the correspondence file
2. Extract key details:
   - Lead magnet name/title (what was promised?)
   - Promised content/structure (what did the email claim it would show?)
   - Specific deliverables mentioned (one-pager, checklist, guide, etc.)
   - Format promised (PDF, checklist, framework, etc.)
   - Target audience context from email
   - Prospect name/company (for context)

**Output:** Structured spec of what needs to be created

---

### Phase 2: Research & Gather Intel (Building the Content Foundation)
**Agent:** Explore agent for client knowledge base mining

**Sub-task 2.1 - Mine Client Knowledge Base**
1. Navigate to `knowledge_base/`
2. Search for relevant nodes:
   - ICPs (who is this for?)
   - Pain points (what problems does this solve?)
   - Value props (what's the unique approach?)
   - Technical capabilities (what can they deliver?)
   - Methodology (existing frameworks/processes)
   - Case studies (proof points to reference)
3. Read email voice/tone guidelines (`00_foundation/messaging/email-voice-and-tone.md`)
4. Compile client-specific context

**Sub-task 2.2 - Identify Knowledge Gaps**
- Compare what was promised vs. what's in knowledge base
- Flag missing intel needed to deliver on promise
- Determine if web research is needed

**Sub-task 2.3 - Web Research (if needed)**
**Agent:** General-purpose agent with Firecrawl access
- Use Firecrawl for scraping industry best practices and specific frameworks
- Search for:
  - Industry best practices for the topic
  - Competitor lead magnets (for structure inspiration)
  - Recent data/stats to include
  - Credible sources for claims
- Compile research notes

**Sub-task 2.4 - Synthesis**
- Combine client knowledge + web research
- Create content brief with key points for each section
- Ensure deliverable matches the promise from email

**Output:** Content brief with all research organized by section

---

### Phase 3: Structure & Outline (Architecting the Lead Magnet)
**Agent:** General-purpose agent for structured thinking

**Task:**
1. Create detailed outline based on:
   - What was promised in the email (this is the contract)
   - Client's voice/tone guidelines
   - Research findings
   - Lead magnet best practices (scannable, actionable, specific)

2. Define structure:
   - Header/title section (lead magnet name, client branding)
   - Core content sections (based on promise)
   - Footer/CTA (soft pitch + next step)

3. Validate against promise:
   - Does it deliver on every claim made in the email?
   - Is it the right format (one-pager, multi-page, etc.)?
   - Does it match the scope (not over-delivering or under-delivering)?

**Output:** Complete outline with section-by-section structure

---

### Phase 4: Generate Content (Writing the Lead Magnet)
**Agent:** General-purpose agent for content creation

**Task:**
1. Draft the full lead magnet content based on outline
2. Use client's voice/tone:
   - Check `email-voice-and-tone.md` for style guidelines
   - Match brand personality (data-driven, conversational, direct, etc.)
   - Use approved phrases and positioning
3. Include:
   - Actionable insights (not just theory)
   - Specific frameworks/checklists (tactical)
   - Real examples where possible (client case studies if relevant)
   - Client branding/positioning naturally woven in
4. Add soft CTA:
   - Natural next step (book a call, get audit, etc.)
   - Contact info for client
   - P.S. line if client requires it

**Output:** Full markdown content ready for formatting

---

### Phase 5: Format & Produce PDF (Creating Deliverable)
**Agent:** General-purpose agent for formatting

**Sub-task 5.1 - Convert to HTML**
1. Read appropriate template:
   - Simple: `templates/lead-magnets/simple-template.html`
   - Branded: `templates/lead-magnets/branded-template.html`
2. Convert markdown content to HTML
3. Apply template styling
4. Ensure proper formatting (headings, tables, lists, callouts)

**Sub-task 5.2 - Generate PDF**
1. Use `page.setContent()` to load HTML
2. Use `page.pdf()` to generate PDF:
   - Format: Letter size
   - Margins: 0.75in (simple) or 0.5in (branded)
   - Print background: true (for colors/gradients)
3. Save to: `00_foundation/messaging/lead-magnets/[name]/[name]-[style].pdf`

**Sub-task 5.3 - Save All Versions**
Create subfolder: `00_foundation/messaging/lead-magnets/[name]/`

Then save:
- Markdown: `[name]/[name].md`
- HTML (simple): `[name]/[name]-simple.html`
- PDF (simple): `[name]/[name]-simple.pdf`
- HTML (branded): `[name]/[name]-branded.html` (if requested)
- PDF (branded): `[name]/[name]-branded.pdf` (if requested)

**Output:** PDF files ready to send to prospect

---

### Phase 6: Document & Track (Knowledge Compounding)
**Agent:** General-purpose agent for documentation

**Sub-task 6.1 - Update Front-End Offers**
1. Read `00_foundation/messaging/front-end-offers/front-end-offers.md`
2. Increment `total_offers` count
3. Add new offer entry with:
   - Offer number and name
   - Type (Educational PDF / Lead Magnet)
   - Description (what it delivers)
   - Format (markdown, HTML, PDF)
   - Typical use case
   - Target ICP
   - CTA (from original email)
   - Status (Active)
   - Source (when created, why)
   - Created for (prospect details)
   - Files location
   - Notes (context, strategy, positioning)

**Sub-task 6.2 - Log Creation Event**
- Note what was created, when, for whom
- Track if lead magnet was promised in email vs. created proactively
- Document any learnings (e.g., "prospect responded within 2 hours of receiving PDF")

**Sub-task 6.3 - Optional: Create Knowledge Node**
If this becomes a repeatable offer:
- Create node in `knowledge_base/methodology/`
- Tag with: `#lead-magnet`, `#validated` (since prospect requested it)
- Link to relevant ICPs and pain points

**Output:** Updated documentation, ready for future reference

---

## File Structure Created

After running this command, the following structure will exist:

```
00_foundation/messaging/
├── lead-magnets/                           # Lead magnets directory
│   └── [lead-magnet-name]/                 # Subfolder for this lead magnet
│       ├── [lead-magnet-name].md           # Source content (markdown)
│       ├── [lead-magnet-name]-simple.html  # Simple HTML version
│       ├── [lead-magnet-name]-simple.pdf   # Simple PDF (ready to send)
│       ├── [lead-magnet-name]-branded.html # Branded HTML (if requested)
│       └── [lead-magnet-name]-branded.pdf  # Branded PDF (if requested)
└── front-end-offers/
    └── front-end-offers.md                 # Updated with new offer
```

**Organization Benefits:**
- Each lead magnet is self-contained in its own folder
- Easy to find all related files (markdown, HTML, PDF versions)
- Scalable as you create more lead magnets
- Room for future additions (images, supplementary files, etc.)

---

## Quality Standards

### Every Lead Magnet Must:
1. ✅ **Deliver on the email promise** (don't over-promise in email, under-deliver in PDF)
2. ✅ **Match client voice/tone** (check email-voice-and-tone.md)
3. ✅ **Be immediately actionable** (frameworks, checklists, templates—not just theory)
4. ✅ **Include soft CTA** (natural next step, not hard sell)
5. ✅ **Reference client expertise** (weave in positioning, case studies, frameworks)
6. ✅ **Be scannable** (headings, tables, lists, callouts—easy to skim)
7. ✅ **Include visual hierarchy** (not a wall of text)
8. ✅ **Be brand-appropriate** (simple for scrappy outreach, branded for premium positioning)

### Format Requirements:
- **One-pager:** Fit on 1 page (Letter size, 0.75" margins)
- **Multi-page:** Use clear sections, page breaks, navigation
- **Tables:** Use for comparisons (STOP vs. START, Before vs. After)
- **Checklists:** Use ✅/❌ for visual clarity
- **Callouts:** Highlight key insights, warnings, pro tips

---

## Common Lead Magnet Types

Based on cold email patterns, common lead magnets include:

### 1. Checklist / Diagnostic
- "Where [problem] breaks down"
- "5 signs you're making [mistake]"
- "Testing hygiene checklist"

**Structure:**
- Diagnostic section (red flags)
- Comparison table (stop vs. start)
- Action plan (30-60-90 day)

---

### 2. Framework / Process
- "[Number]-step framework for [outcome]"
- "How we [result] in [timeframe]"
- "[Process name] playbook"

**Structure:**
- Overview of framework
- Step-by-step breakdown
- Examples/case studies
- Implementation guide

---

### 3. Profit Sheet / Calculator
- "No-cost profit sheet showing [metrics]"
- "[ROI] calculator"
- "CAC ceiling analysis"

**Structure:**
- Explanation of methodology
- Key metrics defined
- Sample calculation
- How to apply to their business

---

### 4. Swipe File / Template
- "[Number] proven [asset type]"
- "Email templates that drove [result]"
- "Ad creative frameworks"

**Structure:**
- Introduction to approach
- Template 1, 2, 3... (with context)
- How to customize
- When to use each

---

### 5. Guide / Playbook
- "Complete guide to [topic]"
- "[Process] playbook"
- "How to [outcome] in [timeframe]"

**Structure:**
- Problem overview
- Solution framework
- Step-by-step execution
- Common pitfalls
- Next steps

---

## Templates Available

**Location:** `templates/lead-magnets/`

### 1. Simple Template (`simple-template.html`)
**Use when:**
- Scrappy, direct outreach
- Low-friction, high-volume campaigns
- Testing new lead magnet concepts
- Founder-to-founder emails

**Styling:**
- Clean, minimal design
- Standard fonts (system fonts)
- Black/white/gray palette
- No heavy branding
- Fast to generate

---

### 2. Branded Template (`branded-template.html`)
**Use when:**
- Premium positioning
- Enterprise prospects
- High-value engagements
- Professional branding matters

**Styling:**
- Gradient headers
- Brand colors
- Professional typography
- Logo/brand elements
- Visual polish

---

## When to Create Lead Magnets

### ✅ Create when:
1. **Prospect responds positively** to email mentioning a lead magnet (TEST FIRST strategy)
2. **Multiple prospects** ask for the same resource (validates demand)
3. **Common objection** can be addressed with educational content
4. **New ICP segment** needs specific positioning
5. **Campaign angle** requires proof/credibility boost

### ❌ Don't create when:
1. **No demand validated** (don't build speculatively—mention in emails first)
2. **Existing offer** already covers it (check front-end-offers.md first)
3. **Too complex** for PDF (offer audit/call instead)
4. **Client doesn't have expertise** in topic (can't deliver on promise)

---

## Pro Tips

### Test Before Building
**The "Just-In-Time" Strategy:**
1. Mention lead magnet in cold email (with descriptive name)
2. If prospect responds positively → Use this command to build it
3. If no one responds → Don't build it (saves time)
4. Track response rates to validate lead magnet concepts

**Example:**
- Email: "I can send you a 'Testing Hygiene Checklist' showing where ad learnings break down..."
- Prospect: "Sure, please send over the resource"
- You: Run `/create-lead-magnet aa_canvas.md simple`
- Result: Lead magnet created in <30 min, sent immediately

---

### Naming Conventions
**Good names (descriptive, outcome-focused):**
- ✅ "Testing Hygiene Checklist"
- ✅ "30-Day Ad Scaling Framework"
- ✅ "CAC Ceiling Calculator"
- ✅ "5 ROAS Killers & How to Fix Them"

**Bad names (vague, generic):**
- ❌ "Marketing Guide"
- ❌ "Our Framework"
- ❌ "Free Resource"

---

### Content Best Practices
1. **Lead with pain, not pitch:** Start with the problem, show you understand it
2. **Be specific:** "Scale Meta revenue 20-30%" > "Improve performance"
3. **Use numbers:** "5 breakdown points" > "Common mistakes"
4. **Make it actionable:** "Do this" > "Consider this"
5. **Reference proof:** Client case studies, stats, benchmarks
6. **Soft CTA:** "Want us to run your numbers?" > "Book a demo now"

---

### Delivery Best Practices
1. **Send immediately:** Prospect requested it, don't make them wait
2. **Personalized email:** "Here's the Testing Hygiene Checklist you asked for..."
3. **Context reminder:** "You mentioned you're scaling ad spend and ROAS is inconsistent..."
4. **Ask qualifying question:** "Curious—which of these 5 breakdown points resonated most?"
5. **Include next step:** "If you want us to audit your numbers, here's my calendar..."

---

## Integration with Campaign Tracking

When a lead magnet is delivered:

1. **Log in weekly campaign file:**
   - Note lead magnet was sent
   - Track response (did they reply? book a call?)
   - Conversion rate (lead magnet → meeting)

2. **Update front-end-offers.md:**
   - Add to "Used in campaigns" section
   - Track performance over time

3. **Iterate based on results:**
   - If high conversion → Create variations
   - If low conversion → Revise content or test different angle
   - If no response → Archive and try different offer

---

## Error Handling

### If correspondence file not found:
- Prompt user to provide path or paste content directly
- Example: "I couldn't find that file. Please provide the correspondence or paste the email exchange."

### If knowledge base is empty:
- Warn that lead magnet will rely heavily on web research
- Ask if user wants to proceed or populate knowledge base first
- Example: "XP Labs's knowledge base is sparse. Should I proceed with web research only, or do you want to add context first?"

### If web research fails:
- Fall back to client knowledge base only
- Note in documentation that content may need enrichment
- Example: "Web research failed. Lead magnet created from client knowledge base only. Consider enriching with industry data manually."

---

## Success Metrics

Track these to validate the "test first, build later" strategy:

1. **Response rate to emails mentioning lead magnets:** What % of prospects say "yes, send it"?
2. **Time to create:** How long from prospect request → PDF delivered? (Goal: <30 min)
3. **Lead magnet → meeting conversion:** What % of prospects book call after receiving PDF?
4. **Reuse rate:** How many times is each lead magnet sent? (1x = one-off, 10x = validated)
5. **Quality score:** Do prospects reply with insights/questions? (High engagement = quality content)

---

## Maintenance

### When to update a lead magnet:
- Industry best practices change
- Client methodology evolves (new framework, new case study)
- Feedback from prospects ("This was helpful, but I wish it covered X")
- Conversion rate drops (content may be stale)

### Version control:
- Use date stamps in file names if creating multiple versions
- Document changes in front-end-offers.md
- Archive old versions if significantly different

---

## Examples

### Example 1: Testing Hygiene Checklist (Onda)
**Email Promise:**
"If you're scaling ad spend and aren't seeing reasonable ROAS change, I can send you a free 'Testing Hygiene' checklist. It's a one-pager that shows where ad learnings might be breaking down, what to stop vs. what to keep, and a simple 30-day testing cadence you can realistically run."

**Prospect Response:**
"Hey, sure please send over the resource"

**Command:**
```
/create-lead-magnet onda aa_canvas/aa_canvas.md simple
```

**Result:**
- 3-page PDF (expanded from "one-pager" due to value density)
- Sections: Where learnings break down (5 red flags), STOP vs. KEEP table, 30-day cadence
- Voice: Direct, data-driven, specific (matches Onda's brand)
- CTA: "Want to see how your numbers stack up? Book a free audit"
- Delivered in <30 minutes from prospect request
- Files saved to: `00_foundation/messaging/lead-magnets/testing-hygiene-checklist/`

---

---

## Technical Notes

### PDF Generation
- Convert HTML to PDF using available tools (Python weasyprint, wkhtmltopdf, or browser-based generation)
- Options:
  - Format: Letter (8.5" x 11")
  - Print background: true (includes colors/gradients)
  - Margins: 0.75in all sides
- Output path: Absolute path to client's lead-magnets folder

### HTML Template Variables
Templates use `{{VARIABLE}}` placeholders:
- `{{TITLE}}`: Lead magnet title
- `{{SUBTITLE}}`: Tagline/subtitle
- `{{CONTENT}}`: Main HTML content
- `{{FOOTER}}`: Footer/CTA section

Simple template: Basic variable replacement
Branded template: Structured with header bar, content wrapper, footer section

---

## Future Enhancements

Potential improvements to this command:

1. **AI-generated imagery:** Use DALL-E or similar to create custom diagrams/visuals
2. **Interactive PDFs:** Add form fields, clickable TOC, bookmarks
3. **Multi-format output:** Also generate Google Doc, Notion page, landing page
4. **A/B testing:** Create 2 variations automatically, track which converts better
5. **Personalization:** Inject prospect's name, company, metrics into PDF
6. **Email template generation:** Auto-generate delivery email text
7. **Analytics integration:** Track PDF opens, time spent, pages viewed
8. **Automated delivery:** Send PDF directly to prospect via email API

---

## Related Commands

- `/ingest` - Process raw content into knowledge base (to enrich lead magnets)
- `/quickstart` - Create new client folder structure (includes lead-magnets folder)
- `/graph-health` - Check knowledge base quality (affects research phase)

---

**Created:** 2026-02-02
**Status:** Active
**Maintained by:** XP Labs
**Version:** 1.0

---

## Implementation Notes for Claude

When this command is invoked:

1. **Validate inputs:**
   - Correspondence file exists?
   - Style parameter valid?

2. **Spawn sub-agents:**
   - Use Task tool with `subagent_type="general-purpose"` for most phases
   - Use Task tool with `subagent_type="Explore"` for knowledge base mining (Phase 2.1)
   - Run agents in parallel where possible (e.g., client research + web research simultaneously)

3. **Coordinate phases:**
   - Wait for each phase to complete before next
   - Pass outputs between agents (via file writes or direct context)
   - Validate outputs at each phase

4. **Generate files:**
   - Create subfolder: `00_foundation/messaging/lead-magnets/[lead-magnet-name]/`
   - Use Write tool for markdown/HTML files in that subfolder
   - Generate PDF (save to same subfolder)
   - Ensure proper file paths (absolute paths on Windows: `C:/Users/...`)

5. **Update documentation:**
   - Edit front-end-offers.md (increment count, add offer entry)
   - Use current date (YYYY-MM-DD format)

6. **Error handling:**
   - Catch missing files, invalid clients, web fetch failures
   - Provide clear error messages
   - Suggest fixes

7. **Report to user:**
   - Summarize what was created
   - Show file paths
   - Confirm documentation updated
   - Suggest next steps (e.g., "PDF ready to send to prospect")

---

## Command Execution Flow

```
User runs: /create-lead-magnet aa_canvas.md simple

↓

1. Validate inputs (file exists?)
   ✅ aa_canvas.md found

↓

2. Parse correspondence (spawn agent)
   → Extract: "Testing Hygiene Checklist", promised content, prospect details

↓

3. Research (spawn 2 agents in parallel)
   → Agent A: Mine XP Labs knowledge base
   → Agent B: Web research on ad testing best practices

↓

4. Synthesize research
   → Combine findings into content brief

↓

5. Create outline
   → Structure based on promise + research

↓

6. Generate content (spawn agent)
   → Write full markdown content

↓

7. Format & generate PDF (spawn agent)
   → Convert markdown → HTML → PDF (simple style)

↓

8. Save all files
   → Create subfolder: lead-magnets/testing-hygiene-checklist/
   → Save .md, .html, .pdf to that subfolder

↓

9. Update documentation
   → front-end-offers.md updated

↓

10. Report to user
   → "Testing Hygiene Checklist created successfully!"
   → Files: [list paths]
   → Next: Send PDF to prospect
```

---

**End of Command Documentation**
