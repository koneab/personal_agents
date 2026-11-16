# Task: Architect Review

Workflow for the `Architect` agent. Follow the steps in order.

1. **Validate arguments**: `profile`, `paths` and `decision` must all be present. If any is missing, ask the user and stop.
2. **Load profile**: read `.core/coding-rules/<profile>.coding-rules.md`. If missing, stop and report its exact path. Never guess a stack.
3. **Confirm scope**: restate the decision and the in-scope paths, then ask the user to confirm before reading further.
4. **Plan**: list the review steps with the todo tool.
5. **Gather evidence**: read the decision document and the in-scope code needed to judge it; state each path before reading.
6. **Assess**: apply the `architect-review-decision` skill against the profile and the architect guardrails.
7. **Checklist**: go through `.core/checklists/architect-review.checklist.md`.
8. **Report**: output in the format defined in `.github/agents/architect.agent.md`.

Rules for every step: [architect guardrails](../guardrails/architect.guardrails.md) and [dev security guardrails](../guardrails/dev-security.guardrails.md).
