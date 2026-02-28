---
id: tdd_implement_v1
name: TDD Implement
description: Implement a feature or fix using strict test-driven development — write one failing test, watch it fail, write minimal code to pass, repeat for each behavior.
slots: [task, context, requirements, constraints, acceptance_criteria]
example_triggers:
  - implement with TDD
  - write tests first then implement
  - TDD for
  - test-driven implementation
  - red green refactor
  - write failing test first
---
## What to Build
{{task}}

## Relevant Files / Modules
{{context}}

## Details
{{requirements}}

## Constraints
{{constraints}}

## Done When
{{acceptance_criteria}}

---

**Iron Law: NO production code without a failing test first.**

If you wrote code before the test — delete it. Start over. Do not keep it as "reference". Delete means delete. Implement fresh from the tests.

**Violating the letter of these rules violates the spirit.**

**Red-Green-Refactor cycle — repeat for every behavior:**

**RED — Write one failing test**
- One behavior per test, clear name that describes what it verifies
- Test real behavior (no mocks unless the dependency is truly external)
- Name the test after what it verifies, not what calls it

**Verify RED — watch it fail (MANDATORY, never skip)**
Run the test command. Confirm:
- Test fails (not errors out due to a typo or missing import)
- Failure message matches the expected missing feature
- It fails because the feature is missing, not for any other reason

If the test passes immediately: you are testing existing behavior. Fix the test.
If the test errors out: fix the error, re-run until it fails correctly.

**GREEN — Write minimal code to pass**
Write the simplest code that makes the test pass. Nothing more. Do not add features, refactor other code, or "improve" beyond what the test requires.

**Verify GREEN — watch all tests pass (MANDATORY)**
Run the full test suite. Confirm:
- Target test passes
- All other tests still pass
- No errors or warnings in output

If the target test fails: fix code, not the test.
If other tests fail: fix them now.

**REFACTOR — clean up (optional)**
Remove duplication, improve names, extract helpers — only after green. Do not add new behavior. Verify tests stay green after every change.

**Commit** after each complete RED-GREEN-REFACTOR cycle.

**Repeat** for the next behavior.

**Verification checklist before marking done:**
- [ ] Every new function/method has a test
- [ ] Watched each test fail before implementing
- [ ] Each test failed for the expected reason (feature missing, not a typo)
- [ ] Wrote minimal code to pass each test
- [ ] All tests pass
- [ ] No errors or warnings in output
- [ ] Tests use real code (mocks only if unavoidable)
