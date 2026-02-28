---
id: pr_code_review_v1
name: PR Code Review
description: Review recently written or modified code for guideline violations, bugs, and quality issues — only reports findings with 80%+ confidence to filter false positives.
slots: [task, context, requirements, constraints, acceptance_criteria]
example_triggers:
  - review this code
  - code review
  - check my implementation
  - review before commit
  - review before PR
  - check for bugs
---
## What Was Implemented
{{task}}

## Files / Commit Range
{{context}}

## Guidelines It Should Follow
{{requirements}}

## Constraints
{{constraints}}

## Done When
{{acceptance_criteria}}

---

Review recently modified code for guideline compliance, bugs, and quality issues. Focus on recently modified sections unless told otherwise (run `git diff` to identify them).

**Confidence threshold: only report issues scoring 80 or above (0-100 scale).**
- 90-100: Critical — explicit guideline violation or clear bug
- 80-89: Important — requires attention before merging
- Below 80: Do not report — likely a false positive

**Step 1: Get the changes**
```bash
git diff          # unstaged
git diff --staged # staged
# or a specific range: git diff BASE_SHA..HEAD_SHA
```

**Step 2: Check guideline compliance**
Read CLAUDE.md (or equivalent project rules). For each modified file, check:
- Naming conventions and code style
- Import patterns and framework usage
- Error handling requirements
- Testing requirements
- Any project-specific rules

**Step 3: Check for bugs**
For each modified section, look for:
- Logic errors and off-by-one conditions
- Null/undefined/None access without guards
- Race conditions and shared state issues
- Security vulnerabilities (injection, unvalidated input, exposed secrets)

**Step 4: Check code quality**
- Unnecessary duplication
- Missing error handling for fallible operations
- Insufficient test coverage for new behavior

**Step 5: Report**
Organize by severity. For each issue include:
- Description of the problem
- Confidence score (80-100)
- File and line location
- Relevant guideline (if applicable)
- Suggested fix
