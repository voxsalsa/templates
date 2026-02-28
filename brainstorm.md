---
id: brainstorm_v1
name: Brainstorm
description: Design a new feature from scratch before touching any code — explores requirements, proposes 2-3 approaches, gets design approval, then creates an implementation plan.
slots: [task, context, requirements, constraints, acceptance_criteria]
example_triggers:
  - brainstorm
  - let's design
  - new feature idea
  - I want to build
  - think about adding
  - explore this idea
---
## Feature / Idea
{{task}}

## Technical Context
{{context}}

## Background
{{requirements}}

## Constraints
{{constraints}}

## Success Criteria
{{acceptance_criteria}}

---

**Do NOT write any code until the design is explicitly approved.**

Follow these steps in order:

**Step 1: Explore project context**
Check relevant files, docs, and recent commits to understand what already exists. Every project goes through this step — even "simple" additions have unexamined assumptions.

**Step 2: Ask clarifying questions — one at a time**
Understand purpose, constraints, and success criteria. Ask one question per message. Prefer multiple-choice questions when possible. Focus on: what problem this solves, who uses it, what success looks like.

**Step 3: Propose 2-3 approaches**
For each approach: what it involves, the trade-offs, and your recommendation with reasoning. Lead with your recommended option and explain why. Apply YAGNI ruthlessly — remove unnecessary features from all options.

**Step 4: Present the design in sections**
Cover: architecture, components, data flow, error handling, testing approach. Scale each section to its complexity (a few sentences if straightforward, up to 200-300 words if nuanced). After each section ask: "Does this look right so far?" Revise before proceeding to the next section.

**Step 5: Write the design doc**
Save to `docs/plans/YYYY-MM-DD-<topic>-design.md` and commit.

**Step 6: Create an implementation plan**
Write a plan to `docs/plans/YYYY-MM-DD-<topic>.md` with this header:
```
# [Feature] Implementation Plan

**Goal:** [one sentence]
**Architecture:** [2-3 sentences]
**Tech Stack:** [key libs]
```
Each task must include: exact file paths, complete code (not "add validation" — write it out), exact run commands with expected output, and a commit step. TDD throughout: write failing test → watch it fail → implement → pass → commit.

After saving the plan, offer two execution options:
1. **Subagent-Driven (this session)** — fresh subagent per task, spec + code quality review after each
2. **Parallel Session (separate)** — open new session, execute in batches of 3 with checkpoints between
