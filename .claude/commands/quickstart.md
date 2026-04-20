---
name: quickstart
description: Scaffold a new model folder (per-model knowledge_base + 00_foundation) in the multi-model repo
model: inherit
---

# Quickstart — XP Labs (Multi-Model)

Create a new model folder at the repo root with a complete empty scaffolding.

## Input

Required: `<model-name>` — the companion's slug (lowercase, hyphens), e.g. `ava-laurent`, `mia-russo`.

If no argument is given, list existing model folders at the repo root and show the usage:
```
Existing models:
- ava-laurent
- mia-russo

Usage: /quickstart <model-name>
Example: /quickstart ava-laurent
```

## Process

### 1. Check existing structure

If `<model-name>/` already exists at the repo root:
```
⚠️  Model folder '<model-name>/' already exists.

Options:
1. Add missing subdirs + READMEs only (preserve existing content)
2. Skip — work with the existing folder as-is
3. Full reset (DESTRUCTIVE — wipes the model folder)

What would you like to do?
```

Wait for explicit choice. Never proceed destructively without confirmation.

### 2. Create per-model folders

```bash
mkdir -p <model-name>/knowledge_base/{audience,companions,niches,platforms,monetization,sales-scripts,tech-stack,competitors,methodology}
mkdir -p <model-name>/00_foundation/{positioning,strategy,content-playbook,sales-playbook}
mkdir -p <model-name>/00_foundation/companions/{active,queue,retired}
mkdir -p <model-name>/00_foundation/campaigns/{idea-queue,launched}
mkdir -p <model-name>/00_foundation/_synthesis/{weekly-sitreps,monthly-reviews}
```

### 3. Date-aware launched-campaigns scaffold

For the **current year and current month only**:
```bash
mkdir -p "<model-name>/00_foundation/campaigns/launched/[YEAR]/[MONTH]"
for N in 1..weeks_in_month:
    mkdir -p "<model-name>/00_foundation/campaigns/launched/[YEAR]/[MONTH]/week_${N}"
```

Do not create past or future month folders.

### 4. Populate README stubs

Write a README in each subfolder explaining what goes there. Use the same conventions as the repo-wide docs. The READMEs should reference this model by name where relevant (e.g., `audience/README.md`: "Intel on the men this companion (<model-name>) targets").

The model's `00_foundation/README.md` should also note:
- This is the operational layer for `<model-name>`
- Shared doctrine (methodology, templates, knowledge-graph config) lives at the repo root — it's not duplicated here
- The character sheet for this model lives at `<model-name>/knowledge_base/companions/companion-<model-name>.md` (or similar slug)

### 5. Confirm

```
✅ Scaffolded model folder: <model-name>/

Structure:
<model-name>/
├── knowledge_base/
│   ├── audience/  companions/  niches/  platforms/  monetization/
│   └── sales-scripts/  tech-stack/  competitors/  methodology/
└── 00_foundation/
    ├── positioning/  strategy/  content-playbook/  sales-playbook/
    ├── companions/{active,queue,retired}/
    ├── campaigns/idea-queue/
    ├── campaigns/launched/[YEAR]/[Month]/week_{1..N}/
    └── _synthesis/{weekly-sitreps,monthly-reviews}/

Shared resources at repo root (not duplicated):
- _system/knowledge_graph/{taxonomy,ontology}.yaml
- templates/
- .claude/commands, skills, agents

Next steps:
1. Build her character sheet:     /build-companion --model <model-name>
2. Ingest audience research:      /ingest <file> --model <model-name>
3. Draft her first story arc:     /draft-story-arc --model <model-name>
4. Check graph health:            /graph-health --model <model-name>
```

## Shared-vs-per-model reminder

Everything under `<model-name>/` is scoped to that model. **Do not duplicate** shared resources here:
- `_system/knowledge_graph/` — shared taxonomy + ontology at repo root
- `templates/` — shared node templates at repo root
- `.claude/` — shared commands, skills, agents at repo root
- `CLAUDE.md`, `CLIENT_INFO.md` — shared system docs at repo root

## Quality standards
- Always create the **full** per-model structure — don't skip folders
- Never overwrite existing content unless the user explicitly picks "Full reset"
- Date-aware folders: current year + current month only, weeks calculated dynamically
- Model-name slug must be lowercase, hyphens only, URL-safe
