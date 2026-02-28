---
id: execute_plan_v1
name: Execute Plan
description: Execute an existing implementation plan file — load it, review for issues, then implement in batches of 3 tasks with reporting between batches.
slots: [task, context, requirements, constraints, acceptance_criteria]
example_triggers:
  - execute the plan
  - implement the plan
  - run this plan
  - follow the plan at
  - carry out the plan
  - start implementing the plan
---
## Plan to Execute
{{task}}

## Plan File Location
{{context}}

## Additional Context
{{requirements}}

## Constraints
{{constraints}}

## Done When
{{acceptance_criteria}}

---

**Never start implementation on main/master without explicit consent.**

**Step 1: Load and review**
Read the plan file. Review critically — identify concerns or gaps before starting. If concerned: raise with your partner before proceeding. If clear: create a todo list with all tasks and proceed.

**Step 2: Execute first 3 tasks**
For each task:
1. Mark as in_progress
2. Follow each step exactly as written — do not adapt or improve
3. Run the verification command specified; do not skip it
4. Mark as completed

**Step 3: Report**
Show what was implemented. Paste the verification output. Say: "Ready for feedback."

**Step 4: Continue**
Apply any feedback. Execute the next batch of 3. Repeat until all tasks are done.

**Step 5: Complete the branch**
After all tasks are verified:
1. Run the full test suite. STOP if anything fails — fix before proceeding.
2. Determine base branch:
   ```bash
   git merge-base HEAD main 2>/dev/null || git merge-base HEAD master 2>/dev/null
   ```
3. Present exactly these 4 options (no more, no fewer):
   ```
   Implementation complete. What would you like to do?
   1. Merge back to <base-branch> locally
   2. Push and create a Pull Request
   3. Keep the branch as-is (I'll handle it later)
   4. Discard this work
   ```
4. Execute the chosen option. For Option 4, require the user to type "discard" before proceeding.
5. Clean up worktree for Options 1 and 4. Keep for 2 and 3.

**STOP immediately if blocked.** Ask rather than guess.
