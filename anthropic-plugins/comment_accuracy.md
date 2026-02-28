---
id: pr_comment_accuracy_v1
name: Comment Accuracy
description: Verify code comments and documentation are factually accurate, complete, and provide lasting value — flags comment rot, misleading docs, and redundant noise.
slots: [task, context, requirements, constraints, acceptance_criteria]
example_triggers:
  - review my comments
  - check documentation accuracy
  - verify comments
  - comment review
  - docs accuracy
  - check my docstrings
---
## What Was Documented
{{task}}

## Files to Review
{{context}}

## Documentation Standards
{{requirements}}

## Constraints
{{constraints}}

## Done When
{{acceptance_criteria}}

---

Review code comments and documentation for accuracy, completeness, and long-term maintainability. Every comment should earn its place by providing clear, lasting value.

**Step 1: Check factual accuracy**
For each comment, verify against the actual code:
- Do documented parameters match the function signature?
- Do documented return types match what the code actually returns?
- Do described behaviors match what the code actually does?
- Do referenced variables, functions, or constants exist?
- Are described algorithms correct?

**Step 2: Check completeness**
For each documented function/type/module, ask:
- Are critical assumptions documented (e.g., "caller must hold the lock", "input must be sorted")?
- Are significant side effects mentioned?
- Are error conditions and what triggers them explained?
- For non-obvious algorithms, is the approach explained (not just what, but why)?

**Step 3: Assess long-term value**
Flag comments that:
- Explain *what* the code does when the code is already self-explanatory (redundant noise)
- Will become false as the code evolves (obsolescence risk)
- Reference things that no longer exist
- Use vague or ambiguous language that could confuse a future maintainer

Preserve and highlight comments that:
- Explain *why* a decision was made (context future maintainers won't have)
- Warn about non-obvious gotchas
- Document constraints imposed by external systems

**Step 4: Report**
Organize into four sections:
- **Critical issues** — factually incorrect comments (must fix)
- **Improvements** — completeness gaps and clarity issues (should fix)
- **Remove** — low-value or redundant comments (consider removing)
- **Good examples** — comments that set the right standard
