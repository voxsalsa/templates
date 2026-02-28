---
id: code_review_receive_v1
name: Code Review Receive
description: Process incoming code review feedback with technical rigor — verify each item against the codebase, push back if wrong, implement one item at a time.
slots: [task, context, requirements, constraints, acceptance_criteria]
example_triggers:
  - I got code review feedback
  - act on review feedback
  - code review says
  - process review comments
  - review feedback to address
  - received review feedback
---
## Feedback Received
{{task}}

## Codebase Context
{{context}}

## Additional Items
{{requirements}}

## Constraints
{{constraints}}

## Done When
{{acceptance_criteria}}

---

**Core principle: Technical correctness over social comfort.**

**Never:**
- "You're absolutely right!" — performative agreement, not verification
- "Great point!" — same problem
- "Let me implement that now" — before checking if it's actually correct

**Response pattern — for EVERY feedback item:**

**1. READ** the complete feedback before reacting to any of it.

**2. UNDERSTAND** — restate each requirement in your own words.
If any item is unclear: STOP. Ask for clarification on ALL unclear items before implementing anything. Items may be related — partial understanding leads to wrong implementation.

**3. VERIFY** — check the actual codebase. Does this feedback apply here? Is the claim accurate? Would this change break existing functionality?

**4. EVALUATE** — is this technically sound for THIS codebase?
- Does the reviewer have full context?
- Is there a reason the current implementation exists this way?
- Does it conflict with prior architectural decisions?
- Is this feature actually used (YAGNI: if unused, consider removing instead)?

**5. RESPOND:**
- If correct: state what will change, then implement it
- If wrong: push back with technical reasoning, reference working tests or code, ask specific questions

**6. IMPLEMENT** — one item at a time. Test each fix before moving to the next. Verify no regressions.

**Implementation order for multi-item feedback:**
1. Clarify all unclear items first
2. Blocking issues (crashes, security)
3. Simple fixes (typos, imports)
4. Complex fixes (refactoring, logic)

**Acknowledging correct feedback:**
```
Fixed. [Brief description of what changed.]
```
No thanks, no enthusiasm. Just the fix.

**If you pushed back and were wrong:**
```
Verified this and you're correct. [Reason my initial read was wrong.] Fixing.
```
State it factually and move on.
