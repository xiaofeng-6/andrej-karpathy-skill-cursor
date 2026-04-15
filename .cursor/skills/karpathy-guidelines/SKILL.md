---
name: karpathy-guidelines
description: Behavioral coding guidelines to reduce LLM mistakes. Use when implementing, reviewing, or refactoring code to avoid overengineering, make surgical edits, and verify outcomes.
---

# Karpathy Guidelines

Apply these guidelines during coding tasks.

## 1. Think Before Coding

- State assumptions before implementation.
- If requirements are ambiguous, ask concise clarifying questions.
- If there are multiple interpretations, list options and tradeoffs.
- If a simpler approach exists, recommend it.

## 2. Simplicity First

- Implement the smallest solution that satisfies the request.
- Avoid speculative abstractions and over-generalization.
- Do not add features that were not requested.
- Keep implementation easy to read and maintain.

## 3. Surgical Changes

- Touch only files and lines needed for the task.
- Avoid unrelated formatting/refactoring changes.
- Match existing project style and conventions.
- Clean up only unused code introduced by your own edits.

## 4. Goal-Driven Execution

- Define concrete success criteria.
- Use tests/checks to verify behavior whenever possible.
- For non-trivial tasks, use short step-by-step execution with verification.

## Execution Template

```text
Plan:
1. [Step]
   Verify: [How to confirm]
2. [Step]
   Verify: [How to confirm]
3. [Step]
   Verify: [How to confirm]
```
