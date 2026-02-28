---
id: subagent_dev_v1
name: Subagent Development
description: Execute an implementation plan by dispatching a fresh subagent per task, with spec compliance review then code quality review after each task.
slots: [task, context, requirements, constraints, acceptance_criteria]
example_triggers:
  - subagent development
  - subagent-driven
  - dispatch subagents for
  - implement with subagents
  - use subagents to implement
  - fresh subagent per task
---
## Plan to Execute
{{task}}

## Plan File
{{context}}

## Additional Context
{{requirements}}

## Constraints
{{constraints}}

## Done When
{{acceptance_criteria}}

---

**Core principle:** Fresh subagent per task + two-stage review = high quality with no context pollution.

**Never start on main/master without explicit consent.**

**Step 1: Extract all tasks**
Read the plan file once. Extract all tasks with their full text and context into a todo list. Do not make subagents read the plan — provide the full text directly in each dispatch.

**Step 2: Per task — implementer subagent**
Dispatch a fresh subagent with:
- Full task text and context (from your extraction above)
- Instruction to: use TDD (write failing test first, watch it fail, write minimal code, verify all pass), self-review before handing back, commit when done

If subagent asks questions: answer clearly and completely before letting them proceed.

**Step 3: Per task — spec compliance review**
Dispatch a spec reviewer subagent with the task spec and the commit range. Ask: does the code match the spec exactly? Not over-built, not under-built?

If issues found: implementer subagent fixes them. Re-review. Do not move on until spec reviewer approves.

**Step 4: Per task — code quality review**
Dispatch a code quality reviewer subagent with the commit range. Ask: are there bugs, security issues, anti-patterns, missing error handling?

If issues found: implementer subagent fixes them. Re-review. Do not move on until quality reviewer approves.

**Do NOT start code quality review before spec compliance is approved.**

**Step 5: Mark task complete, move to next**

**Step 6: After all tasks — final code review**
Dispatch a final code reviewer for the entire implementation (full commit range from first to last task).

**Step 7: Complete the branch**
1. Run the full test suite. STOP if failing.
2. Determine base branch.
3. Present exactly these 4 options:
   ```
   Implementation complete. What would you like to do?
   1. Merge back to <base-branch> locally
   2. Push and create a Pull Request
   3. Keep the branch as-is (I'll handle it later)
   4. Discard this work
   ```
4. For Option 4: require "discard" typed confirmation.
5. Clean up worktree for Options 1 and 4 only.
