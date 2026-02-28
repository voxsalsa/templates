---
id: systematic_debug_v1
name: Systematic Debug
description: Investigate a bug by finding root cause before attempting any fix — four phases: root cause investigation, pattern analysis, hypothesis testing, targeted fix.
slots: [task, context, requirements, constraints, acceptance_criteria]
example_triggers:
  - systematically debug
  - investigate this bug
  - find the root cause
  - why is this crashing
  - track down the error
  - debug properly
---
## Symptom
{{task}}

## Technical Context (files, errors, stack traces)
{{context}}

## Background (when it started, what changed)
{{requirements}}

## Constraints
{{constraints}}

## Done When
{{acceptance_criteria}}

---

**Iron Law: NO fixes without completing Phase 1 first.**

Random fixes waste time and create new bugs. Complete each phase before proceeding to the next. This applies especially under time pressure — systematic debugging is faster than guess-and-check thrashing.

**Phase 1: Root cause investigation**
Do ALL of these BEFORE proposing any fix:
- Read all error messages and stack traces completely — do not skip past warnings
- Reproduce the issue consistently — what are the exact steps that trigger it every time?
- Check recent changes: `git diff`, recent commits, new dependencies, config changes
- If the system has multiple components: add diagnostic logging at EVERY component boundary first. Run once to see WHERE it breaks. Then investigate that specific component.
- Trace data flow backward: where does the bad value originate? What called this with the bad value? Keep tracing up until you find the source.

**Phase 2: Pattern analysis**
- Find working examples of similar code in the same codebase
- List every difference between working and broken, however small — do not assume "that can't matter"
- Understand what dependencies, config, or environment the working version relies on that the broken one doesn't

**Phase 3: Hypothesis and testing**
- State the root cause hypothesis explicitly: "I think X is the root cause because Y"
- Make the smallest possible change to test it — one variable at a time
- Did it work? Yes → Phase 4. No → form a new hypothesis. Do NOT stack more fixes on top.

**Phase 4: Implementation**
- Write a failing test that reproduces the bug (TDD — write the test first, watch it fail)
- Implement the single fix that addresses the root cause — nothing else
- Verify: test passes, no other tests broken, original symptom is gone

**If 3+ fixes have failed:** STOP. This indicates an architectural problem, not a symptom to patch. Question the fundamental approach with your partner before attempting more fixes.

**Red flags — stop and return to Phase 1:**
- "Quick fix for now, investigate later"
- "Just try changing X and see if it works"
- "It's probably X, let me fix that"
- Proposing a fix before you can explain exactly why the bug occurs
- "One more fix attempt" after already trying two
