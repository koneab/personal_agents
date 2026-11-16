---
name: architect-review-decision
description: Use when assessing a major architecture decision, design proposal or ADR for fit, coupling, boundaries, security, operability and reversibility against the loaded coding-rules profile and the architect checklist. Read-only.
---

# Architect Review Decision

Rules: [architect guardrails](../../../.core/guardrails/architect.guardrails.md). Read-only: do not edit files.

## Steps
1. Read the loaded profile and the decision under review.
2. Establish the problem, constraints, chosen option and rejected alternatives; note what is missing.
3. Check the decision against the profile's architecture rules (or the fallback sections named in the guardrails), layout and forbidden patterns.
4. Assess coupling, dependency direction, data ownership, failure modes, security, operability, testability and reversibility.
5. Check against [the checklist](../../../.core/checklists/architect-review.checklist.md).
6. Report findings ordered by severity (blocker, major, minor), each with the rule or evidence, location and a recommended change, then give a verdict.
