---
name: git-workflow
description: Stage, commit, push, and open a PR — never directly to main
model: inherit
---

# XP Labs Git Workflow

> **This file is both a reference and an executable command.**
> When invoked as `/git-workflow`, read the current state of the repo (branch, modified files, untracked files) and execute the workflow below. Do not ask which workflow — infer it from context.

**The golden rule: never push directly to `main`. All changes go through a PR.**

`main` is the canonical branch. Collaborators pull from `main` to get the latest knowledge, commands, and skills. Every change must land via a reviewed PR so the system stays trustworthy and traceable.

---

## What this command does

1. Analyzes the current repo state (branch, staged/unstaged/untracked files).
2. Runs the **Pre-Commit Doc Sweep** to keep system-of-record files in sync.
3. If on `main` → creates a feature branch with the right prefix.
4. Stages files **explicitly by name** (never `git add -A` / `git add .`).
5. Commits with a typed message in the format below.
6. Pushes to `origin` and **always opens a PR** on GitHub (or updates the existing one).
7. Returns the PR URL.

---

## Step-by-step

### Step 1 — Analyze changes

Run in parallel:
```
git status
git diff
git log -5 --oneline
git branch --show-current
```

Understand what changed and why before writing the commit message. Group related changes together — one PR = one coherent change.

### Step 2 — Pre-Commit Doc Sweep (do this BEFORE staging)

Walk through this checklist. **If a commit changes what XP Labs's system does or how it's structured, the docs must ship in the same commit.** Do not leave docs for a follow-up PR.

| If the commit touches… | Update… |
|---|---|
| New/removed file in `.claude/commands/` | `CLAUDE.md` → **Commands** table |
| New/removed file/folder in `.claude/skills/` | `CLAUDE.md` → **Skills** table |
| New knowledge node type or domain | `CLAUDE.md` → **Knowledge Base Overview** (counts + descriptions) |
| New top-level directory or structural change | `CLAUDE.md` → **Directory Structure** tree |
| New `topics:` value used in a node frontmatter | `_system/knowledge_graph/taxonomy.yaml` (add the blessed tag) |
| New relationship type used in `related_concepts:` | `_system/knowledge_graph/ontology.yaml` |
| New template added to `templates/` | `CLAUDE.md` → **Templates** section |
| Client info (contact, stats, positioning) changed | `CLIENT_INFO.md` |
| New ICP / persona / pain point / value prop node | Bump the count in `CLAUDE.md` → **Knowledge Base Overview** |
| New campaign launched, killed, or paused | `00_foundation/messaging/active-campaigns.md` or `inactive-campaigns.md` |

If any of these need updating, edit them now and include them in the same commit.

### Step 3 — Branch check

Run: `git branch --show-current`

- **If on `main`** → create a feature branch:
  ```
  git checkout -b <type>/<short-description>
  ```
  Use the **Branch Naming** table below to pick the right prefix.
- **If already on a feature branch** → stay on it. Do not create a new branch.

### Step 4 — Stage files explicitly

Run `git status` to list every modified, deleted, and untracked file.

Stage each file by name:
```
git add path/to/file1.md path/to/file2.md
```

**Never use `git add -A` or `git add .`** — this prevents accidentally committing local notes, draft files, or anything in `knowledge_base/list-building/` (which is gitignored but easy to mishandle).

### Step 5 — Commit

Use a HEREDOC to preserve formatting:

```
git commit -m "$(cat <<'EOF'
<type>: <short summary in imperative mood>

- What changed
- Why it changed
- Any docs synced (from Step 2)

Co-Authored-By: Claude <noreply@anthropic.com>
EOF
)"
```

See **Commit Message Format** below for types and conventions.

### Step 6 — Push and open PR

Push the branch:
```
git push -u origin <branch-name>
```

Check if a PR already exists:
```
gh pr view --json url
```

- **If no PR exists** → open one. **Always open a PR** — never leave a pushed branch without one.
  ```
  gh pr create --title "<type>: <summary>" --body "$(cat <<'EOF'
  ## Summary
  - <bullet 1>
  - <bullet 2>

  ## Docs synced
  - <list any CLAUDE.md / taxonomy.yaml / etc. updates from Step 2, or "none">

  ## Reviewer notes
  - <anything reviewers should pay attention to>

  🤖 Generated with [Claude Code](https://claude.com/claude-code)
  EOF
  )"
  ```
- **If a PR already exists** → the push updates it automatically. Note this and return the existing PR URL.

**Return the PR URL to the user.**

### Step 7 — Post-merge cleanup (only after the PR is merged on GitHub)

```
git checkout main
git pull origin main
git branch -d <branch-name>
git push origin --delete <branch-name>
```

If starting new work immediately, create a new descriptive branch — do not stay on `main`.

---

## Branch Naming

| Type | Pattern | Example |
|---|---|---|
| Knowledge node add/edit | `knowledge/short-desc` | `knowledge/add-saas-icp` |
| Campaign work | `campaign/short-desc` | `campaign/confidence-crisis-q2` |
| New command, skill, or template | `feat/short-desc` | `feat/add-review-command` |
| Docs / structure / `CLAUDE.md` | `chore/short-desc` | `chore/update-claude-md` |
| Fix (broken links, typos, wrong frontmatter) | `fix/short-desc` | `fix/broken-wikilinks` |

Always name the branch for what you intend to do — never use placeholders like `chore/next` or `chore/updates`. If you realize mid-work that the name is wrong, rename before pushing:
```
git branch -m <better-name>
```

---

## Commit Message Format

```
<type>: <short summary in imperative mood> (50-72 chars)

- What changed (bullet list of key modifications)
- Why it changed (purpose / motivation)
- Docs synced (list any CLAUDE.md, taxonomy, ontology updates)

Co-Authored-By: Claude <noreply@anthropic.com>
```

**Types:** `feat`, `fix`, `chore`, `docs`, `knowledge`, `campaign`

---

## Hard Rules

- **Never commit directly to `main`** — always feature branch + PR.
- **Never use `git add -A` or `git add .`** — stage files explicitly by name.
- **Never push without opening a PR** — every pushed branch gets a PR immediately.
- **Never skip the Pre-Commit Doc Sweep** — out-of-sync docs erode trust in the system.
- **Never force-push to `main`.**
- **Never commit files from `knowledge_base/list-building/`** — gitignored for a reason (large, iterative, often contains client lead data).
- **If a commit changes the system, ship the docs in the same commit** — no follow-up PRs for documentation.

---

## Quick Reference

| What I need to do | Command |
|---|---|
| Stage, commit, push, open PR | `/git-workflow` |
| See what would be committed | `git status && git diff` |
| Rename current branch | `git branch -m <new-name>` |
| Check open PRs | `gh pr list` |
| View current PR | `gh pr view --web` |
