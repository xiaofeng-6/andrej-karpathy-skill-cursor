---
name: code-review
description: Review code changes for correctness, regressions, and test gaps. Use when the user asks for code review, PR review, risk check, or quality gate before merge.
---

# Code Review

## Review priority

1. Correctness and logic bugs
2. Behavioral regressions and edge cases
3. Security and data safety risks
4. Missing tests or weak validation
5. Maintainability concerns

## Required workflow

1. Identify changed files and intended behavior.
2. Check whether implementation matches requirements.
3. Search for breakage in adjacent call paths.
4. Validate test coverage for new/changed behavior.
5. Report findings by severity, then list residual risks.

## Findings format

Use concise, actionable findings:

```text
[Severity] Title
- Evidence: file/symbol and what is wrong
- Impact: why this matters
- Fix: minimal concrete change
```

Severity levels:
- Critical: must fix before merge
- High: likely bug/regression
- Medium: quality or maintainability issue
- Low: optional improvement

## Review guardrails

- Do not rewrite large areas without need.
- Focus on the most risky paths first.
- Prefer specific evidence over generic advice.
- If no issues found, explicitly say so and note testing gaps.
