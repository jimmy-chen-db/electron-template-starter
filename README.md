# Electron Desktop App Template

A starter repository template for building a cross-platform desktop application with a **single shared codebase** and separate packaging targets for **Windows** and **macOS**.

This template is designed for teams that want:

- one repo
- one shared application codebase
- a thin platform adapter layer
- clear separation between source code, docs, and generated artifacts
- a clean GitHub repo template baseline

## Repository goals

This structure is optimized for:

- Electron main / preload / renderer separation
- shared business logic under `src/shared`
- platform-specific behavior isolated under `src/main/platform`
- generated outputs kept out of source control
- GitHub workflow automation for CI/CD and releases

---

## Repository structure

```text
.
├─ .github/
│  ├─ ISSUE_TEMPLATE/
│  ├─ PULL_REQUEST_TEMPLATE/
│  └─ workflows/
├─ artifacts/
│  ├─ coverage/
│  ├─ installers/
│  ├─ releases/
│  ├─ screenshots/
│  ├─ temp/
│  └─ test-reports/
├─ assets/
│  ├─ icons/
│  │  ├─ mac/
│  │  └─ win/
│  └─ installer/
├─ build/
├─ config/
├─ docs/
│  ├─ adr/
│  ├─ architecture/
│  ├─ releases/
│  └─ screenshots/
├─ scripts/
├─ src/
│  ├─ main/
│  │  ├─ ipc/
│  │  └─ platform/
│  ├─ preload/
│  │  └─ api/
│  ├─ renderer/
│  │  ├─ app/
│  │  ├─ components/
│  │  ├─ hooks/
│  │  ├─ pages/
│  │  └─ styles/
│  └─ shared/
│     ├─ domain/
│     ├─ services/
│     ├─ types/
│     └─ utils/
└─ tests/
   ├─ integration/
   └─ unit/
```

---

## Where things go

### Source code

- `src/main/`  
  Electron main-process code: app lifecycle, window creation, menus, IPC registration, shell integration.

- `src/main/platform/`  
  OS-specific adapters. Keep Windows/macOS conditional behavior here instead of scattering `process.platform` checks throughout the codebase.

- `src/preload/`  
  Safe API surface exposed from Electron to the renderer via `contextBridge`.

- `src/renderer/`  
  Frontend UI code such as React/Vue/Svelte pages, components, hooks, and styles.

- `src/shared/`  
  Shared business logic, models, types, validation, and utilities that should be portable across all targets.

### Static assets

- `assets/icons/win/`  
  Windows-specific icon files such as `.ico`.

- `assets/icons/mac/`  
  macOS-specific icon files such as `.icns`.

- `assets/installer/`  
  Static installer resources, license files, branding images, splash assets, DMG backgrounds, etc.

### Build and config

- `build/`  
  Packaging-time resources or generated intermediate build metadata that your build scripts consume.

- `config/`  
  App configuration templates, environment examples, electron-builder config fragments, signing/notarization examples.

- `scripts/`  
  Build/release helper scripts, validation scripts, notarization helpers, versioning scripts.

### Documentation

- `docs/architecture/`  
  Architecture diagrams, design overviews, sequence flows.

- `docs/adr/`  
  Architecture Decision Records.

- `docs/releases/`  
  Release notes drafts or release process documentation.

- `docs/screenshots/`  
  Curated documentation screenshots that are intended to be versioned.

### Tests

- `tests/unit/`  
  Fast unit tests for shared logic, renderer utilities, and lightweight Electron abstractions.

- `tests/integration/`  
  Integration tests, IPC tests, packaged-app smoke tests, end-to-end test harnesses.

### Generated artifacts

The `artifacts/` tree is for **generated outputs** and **local build/test outputs**.

These folders include `.gitkeep` so the structure exists, but their contents should generally remain ignored.

- `artifacts/installers/`  
  Generated `.exe`, `.msi`, `.dmg`, `.pkg`, zipped release bundles.

- `artifacts/releases/`  
  Final release payloads and release-ready assembled outputs.

- `artifacts/test-reports/`  
  JUnit/XML/HTML test reports.

- `artifacts/coverage/`  
  Coverage reports.

- `artifacts/screenshots/`  
  Captured screenshots from tests or manual verification.

- `artifacts/temp/`  
  Throwaway local outputs, staging files, scratch exports.

---

## Version-control policy

Commit:

- source code
- docs
- configuration templates
- curated static assets
- workflow definitions
- placeholder `.gitkeep` files

Do **not** commit:

- packaged installers
- coverage outputs
- test reports
- local cache files
- secrets
- notarization credentials
- node modules
- build system caches

See `.gitignore` for the default policy.

---

## Suggested next steps

1. Add your package manager and build system.
2. Add Electron runtime dependencies.
3. Add renderer framework tooling.
4. Add signing and notarization configuration.
5. Add CI workflows under `.github/workflows/`.
6. Replace placeholder files in `assets/icons/` and `assets/installer/`.

---

## Recommended platform adapter pattern

Keep platform-specific behavior under:

- `src/main/platform/windows.ts`
- `src/main/platform/mac.ts`

Expose a common interface from:

- `src/main/platform/index.ts`

This keeps the application code shared while isolating OS-specific behavior.

---

## Suggested future additions

You will likely add files such as:

- `package.json`
- `tsconfig.json`
- `electron-builder.yml`
- `vite.config.ts` or equivalent
- ESLint / Prettier config
- test runner config
- signing/notarization scripts
- GitHub Actions release workflows

This template intentionally stays lightweight so you can adapt it to your preferred stack.
