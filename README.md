# VoxSalsa Templates

A collection of structured prompt templates for [VoxSalsa](https://github.com/voxsalsa/app) — a voice-to-structured-prompt desktop app. Each template captures a complete workflow as a prompt, invoked by voice and filled with context extracted from what you say.

## How templates work

When you press push-to-talk and speak, VoxSalsa:
1. Transcribes your voice
2. Routes to the best matching template based on what you said
3. Extracts context (task, files, requirements, constraints, acceptance criteria) from the transcript
4. Fills the template slots and copies the result to your clipboard

Templates live in `~/.config/voxsalsa/templates/` and can be downloaded from this repo via the setup wizard.

---

## `superpowers/` — Workflow discipline templates

Templates based on the [obra/superpowers](https://github.com/obra/superpowers) skill library — a collection of process disciplines for AI-assisted development. Each template embeds the complete workflow steps from its corresponding skill, so invoking it puts you and your AI assistant on the same structured process.

| Template | What it does |
|----------|-------------|
| `brainstorm.md` | Design a feature before touching code — explores requirements, proposes approaches, gets approval |
| `write_plan.md` | Create a detailed implementation plan with exact paths, complete code, and TDD steps |
| `execute_plan.md` | Execute a plan file in batches of 3 tasks with review between batches |
| `subagent_dev.md` | Execute a plan with fresh subagents per task + spec and code quality review after each |
| `tdd_implement.md` | Implement with strict TDD — write failing test first, watch it fail, write minimal code |
| `verify_complete.md` | Verify work is actually done — no completion claims without fresh verification evidence |
| `code_review_request.md` | Request a code review with commit range and act on findings by severity |
| `code_review_receive.md` | Process review feedback with technical rigor — verify before implementing, push back if wrong |
| `systematic_debug.md` | Debug by finding root cause first — four phases before any fix is attempted |
| `parallel_fix.md` | Fix multiple independent problems simultaneously with one agent per domain |
| `finish_branch.md` | Complete a branch — verify tests, then choose from exactly 4 options |
| `worktree_setup.md` | Set up an isolated git worktree with safety checks and baseline verification |
| `write_skill.md` | Document a reusable technique as a skill using TDD for documentation |

**Source:** [obra/superpowers](https://github.com/obra/superpowers)

---

## `anthropic-plugins/` — PR review templates

Templates based on the [pr-review-toolkit](https://github.com/anthropics/claude-code/tree/main/plugins/pr-review-toolkit) plugin from Anthropic's official Claude Code plugin collection. Each template embeds the review methodology of one of the six specialized agents in that toolkit.

| Template | What it does |
|----------|-------------|
| `code_review.md` | Review code for guideline violations and bugs — confidence-filtered (80%+ threshold) |
| `test_coverage.md` | Analyze test coverage — behavioral gaps, edge cases, missing error path tests |
| `silent_failures.md` | Hunt for swallowed exceptions, empty catch blocks, and inadequate error handling |
| `comment_accuracy.md` | Verify comments are factually accurate, complete, and provide lasting value |
| `type_design.md` | Rate type designs on encapsulation, invariant expression, usefulness, enforcement (1-10 each) |
| `simplify_code.md` | Simplify recently modified code for clarity — never changes behavior |

**Source:** [anthropics/claude-code — pr-review-toolkit](https://github.com/anthropics/claude-code/tree/main/plugins/pr-review-toolkit)

---

## Contributing

Templates use YAML frontmatter with these fields:

```yaml
---
id: unique_id_v1
name: Human-readable name
description: One sentence — what it does and when to use it
slots: [task, context, requirements, constraints, acceptance_criteria]
example_triggers:
  - phrase that should route here
  - another phrase
---
```

Only these slot names are filled by the engine: `task`, `context`, `requirements`, `constraints`, `acceptance_criteria`.
