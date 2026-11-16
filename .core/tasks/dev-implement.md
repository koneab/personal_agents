# Task: Dev Implement

Workflow for the `Dev` agent. Follow the steps in order.

1. **Validate arguments**: `profile`, `paths` and `task` must all be present. If any is missing, ask the user and stop.
2. **Load profile**: read `.core/coding-rules/<profile>.coding-rules.md`. If missing, stop and report its exact path. Never guess a stack.
3. **Confirm scope**: restate the task and the in-scope paths, then ask the user to confirm before any edit.
4. **Plan**: break the task into steps with the todo tool.
5. **Implement**: edit only inside `paths=`, following the profile and the skills relevant to the step (see the agent file).
6. **Verify**: run the profile build command, then the lint command; fix in-scope issues and rerun. Do not run tests.
7. **Checklist**: go through `.core/checklists/dev-definition-of-done.checklist.md`.
8. **Report**: output in the format defined in `.github/agents/dev.agent.md`.

Rules for every step: [dev guardrails](../guardrails/dev.guardrails.md) and [dev security guardrails](../guardrails/dev-security.guardrails.md).
