# Protected Paths

Agents must not modify these without explicit user approval:

- `.github/guardrails/**`
- `.github/workflows/**`
- `.env`, `.env.*`, `**/*.pem`, `**/*.key`
- Lock files (`package-lock.json`, `pnpm-lock.yaml`, `poetry.lock`, ...) except via the package manager
- Generated or vendored directories (`dist/`, `build/`, `node_modules/`, `vendor/`)
