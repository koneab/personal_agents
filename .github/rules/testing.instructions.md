---
description: Rules for test files.
applyTo: '**/*.{test,spec}.*,**/tests/**,**/test_*.py'
---

- One behavior per test; name tests after the behavior.
- Use arrange / act / assert structure.
- No shared mutable state between tests.
- Mock only external boundaries (network, filesystem, clock).
