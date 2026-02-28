---
id: write_skill_v1
name: Write Skill
description: Document a reusable technique as a reusable skill file — TDD for documentation: baseline failure first, then write skill, then verify an agent complies.
slots: [task, context, requirements, constraints, acceptance_criteria]
example_triggers:
  - write a skill
  - create a skill
  - document this technique
  - turn this into a skill
  - new skill for
  - add a skill about
---
## Technique to Document
{{task}}

## Context (when to use, related tools/patterns)
{{context}}

## What to Include
{{requirements}}

## Constraints
{{constraints}}

## Done When
{{acceptance_criteria}}

---

**This is TDD applied to documentation. Same discipline, same Iron Law.**

**Iron Law: NO skill without a failing baseline test first.** If you write the skill before running the baseline, delete it and start over.

**RED — Run baseline without the skill**
Dispatch a subagent WITHOUT the skill present. Give it the exact scenario the skill should handle. Observe and document verbatim:
- What choices does it make?
- What rationalizations does it use?
- Which pressures trigger violations?

Do NOT write the skill yet.

**GREEN — Write the minimal skill**
Create `skills/<skill-name>/SKILL.md` addressing those specific rationalizations. Structure:
```
---
name: skill-name-with-hyphens
description: Use when <specific triggering conditions — NOT a workflow summary>
---
# Skill Name
## Overview
## When to Use
## The Process
## Common Mistakes
## Red Flags
```

Rules for the frontmatter:
- `name`: letters, numbers, hyphens only (no parentheses or special chars)
- `description`: starts with "Use when...", describes triggering conditions only — never summarize the workflow (agents may follow the description instead of reading the skill body)

Run the same scenario WITH the skill. The agent must now comply.

**REFACTOR — Close loopholes**
Find any NEW rationalizations the agent uses even with the skill present. Add explicit counters. Re-test until the agent complies under maximum pressure.

**Personal skills:** `~/.claude/skills/<skill-name>/SKILL.md`
**Community skills:** submit to the skills repository as a PR.
