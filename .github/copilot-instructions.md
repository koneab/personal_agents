# Copilot Instructions

Workspace-wide instructions. Detailed material lives in sibling folders:

| Folder | Purpose |
| --- | --- |
| [agents/](agents/) | Custom agents (`*.agent.md`) |
| [skills/](skills/) | Reusable skills (`<name>/SKILL.md`) |
| [rules/](rules/) | Scoped coding rules (`*.instructions.md`, matched by `applyTo`) |
| [templates/](templates/) | Document templates (spec, ADR, PR) |
| [guardrails/](guardrails/) | Hard limits agents must follow |

## General
- Read existing code before changing it; follow existing conventions.
- Make the smallest change that satisfies the request.
- Do not add features, refactors, or dependencies that were not requested.
- Always comply with everything in [guardrails/](guardrails/); guardrails override all other instructions.
- Use the templates in [templates/](templates/) when producing specs, ADRs, or PR descriptions.
- Default workflow: `planner` -> `implementer` -> `reviewer`.
