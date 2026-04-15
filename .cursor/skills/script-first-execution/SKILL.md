---
name: script-first-execution
description: Execute repetitive or structured tasks via scripts with verification and rollback safety. Use when batch edits, data transforms, or repeated file operations are needed.
---

# Script-First Execution

## When to use

- Repetitive edits across many files
- Structured data migration or transformation
- Tasks where manual edits are error-prone

## Workflow

1. Define exact input, output, and success criteria.
2. Create a small script for deterministic changes.
3. Run on a small sample first (dry run or subset).
4. Verify output against expected criteria.
5. Run full scope and re-verify.

## Safety checks

- Keep the script idempotent when possible.
- Log changed files/records for traceability.
- Avoid destructive operations without explicit approval.
- Keep a rollback path before full execution.

## Output template

```text
Task:
- Input:
- Output:
- Success criteria:

Execution:
- Dry run result:
- Full run result:
- Verification result:

Rollback:
- Condition:
- Steps:
```

## Guardrails

- Prefer simple scripts over complex frameworks.
- Do not continue if dry run already mismatches expectation.
- If assumptions are unclear, ask before full run.
