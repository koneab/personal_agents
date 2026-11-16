# Coding-Rules Profile: typescript-react-native

## Versions and framework
- TypeScript with React Native, managed with npm. Use the versions already declared in the project; do not change them.
- Follow the existing setup (bare React Native CLI or Expo); do not switch between them or eject.
- TypeScript `strict` mode on. Linting with ESLint.

## Project layout
- Feature folders under `src/<feature>/` with screens, components, hooks, API clients and types together.
- Shared, reusable code under `src/shared/`.
- Navigation setup and route param types under `src/navigation/`.
- Do not edit generated native folders (`ios/`, `android/`) unless the task explicitly requires it.

## Naming
- Components, screens and their files `UpperCamelCase` (`UserCard.tsx`, `ProfileScreen.tsx`); hooks `useXxx`; other files `kebab-case`.
- Platform-specific files use the `.ios.tsx` / `.android.tsx` suffix next to a shared default file.
- Tests `*.test.tsx` or `*.test.ts` next to the code under test.

## Components and styling
- Function components with hooks only.
- Use `StyleSheet.create` for styles; no inline style objects in render paths.
- Use `Platform.select` or platform file suffixes for platform differences; do not branch on platform deep inside components.
- Respect safe areas (`SafeAreaView` / safe-area context) and keyboard avoidance on screens with inputs.
- Add accessibility props (`accessibilityLabel`, `accessibilityRole`) to interactive elements.
- Use `FlatList` / `SectionList` for long lists with a stable `keyExtractor`; never render long lists with `ScrollView` + `map`.
- Memoise (`memo`, `useCallback`, `useMemo`) only for list items and measured hot paths.

## Navigation
- Type route names and params; no untyped `navigate` calls.
- Screens receive params and render; data fetching and side effects live in hooks.

## Error handling
- Handle API errors in the API client layer; surface user-safe messages only.
- Use error boundaries for rendering failures.
- Never swallow errors in async code.
- Handle offline and slow-network states explicitly in user-facing flows.

## Testing conventions
- Test components through rendered output and user-visible behaviour (React Native Testing Library); mock the network and native modules.
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
- `ios/Pods/`
- `android/build/`
- `android/app/build/`

## Forbidden commands
- `npm install`
- `npm ci`
- `npm test`
- `npm publish`
- `pod install`
- `npx react-native run-ios`
- `npx react-native run-android`
- `npx expo prebuild`

## Protected config files
- `package.json` scripts
- Lockfile
- ESLint configuration
- `metro.config.js`
- `babel.config.js`
- `app.json` / `app.config.*`
- Native project files (`Podfile`, `build.gradle`, `Info.plist`, `AndroidManifest.xml`)

## Forbidden patterns
- `any`.
- Class components for new code.
- Hooks called conditionally.
- Web-only APIs (`window`, `document`, `localStorage`, DOM elements).
- Secrets in `EXPO_PUBLIC_*` variables or in bundled source or config.
- Inline functions and style objects as props of list items.
- `console.log` left in committed code.

## Stack-specific security rules
- Everything in the JS bundle and in public environment variables can be extracted from the app; never place secrets there.
- Store tokens and credentials in secure storage (Keychain / Keystore, e.g. `expo-secure-store` or `react-native-keychain`), not in `AsyncStorage`.
- Use HTTPS only; do not enable cleartext traffic or disable certificate validation.
- Validate and allow-list deep link and universal link parameters before using them for navigation or API calls.
- Do not load untrusted content in `WebView` without restricting `originWhitelist` and disabling unneeded JavaScript bridges.
- Request the minimum native permissions, and only at the moment they are needed.
- Do not log tokens or personal data.
