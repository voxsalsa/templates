---
id: verify_complete_v1
name: Verify Complete
description: Verify work is actually complete before claiming done — runs evidence-based checks, shows full command output, no success claims without current verification evidence.
slots: [task, context, requirements, constraints, acceptance_criteria]
example_triggers:
  - verify before completing
  - check before done
  - verify this works
  - confirm it passes
  - verify before committing
  - make sure it actually works
---
## Claim to Verify
{{task}}

## What to Run
{{context}}

## Additional Checks
{{requirements}}

## Constraints
{{constraints}}

## Evidence Required
{{acceptance_criteria}}

---

**Iron Law: NO completion claim without fresh verification evidence in this response.**

If you haven't run the verification command in this response, you cannot claim it passes. "Should work" is not evidence. "Looks correct" is not evidence. Confidence is not evidence.

**Gate function — for EACH claim:**
1. Identify the command that proves it
2. Run the FULL command right now (not a partial check, not a cached result)
3. Read all output; check exit code; count failures
4. If output confirms → state the claim WITH the evidence (paste the relevant output)
5. If output does NOT confirm → state actual status with evidence

**Common failure modes:**

| Claim | Requires | Not sufficient |
|-------|----------|----------------|
| Tests pass | Test command output: 0 failures | Previous run, "should pass" |
| Build succeeds | Build command: exit 0 | Linter passing |
| Bug fixed | Original symptom no longer occurs | Code changed |
| Requirements met | Line-by-line checklist against spec | Tests passing |
| Agent completed | VCS diff shows actual changes | Agent reported "success" |

**Regression tests need red-green verification:**
Write test → run (must FAIL) → revert fix → run (must fail) → restore fix → run (must PASS). Seeing it pass once is not enough.

**Red flags — STOP if you notice:**
- Using "should", "probably", "seems to" about work state
- About to commit without running verification in this message
- Satisfied with a partial check ("linter passed" ≠ "build passed")
- Trusting an agent's success report without independently verifying
- About to express satisfaction ("Done!", "Perfect!", "Great!") before running anything
