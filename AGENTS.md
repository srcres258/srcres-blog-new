# AGENTS.md

## Repository Overview
- Project type: Hexo static blog (`hexo` 8.x) with NexT theme.
- Primary content lives under `source/`; generated site output is `public/`.
- Main configuration files are `_config.yml` (Hexo) and `_config.next.yml` (NexT).
- Package manager in CI is **npm** (`package-lock.json` present).
- `pnpm-lock.yaml` also exists; `pnpm run <script>` works for existing scripts.

## Canonical Paths
- Blog posts: `source/_posts/*.md`
- Custom theme data/assets: `source/_data/*`
- Post/page scaffolds: `scaffolds/*.md`
- Hexo config: `_config.yml`
- Theme config: `_config.next.yml`
- CI workflow: `.github/workflows/ci.yml`

## Files You Should Usually NOT Edit
- `public/**` (generated output; also gitignored)
- `node_modules/**`
- Lockfiles unless dependency changes are intentional

## Build / Lint / Test / Typecheck Commands

### Install
- `npm install`

### Build & Serve
- `npm run clean` → runs `hexo clean`
- `npm run build` → runs `hexo generate`
- `npm run server` → runs `hexo server`
- `npm run deploy` → runs `hexo deploy`

### Direct CLI Equivalents
- `npx hexo clean`
- `npx hexo generate`
- `npx hexo server`
- `npx hexo deploy`

### pnpm Equivalents (if pnpm is used locally)
- `pnpm run clean`
- `pnpm run build`
- `pnpm run server`
- `pnpm run deploy`

### CI Command Flow (from `.github/workflows/ci.yml`)
- `npm install`
- `npx hexo generate`
- `npx hexo deploy`
- Node.js version pinned to `24.14.0` in CI jobs.

### Lint / Test / Typecheck Status
- No lint script is defined in `package.json`.
- No test script/framework is configured in this repository.
- No TypeScript config (`tsconfig*.json`) exists.

### Running a Single Test (Important)
- There is currently **no test runner configured**, so single-test execution is **not available**.
- If you add tests in future, also add:
  - a root `test` script in `package.json`
  - a documented single-test command in this file.

## Code Style & Conventions

### General
- Keep changes minimal and focused to the user request.
- Preserve existing file structure and naming patterns.
- Prefer explicit configuration edits over broad rewrites.

### Markdown (posts/pages/scaffolds)
- Use YAML front matter bounded by `---`.
- For posts, keep at least: `title`, `date`; `tags` is commonly present.
- Existing posts also use `lang: zh-CN`; follow the locale of the post content.
- Keep headings and prose readable; avoid unnecessary HTML unless needed.
- Use `<!-- more -->` only when you intentionally want excerpt splitting.

### YAML (`_config.yml`, `_config.next.yml`)
- Use 2-space indentation.
- Keep keys grouped by existing comment blocks/sections.
- Do not reorder large sections unless required.
- Prefer editing the smallest possible key path.
- Preserve quoted values where already quoted.

### Stylus (`source/_data/styles.styl`)
- Follow indentation-based Stylus syntax (no braces/semicolons).
- Keep font/style declarations concise and grouped logically.
- Reuse existing font naming style (e.g., quoted family names).

### JavaScript (if you must add custom JS)
- There is no local JS app source by default; avoid adding JS unless needed.
- Match NexT/Hexo ecosystem style used by theme scripts:
  - 2-space indentation
  - semicolons
  - single quotes
  - `const`/`let` (avoid `var`)
  - camelCase naming
- Prefer defensive error handling for browser APIs (`try/catch` + fallback path).
- Do not introduce TypeScript-only syntax into `.js` files.

### Imports / Modules
- This repo does not define an app-level module system for custom source.
- Before introducing `import`/`export`, ensure the target file is actually processed by an appropriate build/runtime path.
- For content/config-only changes, avoid adding JS module infrastructure.

### Types
- No TypeScript is configured; keep authored code compatible with plain JS/Hexo.
- Do not add `tsconfig`/TS tooling unless explicitly requested.

### Naming
- Follow existing conventions:
  - files: lowercase, kebab-case or existing pattern
  - variables/functions (JS): camelCase
  - config keys: preserve upstream Hexo/NexT naming

### Error Handling
- Avoid silent failures in scripts.
- If adding async browser logic, use `try/catch` and preserve UX fallback behavior.
- In config/content edits, validate by running `npm run build`.

## Agent Workflow Expectations
- Read relevant config and content files before editing.
- For content edits: verify front matter + markdown rendering assumptions.
- For config edits: verify with `npm run build`.
- Do not edit generated `public/` output to implement source changes.
- Keep commits atomic if user later asks for commit creation.

## Rule Files Check (Cursor / Copilot)
- `.cursor/rules/**`: not found
- `.cursorrules`: not found
- `.github/copilot-instructions.md`: not found
- Therefore, no additional Cursor/Copilot repository instructions are currently enforced.

## Quick Task Playbooks

### Add or edit a post
1. Edit/create file in `source/_posts/`.
2. Ensure valid front matter (`title`, `date`, optional `tags`, optional `lang`).
3. Run `npm run build`.

### Update site/theme configuration
1. Modify `_config.yml` and/or `_config.next.yml`.
2. Keep existing section structure and comments intact.
3. Run `npm run build`, then optionally `npm run server` for visual verification.

### Update styling
1. Edit `source/_data/styles.styl`.
2. Keep Stylus syntax and current formatting conventions.
3. Run `npm run build` and inspect locally via `npm run server`.

## What “Done” Means in This Repo
- Requested source/config/content updates are implemented.
- `npm run build` succeeds.
- No generated artifacts are manually patched in `public/`.
- Documentation updates (this file) remain aligned with `package.json` and CI.
