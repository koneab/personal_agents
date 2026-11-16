---
name: dev-implement-feature
description: Use when implementing a feature, fixing a bug, or refactoring code in any language or framework, following the loaded coding-rules profile and staying inside the task's declared paths.
---

# Dev Implement Feature

Rules: [dev guardrails](../../../.core/guardrails/dev.guardrails.md) and [dev security guardrails](../../../.core/guardrails/dev-security.guardrails.md).

## Steps
1. Read the loaded profile's layout, naming, error-handling and forbidden-pattern sections.
2. Read the existing in-scope code and follow its conventions.
3. Make the smallest focused edits that satisfy the task; flag scope changes instead of making them.
4. Do not touch the profile's protected config files unless the task asks for it.
5. Run the profile build command, then the lint command, and fix in-scope issues.
