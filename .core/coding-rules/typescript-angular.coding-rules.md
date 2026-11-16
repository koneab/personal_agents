# Coding-Rules Profile: typescript-angular

## Versions and framework
- TypeScript with Angular, managed with npm. Use the versions already declared in the project; do not change them.
- TypeScript `strict` mode on. Linting with ESLint.

## Project layout
- Feature folders under `src/app/<feature>/` with components, services, models and routes together.
- Standalone components only; no NgModules for new code.
- Shared, reusable code under `src/app/shared/`.

## Naming
- Files `kebab-case` with type suffix: `*.component.ts`, `*.service.ts`, `*.model.ts`, `*.spec.ts`.
- Classes `UpperCamelCase` with matching suffix; members `lowerCamelCase`; observables end with `$`.

## Error handling
- Handle HTTP errors in services or an interceptor; surface user-safe messages only.
- Never swallow errors in subscriptions.

## Testing conventions
- Spec files next to the code under test, named `*.spec.ts`.
- Test components through their rendered output and services with mocked HTTP.
- Tests are written, never run.

## Build command
`npm run build`

## Lint command
`npm run lint`

## Prerequisites
- Dependencies already installed (`node_modules/` present).
- `build` and `lint` scripts already defined in the project.

## Additional denied paths
- `node_modules/`
- `dist/`

## Forbidden commands
- `npm install`
- `npm ci`
- `npm test`
- `npm publish`

## Protected config files
- `package.json` scripts
- Lockfile
- ESLint configuration

## Forbidden patterns
- `any`.
- `bypassSecurityTrust*`.
- Unsanitised `innerHTML`.
- Typed forms replaced by untyped forms.
- Manual subscriptions without cleanup (use `takeUntilDestroyed` or the async pipe).

## Stack-specific security rules
- Rely on Angular's built-in sanitisation; never bypass it.
- Never store tokens in local storage when a safer mechanism is available.
- No secrets in environment files shipped to the browser.
