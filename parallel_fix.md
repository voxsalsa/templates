---
id: parallel_fix_v1
name: Parallel Fix
description: Fix multiple independent problems simultaneously — dispatches one agent per domain when failures have different root causes and no shared state between investigations.
slots: [task, context, requirements, constraints, acceptance_criteria]
example_triggers:
  - fix in parallel
  - dispatch parallel agents
  - multiple independent failures
  - fix these separately
  - run parallel investigation
  - multiple issues at once
---
## Independent Problems
{{task}}

## Files / Components Involved
{{context}}

## Additional Context
{{requirements}}

## Constraints
{{constraints}}

## Done When
{{acceptance_criteria}}

---

**Core principle:** One agent per independent problem domain. Run them concurrently.

**When to use:**
- 3+ failures across different subsystems or test files
- Each problem can be fully understood without context from the others
- No shared state between investigations
- Fixing one domain cannot accidentally fix or break another

**When NOT to use:**
- Failures share a root cause (fix one might fix others — investigate together first)
- Agents would need to modify the same files
- You need full system context to understand what's broken
- The problem is exploratory (you don't know yet what's wrong)

**Step 1: Identify independent domains**
Group failures by what's broken, not by file location. A race condition in auth and a null pointer in rendering are independent even if both show up as failing tests.

**Step 2: Verify independence**
Confirm: fixing domain A cannot affect domain B. If uncertain, treat them as related and investigate together first.

**Step 3: Write a focused agent task for each domain**
Each task must include:
- **Specific scope:** One test file, one subsystem, or one component — no broader
- **Clear goal:** "Make these specific tests pass" or "Fix this specific crash"
- **All context needed:** Paste the error messages and test names directly
- **Constraints:** "Do not change code outside this module"
- **Expected output:** Summary of root cause and what was changed

**Step 4: Dispatch all agents concurrently**
Use the Task tool to dispatch them in a single message so they run in parallel.

**Step 5: Review and integrate**
When all agents return:
- Read each summary to understand what changed
- Check for conflicts: did any two agents modify the same files?
- Run the full test suite on the integrated result
- If conflicts exist: resolve them before committing
