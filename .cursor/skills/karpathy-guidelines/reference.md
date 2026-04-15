# Karpathy Guidelines Reference

This document captures the full intent behind the Karpathy-inspired coding behavior framework and is designed to preserve the original philosophy for Cursor usage.

## Why this exists

Common LLM coding failure modes:

- Wrong assumptions made silently
- Confusion hidden instead of surfaced
- Tradeoffs not presented
- Overcomplicated designs and unnecessary abstractions
- Unrelated edits outside request scope
- Weak or unverifiable completion criteria

The framework addresses these failures with four principles that should be applied together.

## The Four Principles

## 1) Think Before Coding

**Intent:** Do not guess. Surface uncertainty. Make decision points explicit.

Behavior requirements:

- State assumptions explicitly before coding.
- If requirements are ambiguous, ask concise clarifying questions.
- If multiple interpretations exist, present options instead of silently choosing.
- If a simpler approach exists, say so and explain tradeoffs.
- If context is insufficient, stop and request missing information.

Anti-patterns:

- Silent interpretation of ambiguous user requests
- Proceeding despite confusion
- Acting as if hidden assumptions are facts

## 2) Simplicity First

**Intent:** Solve today's problem with minimum code and complexity.

Behavior requirements:

- Build the smallest solution that satisfies the request.
- Do not add features that were not requested.
- Do not introduce abstractions for single-use code.
- Avoid speculative "future flexibility" and unnecessary configurability.
- Keep error handling practical; avoid impossible-scenario branching.
- If implementation feels bloated, simplify before finalizing.

Anti-patterns:

- Strategy/factory/plugin systems for simple one-off tasks
- Preemptive generalization "for future use"
- Large architecture changes for small behavior requests

## 3) Surgical Changes

**Intent:** Touch only what is necessary. Avoid collateral changes.

Behavior requirements:

- Change only files/lines directly related to the request.
- Do not refactor adjacent unrelated areas.
- Do not reformat unrelated code.
- Match existing code style unless explicitly asked to change style.
- If your own change creates dead imports/variables/functions, clean them.
- Do not remove pre-existing dead code unless asked.

Core test:

- Every changed line should trace directly to the user request.

Anti-patterns:

- "Drive-by refactor" while fixing a bug
- Reformatting entire files to include a small fix
- Adding optional improvements not requested

## 4) Goal-Driven Execution

**Intent:** Replace vague completion with verifiable outcomes.

Behavior requirements:

- Translate vague requests into concrete success criteria.
- For bug fixes and behavior changes, prefer test-first verification.
- Verify with tests, build checks, and direct behavior checks.
- For multi-step tasks, define checkpoints with explicit verification.

Template:

```text
1. [Step] -> verify: [check]
2. [Step] -> verify: [check]
3. [Step] -> verify: [check]
```

Anti-patterns:

- "I fixed it" without reproducible verification
- Long implementation before writing any check
- All-at-once changes with no incremental validation

## Principle-to-Problem mapping

| Principle | Primary failure it prevents |
|---|---|
| Think Before Coding | Hidden assumptions and silent misinterpretation |
| Simplicity First | Overengineering and bloated abstractions |
| Surgical Changes | Unrelated edits and scope creep |
| Goal-Driven Execution | Unverifiable "done" states |

## Judgment boundaries (Use Boundaries)

These guidelines are strict for non-trivial work, but not intended to slow obvious one-line fixes.

Apply full rigor when:

- Task is ambiguous
- Code path is critical or high-risk
- Change spans multiple files/components
- Bug reproduction is unclear
- Release risk is non-trivial

Apply lightweight mode when:

- Obvious typo/text fix
- Small deterministic one-line change
- No architectural or behavior uncertainty

Even in lightweight mode:

- Keep change surgical
- Avoid unrequested features
- Keep output honest about what was and was not verified

## Completion criteria (How to know it works)

The framework is working when you consistently observe:

- Fewer unnecessary lines in diffs
- Fewer rewrites caused by overcomplication
- Clarifying questions happen before implementation
- Cleaner, minimal PRs without drive-by edits
- Claims are backed by tests/checks instead of assumptions

## Decision checklist

Use this quick checklist before sending final output:

- Did I state assumptions?
- Did I avoid silent interpretation?
- Is this the simplest solution that meets the ask?
- Are all changed lines directly traceable to request?
- Did I verify with concrete checks?
- Did I clearly report unknowns, risks, or testing gaps?

## Combining with project-specific rules

This framework is designed to be combined with project-level conventions, such as:

- language/style requirements
- test and CI policies
- architecture boundaries
- security/compliance constraints

When project rules conflict with personal preference, follow project rules.

## Relationship to process skills

This document defines the doctrine. For execution workflows:

- `../code-review/SKILL.md` for structured review and risk findings
- `../release-readiness/SKILL.md` for go/no-go and rollback planning
- `../script-first-execution/SKILL.md` for deterministic automation tasks

## Non-goals

This framework does not try to:

- force heavy process on trivial edits
- replace project-specific technical standards
- prescribe one architecture for every context

It exists to improve reliability, reduce avoidable mistakes, and make outcomes verifiable.
