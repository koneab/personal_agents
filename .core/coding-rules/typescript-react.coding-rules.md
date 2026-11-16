# Coding-Rules Profile: typescript-react

## Versions and framework
- TypeScript with React, managed with npm. Use the versions already declared in the project; do not change them.
- TypeScript `strict` mode on. Linting with ESLint.

## Project layout
- Feature folders under `src/<feature>/` with components, hooks, API clients and types together.
- Shared, reusable code under `src/shared/`.

## Naming
- Components and their files `UpperCamelCase` (`UserCard.tsx`); hooks `useXxx`; other files `kebab-case`.
- Tests `*.test.tsx` or `*.test.ts` next to the code under test.

## Error handling
- Handle API errors in the API client layer; surface user-safe messages only.
- Use error boundaries for rendering failures.
- Never swallow errors in async code.

## Testing conventions
- Test components through rendered output and user-visible behaviour; mock the network.
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
- Unsanitised `dangerouslySetInnerHTML`.
- Secrets in `VITE_*` or `REACT_APP_*` variables.
- Class components for new code.
- Hooks called conditionally.

## Stack-specific security rules
- Rely on React's default escaping; sanitise any HTML before it reaches `dangerouslySetInnerHTML`.
- Anything in a client-exposed environment variable is public; never place secrets there.
- Never store tokens in local storage when a safer mechanism is available.
