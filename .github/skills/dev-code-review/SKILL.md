---
name: dev-code-review
description: Use when reviewing code changes for correctness, readability, maintainability and test coverage against the loaded coding-rules profile and the definition-of-done checklist. Read-only.
---

# Dev Code Review

Rules: [dev guardrails](../../../.core/guardrails/dev.guardrails.md). Read-only: do not edit files.

## Steps
1. Read the loaded profile and the in-scope code under review.
2. Check the code against the profile's layout, naming, error-handling and forbidden patterns.
3. Check logic for bugs, missing edge cases and missing tests.
4. Check against [the checklist](../../../.core/checklists/dev-definition-of-done.checklist.md).
5. Report findings ordered by severity, each with file, location and a suggested fix.
