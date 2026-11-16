---
name: code-review
description: Review code changes for correctness, security, readability, and test coverage. Use when asked to review a diff, PR, or set of changed files.
---

# Code Review

## Checklist
1. **Correctness** - logic errors, edge cases, error handling at system boundaries.
2. **Security** - input validation, secrets, injection, authz (see `.github/guardrails/security.md`).
3. **Tests** - new behavior is covered; tests are deterministic.
4. **Design** - no unrequested scope, no needless abstraction, consistent with existing patterns.
5. **Readability** - clear names; comments only where code can't explain itself.

## Output
Group findings by severity (blocker, major, minor, nit) with file/line and a concrete fix.
