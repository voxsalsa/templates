---
id: pr_type_design_v1
name: Type Design
description: Analyze type designs for invariant strength, encapsulation, and enforcement — rates encapsulation, invariant expression, usefulness, and enforcement each 1-10.
slots: [task, context, requirements, constraints, acceptance_criteria]
example_triggers:
  - review type design
  - check my types
  - type analysis
  - analyze this type
  - review my data model
  - check my struct design
---
## Type(s) to Analyze
{{task}}

## Codebase Context
{{context}}

## Requirements
{{requirements}}

## Constraints
{{constraints}}

## Done When
{{acceptance_criteria}}

---

Analyze the design quality of types (structs, classes, enums, interfaces) for invariant strength, encapsulation, and practical usefulness.

**Core philosophy:** Prefer compile-time guarantees over runtime checks. Make illegal states unrepresentable. Balance safety against implementation cost.

**Step 1: Identify invariants**
For each type, determine:
- What consistency requirements must always hold across the fields?
- What are the valid states and transitions?
- What relationships between fields are always required?
- What business logic rules are embedded in the type?

**Step 2: Rate on four dimensions (1-10 each)**

**Encapsulation (1-10)**
Can the type's internal invariants be violated from outside? Can callers put the type into an invalid state?
- 9-10: All mutations go through methods that enforce invariants; fields are private/opaque
- 5-8: Partial encapsulation; some invariants externally enforceable
- 1-4: Fields publicly mutable; invariants purely by convention

**Invariant expression (1-10)**
How clearly does the type structure communicate its constraints?
- 9-10: Invalid states are unrepresentable at the type level (newtype wrappers, enums, option types)
- 5-8: Some constraints expressed in types; others documented
- 1-4: Invariants only in documentation or comments; nothing enforced by structure

**Usefulness (1-10)**
Do these invariants prevent real bugs? Do they align with actual business requirements?
- 9-10: Invariants directly prevent meaningful runtime errors
- 5-8: Invariants provide some safety benefit
- 1-4: Invariants are theoretical; violations would be caught elsewhere anyway

**Enforcement (1-10)**
Are invariants protected at construction and at every mutation point?
- 9-10: Smart constructors, all mutation through validated methods
- 5-8: Construction validated; some mutation paths bypass checks
- 1-4: No enforcement; invariants assumed by callers

**Step 3: Flag anti-patterns**
- Anemic models (data bags with no behavior that enforces invariants)
- Exposed mutable fields that allow bypassing invariants
- Invariants documented only in comments, not enforced
- Types that represent multiple distinct concepts (should be split)

**Step 4: Report**
For each type: the four ratings with brief justification, identified invariants, and specific improvement suggestions with their benefit/cost trade-off.
