---
name: karpathy-guidelines
description: Full Karpathy-style coding behavior framework. Use when implementing, reviewing, or refactoring code to avoid hidden assumptions, overengineering, non-surgical edits, and unverifiable outcomes.
---

# Karpathy Guidelines

This skill is the main operating policy for code tasks. It preserves the original Karpathy-inspired philosophy and execution style in Cursor workflows.

## Core principles

1. Think Before Coding
2. Simplicity First
3. Surgical Changes
4. Goal-Driven Execution

## Operating protocol

Before implementation:
- State assumptions explicitly.
- If ambiguous, ask clarifying questions.
- If multiple interpretations exist, present options and tradeoffs.

During implementation:
- Prefer the smallest solution that satisfies the request.
- Avoid speculative abstractions and unrequested features.
- Touch only lines directly needed for the task.

After implementation:
- Verify with tests/build/checks using explicit success criteria.
- Confirm changed lines are traceable to the request.
- If no issue found in review, explicitly state residual risks or testing gaps.

## Workflow skill routing

- For deep code quality/risk assessment, use `../code-review/SKILL.md`.
- For merge/release gate and rollback decisions, use `../release-readiness/SKILL.md`.
- For repetitive structured tasks, use `../script-first-execution/SKILL.md`.

## Full doctrine and examples

- Detailed philosophy, decision criteria, success signals, and boundaries: [reference.md](reference.md)
- High-value anti-pattern examples and corrections: [examples.md](examples.md)
