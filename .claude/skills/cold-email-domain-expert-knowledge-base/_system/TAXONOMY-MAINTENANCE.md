# Taxonomy Maintenance Guide

**Purpose:** Keep your taxonomy clean, useful, and reflective of XP Labs's actual cold email expertise as the knowledge base grows.

---

## When to Review Taxonomy

### Automatic Triggers

You'll be prompted to review when:

1. **Every 25 nodes ingested** - Milestone review
2. **Tag sprawl detected** - 10+ tags with ≤2 nodes each
3. **Orphan tags found** - Tags in taxonomy.yaml with 0 nodes
4. **Weak linking detected** - 5+ nodes with <3 links

### Manual Triggers

You should review when:

1. **Can't find the right tag** - When ingesting content, if you struggle to categorize
2. **Tags feel ambiguous** - Multiple tags seem to mean the same thing
3. **Monthly maintenance** - If actively using the system
4. **After major ingestion** - Just processed a book or large content batch

---

## Review Process (Step-by-Step)

### Step 1: Check Tag Distribution

**Command:**
```
"Show me tag distribution across cold email domain expert KB"
```

**What to look for:**
- Tags with 0 nodes (orphans - remove)
- Tags with 1-2 nodes (candidates for consolidation)
- Tags with 10+ nodes (healthy, keep)
- Tags that never get used (consider removing)

**Action:**
```
Edit: _system/taxonomy.yaml
- Remove orphan tags
- Note tags with <3 nodes for Step 2
```

---

### Step 2: Consolidation Check

**Look for overlapping tags:**

**Example:**
- `#subject-line-patterns` (2 nodes)
- `#subject-line-tactics` (1 node)
- `#subject-line-optimization` (3 nodes)

**Ask:**
- Do these represent distinct concepts?
- Or can they merge into `#subject-lines`?

**Action if consolidating:**
1. Edit nodes with old tags
2. Update to consolidated tag
3. Remove old tags from taxonomy.yaml

**Rule of thumb:**
- If <3 nodes per tag, consider consolidating
- If tags overlap significantly, merge them
- Keep tags distinct only if concepts are truly different

---

### Step 3: Coverage Check

**Review recent ingestions:**

**Ask:**
- Did I struggle to tag anything?
- Were there concepts that didn't fit existing categories?
- Are there emerging patterns not captured in taxonomy?

**Example gaps:**
- Ingested 3 nodes about "cold calling integration" but no tag exists
- Multiple nodes mention "follow-up sequences" but not a topic

**Action:**
```
Edit: _system/taxonomy.yaml

Add new topics under appropriate domain:
- cold-calling-integration → campaign_strategy_topics
- follow-up-sequences → campaign_strategy_topics
```

**Guideline:** Only add new tags if 3+ nodes would use them (or you anticipate 3+ in near future)

---

### Step 4: Precision Check

**Look for ambiguous tags:**

**Red flags:**
- Tag name is vague (e.g., `#best-practices`)
- Could mean multiple things (e.g., `#optimization` - optimize what?)
- Generic category (e.g., `#tips`)

**Action:**
```
Rename for clarity:
- #best-practices → remove (too vague)
- #optimization → split into specific optimizations
- #tips → integrate into specific topics
```

**Guideline:** Every tag should clearly indicate WHAT it covers. If ambiguous, rename or remove.

---

### Step 5: Ontology Alignment

**Check if relationships still make sense:**

**Read:** `_system/ontology.yaml`

**Ask:**
- Do relationship types still reflect how concepts link?
- Are there new relationship patterns emerging?
- Do linking requirements make sense (minimum 3 links)?

**Action:**
```
Update ontology.yaml if needed:
- Add new relationship types
- Update examples
- Adjust linking requirements if too strict/loose
```

---

## Maintenance Commands

### Check KB Health

```
"Check cold email domain expert KB health"
```

**Returns:**
- Total node count
- Tag distribution
- Orphan tags
- Weak linking alerts

### List All Tags

```
"Show me all tags used in cold email KB"
```

### Find Nodes by Tag

```
"Show me all nodes tagged with #subject-lines"
```

### Orphan Detection

```
"Find tags in taxonomy.yaml not used in any nodes"
```

---

## Common Maintenance Scenarios

### Scenario 1: Tag Sprawl

**Problem:**
You have 15 tags with only 1-2 nodes each. Hard to find things.

**Solution:**
1. Group related tags:
   - `#subject-lines`, `#subject-line-patterns`, `#subject-line-tips` → merge to `#subject-lines`
2. Remove one-off tags that don't represent patterns
3. Update affected nodes with consolidated tags

**Result:**
Cleaner taxonomy, easier to find relevant knowledge.

---

### Scenario 2: Missing Categories

**Problem:**
You ingest content about "cold email deliverability" but have no tags for it.

**Solution:**
1. Review if this is a one-off or recurring theme
2. If recurring (3+ nodes would use it):
   ```yaml
   # Add to taxonomy.yaml under appropriate domain
   metrics_analysis_topics:
     - deliverability-optimization
     - spam-filter-avoidance
   ```
3. Tag existing nodes with new topic
4. Future ingestions can use these tags

**Result:**
Taxonomy evolves to reflect your actual expertise.

---

### Scenario 3: Orphan Tags

**Problem:**
Taxonomy has tags you created but never use.

**Example:**
- `#cold-calling-tactics` (0 nodes)
- `#linkedin-outreach` (0 nodes)

**Solution:**
```yaml
# Remove from taxonomy.yaml

# OR if you plan to ingest content for these:
# Keep them but add comment:
# cold-calling-tactics  # Planned - book on order
```

**Guideline:**
- Remove if no plans to use
- Keep if content coming soon
- Don't pre-populate with speculative tags

---

### Scenario 4: Ambiguous Tags

**Problem:**
Tag meanings overlap or are unclear.

**Example:**
- `#email-structure` vs `#email-format` (what's the difference?)
- `#optimization` (optimize what? Too vague)

**Solution:**
1. **Choose the clearest term:**
   - Keep `#email-structure`, remove `#email-format`
2. **Make vague tags specific:**
   - `#optimization` → split into `#subject-line-optimization`, `#cta-optimization`, etc.
3. **Update nodes** with clearer tags

**Result:**
Unambiguous taxonomy, easy to query.

---

## Evolution Timeline Example

### Month 1: Seed Taxonomy
```yaml
- 6 domains
- ~20 tags
- Clean and minimal
```

### Month 2: First Consolidation
```yaml
- Added 3 new tags (deliverability, sequences, follow-ups)
- Merged 4 redundant tags into 2
- Removed 2 orphan tags
- Total: ~20 tags (stayed stable)
```

### Month 6: Mature Taxonomy
```yaml
- 6 domains (unchanged)
- ~25 tags (slight growth)
- Tags reflect actual expertise patterns
- High precision, low sprawl
- Easy to query and find knowledge
```

**Goal:** Taxonomy should grow slowly, stay clean, reflect reality.

---

## Quality Metrics

### Healthy Taxonomy

✅ **Most tags have 5+ nodes** (core concepts)
✅ **Few tags with 1-2 nodes** (minimal sprawl)
✅ **No orphan tags** (all tags used)
✅ **Clear, unambiguous names** (easy to query)
✅ **Spans all domains** (coverage)

### Unhealthy Taxonomy

❌ **20+ tags with 1-2 nodes** (sprawl)
❌ **10+ orphan tags** (unused)
❌ **Vague tags** (e.g., `#tips`, `#best-practices`)
❌ **Overlapping tags** (e.g., 5 different subject line tags)
❌ **Growing faster than nodes** (pre-optimization)

---

## Workflow: Quarterly Deep Review

**Every 3 months (or every 100 nodes):**

### 1. Export Tag Report
```
"Generate tag distribution report for cold email KB"
```

### 2. Identify Issues
- Orphan tags?
- Sprawl (10+ tags with <3 nodes)?
- Ambiguous tags?
- Missing coverage?

### 3. Plan Consolidation
- Group related tags
- Rename ambiguous ones
- Remove orphans
- Add missing categories

### 4. Execute Changes
- Edit `taxonomy.yaml`
- Update affected nodes
- Document changes

### 5. Validate
- Re-run health check
- Confirm improvements
- Update this guide if needed

---

## Taxonomy Philosophy

### Start Small
- Begin with seed taxonomy (~20 tags)
- Let reality shape growth
- Don't pre-optimize

### Add Deliberately
- New tag = 3+ nodes will use it
- Not based on speculation
- Based on actual content

### Consolidate Ruthlessly
- Merge overlapping tags
- Remove unused tags
- Keep it tight

### Reflect Reality
- Taxonomy should map to expertise
- Not aspirational (what you wish you knew)
- Actual (what you've ingested)

---

## Quick Reference

**Review triggers:**
- Every 25 nodes
- Monthly if active
- When can't find right tag
- Tag sprawl/orphan alerts

**Maintenance actions:**
1. Check tag distribution
2. Consolidate <3 node tags
3. Remove orphans
4. Add missing categories (if 3+ nodes)
5. Rename ambiguous tags
6. Update ontology if needed

**Goal:**
Clean, queryable, reality-based taxonomy that makes knowledge easy to find and use.

---

**Last Updated:** 2026-01-15
**Review Frequency:** Every 25 nodes or monthly
