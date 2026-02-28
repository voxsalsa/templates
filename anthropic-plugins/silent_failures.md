---
id: pr_silent_failures_v1
name: Silent Failures
description: Hunt for silent failures, empty catch blocks, swallowed exceptions, and inadequate error handling in recently changed code.
slots: [task, context, requirements, constraints, acceptance_criteria]
example_triggers:
  - check error handling
  - find silent failures
  - review catch blocks
  - error handling review
  - find swallowed errors
  - audit exception handling
---
## What Was Changed
{{task}}

## Files / Commit Range
{{context}}

## Expected Error Handling Behavior
{{requirements}}

## Constraints
{{constraints}}

## Done When
{{acceptance_criteria}}

---

Audit recently changed code for places where errors are silently swallowed, inadequately logged, or handled with fallbacks that mask problems.

**Step 1: Find all error handling code**
Locate every:
- try/catch block (or equivalent in Rust: `match`, `.unwrap_or`, `.ok()`, `if let Err`)
- Error callbacks and Promise rejections
- Conditional branches that handle failure cases
- Fallback values and default returns on error

**Step 2: For each error handler, evaluate:**

**Logging quality**
- Is the error logged with appropriate severity?
- Does the log include enough context to debug later (which operation failed, what input triggered it)?
- Is the log reachable — or is it in dead code?

**User/caller feedback**
- Does the caller know something went wrong?
- Is the error message clear and actionable, or generic ("An error occurred")?

**Catch block specificity**
- Does it catch only expected error types, or does a broad catch risk suppressing unrelated errors?

**Fallback appropriateness**
- Is the fallback value genuinely safe, or does it allow the system to continue in a broken state?
- Was this fallback explicitly intended, or is it masking an upstream bug?

**Error propagation**
- Should this error bubble up instead of being caught locally?
- Is the catch at the right level of the call stack?

**Step 3: Severity ratings**
- **CRITICAL**: Empty catch block, or catch that only logs and continues when the operation is essential
- **HIGH**: Silent return of null/undefined/None on error with no log, retry logic that exhausts without notifying the user
- **MEDIUM**: Error logged but at wrong severity, fallback that hides a real problem

**Step 4: Report**
For each finding: severity, file/line location, what error is hidden, user impact, and a concrete fix.
