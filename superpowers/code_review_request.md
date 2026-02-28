---
id: code_review_request_v1
name: Code Review Request
description: Request a structured code review for recently completed work — gets commit range, dispatches a reviewer subagent, and acts on findings by severity.
slots: [task, context, requirements, constraints, acceptance_criteria]
example_triggers:
  - request code review
  - review my code
  - check what I built
  - code review for
  - review this implementation
  - review before merging
---
## What Was Built
{{task}}

## Commit Range / Files Changed
{{context}}

## Requirements It Should Meet
{{requirements}}

## Constraints
{{constraints}}

## Done When
{{acceptance_criteria}}

---

**Step 1: Get the commit range**
```bash
BASE_SHA=$(git rev-parse HEAD~1)   # or: git merge-base HEAD origin/main
HEAD_SHA=$(git rev-parse HEAD)
echo "Reviewing $BASE_SHA..$HEAD_SHA"
```

**Step 2: Dispatch a code reviewer subagent**
Give the reviewer:
- What was implemented (what the code does)
- What it should do (the requirements / plan task)
- BASE_SHA and HEAD_SHA
- Brief description

Ask the reviewer to report: Strengths, Issues (Critical / Important / Minor), and overall assessment.

**Step 3: Act on findings by severity**
- **Critical** — fix immediately, before anything else
- **Important** — fix before moving to next task
- **Minor** — note for later, no block
- **Reviewer is wrong** — push back with technical reasoning; show working tests or code; ask for clarification

If reviewer raises an Important issue: fix it, then dispatch the reviewer again to confirm the fix. Do not self-certify.

**When to review:**
- After each task in subagent-driven development
- After completing a major feature
- Before merging to main
- When stuck (a fresh perspective often unblocks quickly)
