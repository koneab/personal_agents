# personal_agents

My own personal set of GitHub Copilot agents, currently focused on development and implementation for **Java (Spring Boot)**, **React** and **React Native** (plus Angular).

## Agents

Defined in [.github/agents/](.github/agents/).

| Agent | Purpose |
| --- | --- |
| `Dev` | Implements, refactors, writes tests for and reviews code. Loads a coding-rules profile, stays inside declared paths, verifies build and lint only. |
| `Architect` | Read-only review of architecture decisions, ADRs and design proposals. Returns approve / approve-with-conditions / reject. |
| `PR Reviewer` | Reviews a GitHub PR or GitLab MR via `gh` / `glab`. Posts comments only after explicit approval. |
| `planner` | Produces an implementation plan without editing code. |
| `implementer` | Implements an approved plan with minimal, well-tested changes. |
| `reviewer` | Read-only review for correctness, security and rule adherence. |

Default workflow: `planner` → `implementer` → `reviewer`.

### Invoking `Dev`

```
profile=<profile-name> paths=<comma-separated globs> task=<description>
```

Example: `profile=java-spring-boot paths=src/main/java/** task=add pagination to the orders endpoint`

## Coding-rules profiles

Stack-specific rules live in [.core/coding-rules/](.core/coding-rules/). Pass the file name (without `.coding-rules.md`) as `profile=`.

- `java-spring-boot`
- `typescript-react`
- `typescript-react-native`
- `typescript-angular`

To add a stack, copy [_profile-tmpl.md](.core/coding-rules/_profile-tmpl.md).

## Layout

| Folder | Content |
| --- | --- |
| [.github/agents/](.github/agents/) | Custom agents (`*.agent.md`) |
| [.github/skills/](.github/skills/) | Reusable skills (`<name>/SKILL.md`) |
| [.github/rules/](.github/rules/) | Scoped instructions (`*.instructions.md`, matched by `applyTo`): Java, Spring, JPA, Maven, testing |
| [.github/guardrails/](.github/guardrails/) | Hard limits every agent must follow (boundaries, protected paths, security) |
| [.github/templates/](.github/templates/) | Templates for feature specs, ADRs and pull requests |
| [.core/tasks/](.core/tasks/) | Step-by-step workflows for the agents |
| [.core/guardrails/](.core/guardrails/) | Per-agent guardrails |
| [.core/checklists/](.core/checklists/) | Definition of done and architecture review checklists |
| [.core/coding-rules/](.core/coding-rules/) | Stack profiles |

Workspace-wide instructions are in [.github/copilot-instructions.md](.github/copilot-instructions.md). Guardrails override all other instructions.
