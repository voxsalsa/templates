---
id: finish_branch_v1
name: Finish Branch
description: Complete a development branch — verify all tests pass, then present exactly 4 options: merge locally, push PR, keep as-is, or discard.
slots: [task, context, requirements, constraints, acceptance_criteria]
example_triggers:
  - finish the branch
  - wrap up this feature
  - complete the development branch
  - done with this feature
  - ready to merge
  - finalize this branch
---
## Feature Completed
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

**Do these steps in order. Do not present merge options before tests pass.**

**Step 1: Verify tests pass**
```bash
cargo test    # or npm test / pytest / go test ./...
```
If any test fails: STOP. Report the failures and fix them first. Cannot proceed until all tests pass.

**Step 2: Determine base branch**
```bash
git merge-base HEAD main 2>/dev/null || git merge-base HEAD master 2>/dev/null
```

**Step 3: Present exactly these 4 options** (no more, no fewer, no extra explanation)
```
Implementation complete. What would you like to do?

1. Merge back to <base-branch> locally
2. Push and create a Pull Request
3. Keep the branch as-is (I'll handle it later)
4. Discard this work

Which option?
```

**Step 4: Execute the chosen option**

Option 1 — merge locally:
```bash
git checkout <base-branch>
git pull
git merge <feature-branch>
# Run tests again to verify merged result
git branch -d <feature-branch>
```

Option 2 — push and create PR:
```bash
git push -u origin <feature-branch>
gh pr create --title "<title>" --body "$(cat <<'EOF'
## Summary
- <bullet>

## Test Plan
- [ ] <verification step>
EOF
)"
```

Option 3 — keep as-is: report branch name and worktree path. Do nothing else.

Option 4 — discard: require the user to type "discard" before proceeding, then:
```bash
git checkout <base-branch>
git branch -D <feature-branch>
```

**Step 5: Clean up worktree**
For Options 1, 2, 4: check if in a worktree and remove it:
```bash
git worktree list | grep $(git branch --show-current)
git worktree remove <worktree-path>
```
For Option 3: keep the worktree.
