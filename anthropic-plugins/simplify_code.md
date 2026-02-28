---
id: pr_simplify_code_v1
name: Simplify Code
description: Simplify recently written or modified code for clarity, consistency, and reduced complexity — preserves all functionality, focuses only on recently changed sections.
slots: [task, context, requirements, constraints, acceptance_criteria]
example_triggers:
  - simplify this code
  - clean up my code
  - reduce complexity
  - improve readability
  - simplify implementation
  - polish before PR
---
## What to Simplify
{{task}}

## Files / Commit Range
{{context}}

## Project Style Rules
{{requirements}}

## Constraints
{{constraints}}

## Done When
{{acceptance_criteria}}

---

Simplify recently modified code for clarity, consistency, and maintainability. **Never change what the code does — only how it does it.**

**Scope:** Focus only on recently modified sections unless instructed otherwise.

**Step 1: Identify modified sections**
```bash
git diff          # unstaged changes
git diff --staged # staged changes
```

**Step 2: Apply project conventions**
Read CLAUDE.md or equivalent project style guide. Apply:
- Naming conventions (variables, functions, types)
- Preferred constructs (e.g., function keyword vs arrow, explicit return types)
- Module/import patterns
- Any explicit style rules

**Step 3: Reduce unnecessary complexity**
Look for:
- Deeply nested conditions that can be flattened with early returns
- Temporary variables that add no clarity
- Duplicated logic that can be extracted into a named helper
- Overly clever one-liners that sacrifice readability for brevity
- Nested ternary operators (replace with if/else or switch)
- Long functions doing multiple distinct things (split at natural seams)

**Step 4: Improve naming**
- Variable and function names should explain what they represent or do, not how they're implemented
- Boolean names should read as statements: `isValid`, `hasPermission`, `shouldRetry`
- Avoid abbreviations unless they're standard in the domain

**Step 5: Verify functionality is preserved**
Run the test suite before and after any changes:
```bash
cargo test    # or npm test / pytest / go test ./...
```
If any test fails: revert that specific change immediately.

**Step 6: Report**
List the changes made (before/after for each significant simplification) and confirm all tests still pass.
