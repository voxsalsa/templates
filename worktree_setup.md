---
id: worktree_setup_v1
name: Worktree Setup
description: Set up an isolated git worktree before starting a feature — smart directory selection, gitignore safety check, project setup, and baseline test verification.
slots: [task, context, requirements, constraints, acceptance_criteria]
example_triggers:
  - set up a worktree
  - create a worktree
  - isolated workspace for
  - git worktree for
  - new worktree
  - work in isolation on
---
## Feature
{{task}}

## Context
{{context}}

## Requirements
{{requirements}}

## Constraints
{{constraints}}

## Done When
{{acceptance_criteria}}

---

**Step 1: Find the right directory — follow this priority order**

1. Check for existing worktree directories:
   ```bash
   ls -d .worktrees 2>/dev/null
   ls -d worktrees 2>/dev/null
   ```
   If both exist: use `.worktrees/`. If either exists: use it.

2. Check CLAUDE.md for a worktree directory preference:
   ```bash
   grep -i "worktree" CLAUDE.md 2>/dev/null
   ```
   If a preference is specified: use it without asking.

3. If nothing found: ask the user:
   ```
   No worktree directory found. Where should I create worktrees?
   1. .worktrees/ (project-local, hidden)
   2. ~/.config/superpowers/worktrees/ (global)
   ```

**Step 2: Safety check (for project-local directories)**
```bash
git check-ignore -q .worktrees 2>/dev/null && echo "ignored" || echo "NOT ignored"
```
If NOT ignored: add to `.gitignore` and commit that change BEFORE creating the worktree.

**Step 3: Create the worktree**
```bash
project=$(basename "$(git rev-parse --show-toplevel)")
branch="feature/<slug>"
git worktree add <dir>/$branch -b $branch
cd <dir>/$branch
```

**Step 4: Run project setup**
Auto-detect from project files:
```bash
if [ -f Cargo.toml ]; then cargo build; fi
if [ -f package.json ]; then npm install; fi
if [ -f requirements.txt ]; then pip install -r requirements.txt; fi
if [ -f go.mod ]; then go mod download; fi
```

**Step 5: Verify clean baseline**
```bash
cargo test    # or npm test / pytest / go test ./...
```
If tests fail: report the failures and ask whether to proceed or investigate first.
If tests pass: report the worktree path and test count.

**Report:**
```
Worktree ready at <full-path>
Tests passing (<N> tests, 0 failures)
Ready to implement <feature-name>
```
