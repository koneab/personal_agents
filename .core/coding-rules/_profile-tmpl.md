# Coding-Rules Profile: <profile-name>

Template for `<profile-name>.coding-rules.md`. Fill every section; write "None" where nothing applies. This is the only place technology-specific rules live.

## Versions and framework
<Language, framework and tool versions the code targets.>

## Project layout
<Directory structure and the responsibility of each layer.>

## Naming
<Conventions for files, types, functions, variables and tests.>

## Error handling
<How errors are raised, translated and reported at boundaries.>

## Testing conventions
<Framework, location, naming and structure of tests. Tests are written, never run by the agent.>

## Build command
<Exactly one command, as it must be invoked.>

## Lint command
<Exactly one command, as it must be invoked.>

## Prerequisites
<What must already exist before build and lint can run. If missing, the agent reports it and stops.>

## Additional denied paths
<Paths denied in addition to the fixed deny list in the dev guardrails.>

## Forbidden commands
<Commands the agent must never run, in addition to the dev guardrails.>

## Protected config files
<Files the agent edits only if inside `paths=` and explicitly requested by the task.>

## Forbidden patterns
<Code constructs that must not be written.>

## Architecture rules
<Optional. Used by the `Architect` agent: allowed dependency directions, layer and module boundaries, approved technologies and patterns, data-ownership and integration rules, and decisions that always require an ADR.>

## Stack-specific security rules
<Extra security rules for the stack. Stricter than the dev security guardrails; take precedence.>
