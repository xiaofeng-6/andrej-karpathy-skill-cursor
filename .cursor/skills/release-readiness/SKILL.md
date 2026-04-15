---
name: release-readiness
description: Prepare and validate release readiness with checks for tests, build, risk, and rollback. Use when the user asks for release prep, deployment checklist, or merge readiness.
---

# Release Readiness

## Goal

Decide whether a change is safe to release, and provide clear go/no-go reasoning.

## Checklist

- Scope is clear: what changed and why
- Verification is complete: tests, lint, build, smoke checks
- Risk is identified: user impact, data impact, dependency impact
- Rollback path exists and is practical
- Release notes or change summary is ready

## Execution steps

1. Summarize release scope.
2. Run or verify quality gates (tests/lint/build).
3. Assess operational risks and failure modes.
4. Define rollback/mitigation actions.
5. Produce final release verdict.

## Output template

```text
Release Verdict: GO | NO-GO | GO WITH MITIGATIONS

Scope:
- ...

Verification:
- Tests: pass/fail/unknown
- Build: pass/fail/unknown
- Lint: pass/fail/unknown
- Smoke checks: pass/fail/unknown

Risks:
- [Risk] Impact / likelihood / mitigation

Rollback:
- Trigger:
- Steps:
- Owner:
```

## Guardrails

- Never hide unknowns; mark them explicitly.
- If critical checks are missing, default to NO-GO.
- Keep recommendations concrete and minimal.
