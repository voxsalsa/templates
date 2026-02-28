---
id: pr_test_coverage_v1
name: PR Test Coverage
description: Analyze test coverage for new or changed code — checks behavioral coverage, edge cases, error paths, and whether tests would catch real regressions.
slots: [task, context, requirements, constraints, acceptance_criteria]
example_triggers:
  - check test coverage
  - review my tests
  - are tests sufficient
  - test analysis
  - coverage review
  - missing tests
---
## What Was Changed
{{task}}

## Files / PR / Commit Range
{{context}}

## Functionality It Should Test
{{requirements}}

## Constraints
{{constraints}}

## Done When
{{acceptance_criteria}}

---

Analyze whether the tests accompanying recent code changes provide adequate coverage. Prioritize preventing real bugs over academic completeness.

**Step 1: Understand the changes**
Read the modified production code. Identify:
- New behaviors and code paths introduced
- Changed behaviors (what was there before, what changed)
- Error conditions the code handles
- Boundary conditions and edge cases

**Step 2: Review the tests**
Read the accompanying tests. For each new/changed behavior, check:
- Is the happy path tested?
- Are error conditions tested (not just that an error occurs, but the right error)?
- Are boundary conditions covered?
- Do tests verify behavior or implementation details?
  - Good: tests what the code *does* (outputs, side effects, state changes)
  - Bad: tests *how* the code does it (internal method calls, private state)

**Step 3: Identify critical gaps**
Rate each gap 1-10 by criticality:
- **9-10**: Untested path that could cause data loss, security issues, or crashes in production
- **7-8**: Untested business logic that would cause user-facing errors
- **5-6**: Untested edge case that would cause confusion or minor failures
- **3-4**: Nice-to-have coverage
- **1-2**: Optional, low value

Only report gaps scoring 5 or above.

**Step 4: Check test quality**
Flag tests that:
- Pass even when the tested behavior is broken (tests mock behavior instead of real behavior)
- Won't catch future regressions because they test implementation, not behavior
- Missing negative cases (what happens when input is invalid, empty, or out of range)

**Step 5: Report**
List gaps by priority. For each, describe: what's missing, why it matters, and a minimal test case that would cover it.
