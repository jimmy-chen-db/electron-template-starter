# Contributing

## Purpose

This repository is intended to serve as a reusable GitHub template for a cross-platform Electron desktop application.

The main contribution rule is simple:

> Keep shared logic shared, and isolate platform-specific logic.

---

## Repository conventions

### 1. Keep shared code in `src/shared/`

Business rules, domain models, validation, and portable utilities should live in `src/shared/`.

Do not put Windows-only or macOS-only behavior there.

### 2. Keep Electron runtime concerns in `src/main/` and `src/preload/`

- `src/main/` handles lifecycle, windows, menus, shell access, and IPC registration.
- `src/preload/` exposes a narrow API to the renderer.

The renderer should not directly depend on Node/Electron primitives.

### 3. Keep platform-dependent behavior in `src/main/platform/`

Examples:

- startup/login integration
- file reveal behavior
- menu conventions
- native shell integration
- OS-specific paths
- protocol registration edge cases

Prefer adapter classes instead of scattered `if (process.platform === ...)` checks.

### 4. Treat `artifacts/` as generated-output space

Do not commit generated installers, coverage, screenshots from transient runs, or test reports.

The folder structure exists because the repository includes `.gitkeep` placeholders.

### 5. Put permanent documentation in `docs/`

If a file is intended to be reviewed, versioned, and referenced later, it belongs in `docs/`, not `artifacts/`.

Examples:

- architecture diagrams
- ADRs
- release process notes
- curated product screenshots

---

## Pull request expectations

A good pull request should:

- have a clear title
- explain the change
- describe any platform-specific impact
- identify testing performed
- include screenshots only when the UI changed materially
- avoid mixing unrelated refactors with feature work

---

## Commit guidance

Prefer small, reviewable commits.

Good examples:

- `feat: add mac platform adapter skeleton`
- `fix: isolate file reveal logic behind preload API`
- `docs: add release packaging workflow notes`

---

## Artifact placement guide

### Commit to Git

Commit these:

- code under `src/`
- tests under `tests/`
- docs under `docs/`
- workflow files under `.github/`
- curated assets under `assets/`

### Do not commit to Git

Do not commit these generated outputs:

- `artifacts/installers/*`
- `artifacts/releases/*`
- `artifacts/test-reports/*`
- `artifacts/coverage/*`
- `artifacts/screenshots/*` from transient runs
- `artifacts/temp/*`

If something is generated and reproducible, it belongs under `artifacts/` and should usually stay ignored.

---

## Security and secrets

Never commit:

- API keys
- code-signing certificates
- notarization credentials
- `.env` files with real secrets
- release tokens

Use secret stores in CI/CD for signing and release automation.

---

## When to add a `.gitkeep`

Add a `.gitkeep` only when:

- the folder is intentionally part of the repo structure
- the folder needs to exist before tooling runs
- the folder would otherwise be empty

Do not add `.gitkeep` to hide accidental empty folders.

---

## Definition of done

A change is generally done when:

- code is in the correct layer
- platform-specific logic is isolated
- docs are updated if structure or process changed
- tests were added or updated where appropriate
- no generated artifacts were accidentally committed
