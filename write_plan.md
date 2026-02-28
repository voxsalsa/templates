---
id: write_plan_v1
name: Write Plan
description: Create a detailed implementation plan saved to docs/plans/ — assumes zero codebase context, with exact file paths, complete code, and verification steps for every task.
slots: [task, context, requirements, constraints, acceptance_criteria]
example_triggers:
  - write implementation plan
  - write a plan for
  - create a plan
  - plan this feature
  - document the plan
  - plan before coding
---
## Feature
{{task}}

## Relevant Files / Context
{{context}}

## Details
{{requirements}}

## Constraints
{{constraints}}

## Done When
{{acceptance_criteria}}

---

Write a complete implementation plan assuming the implementer has zero codebase context and questionable taste. They are skilled but unfamiliar with the toolset or problem domain. Document everything they need.

**Save to:** `docs/plans/YYYY-MM-DD-<slug>.md`

**Required plan header:**
```
# [Feature] Implementation Plan

**Goal:** [one sentence]
**Architecture:** [2-3 sentences]
**Tech Stack:** [key libs]

---
```

**Task granularity — each step is one action (2-5 minutes):**
- "Write the failing test" — step
- "Run it to see it fail" — step
- "Implement minimal code to pass" — step
- "Run tests and confirm pass" — step
- "Commit" — step

**Each task must include:**
- Exact file paths to create or modify (with line numbers for modifications)
- Complete code — never "add validation here", write it out in full
- Exact run command with expected output to verify each step
- A commit step at the end

**Principles:** DRY, YAGNI, TDD, frequent small commits.

**After saving the plan**, offer two execution options:
1. **Subagent-Driven (this session)** — dispatch fresh subagent per task, spec + code quality review after each, fast iteration
2. **Parallel Session (separate)** — open new session, execute in batches of 3 with review checkpoints
