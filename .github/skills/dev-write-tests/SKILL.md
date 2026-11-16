---
name: dev-write-tests
description: Use when writing or updating automated unit or integration tests for new or changed code, covering happy paths, edge cases and failures per the loaded profile's testing conventions. Tests are written, never executed.
---

# Dev Write Tests

Rules: [dev guardrails](../../../.core/guardrails/dev.guardrails.md) and [dev security guardrails](../../../.core/guardrails/dev-security.guardrails.md).

## Steps
1. Read the profile's testing conventions and reuse the existing test framework, layout and naming.
2. Cover the happy path, edge cases and failure modes of the changed behaviour.
3. For bug fixes, write a test that reproduces the bug.
4. Keep tests independent and deterministic, with no real network access or secrets.
5. Do not run the tests; report them as written but not executed.
