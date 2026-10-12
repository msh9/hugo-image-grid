# Repository Guidelines

## Project information and goals
- Reference `README.md` for information about the goals and features of the project

## Project Structure & Module Organization
- Theme root: Hugo templates in `layouts/` (Go HTML templates).
- Partials: `layouts/_partials/`
  - `image-grid.html`: renders normalized items.
  - `process-image.html`: processes one image into AVIF/JPG renditions and resolves alt text.
  - `prepare-bundle-images.html`, `prepare-feature-image.html`, `prepare-children-featured-items.html`: assemble normalized items for the grid.
  - `use-featured-images.html`: resolves the `useFeaturedImages` setting.
- Pages: `layouts/home.html`, `layouts/list.html`, `layouts/single.html`, `layouts/baseof.html`
- Assets: CSS in `assets/css/` (e.g., `theme.css`). 
- Static: For static assets used by third party libraries provided with theme and in-theme static assets that do not require hugo asset pipeline processing
- exampleSite: Contains a small example site for development testing and demonstrating the theme. 
- Config/examples live alongside in repo (`hugo.toml`, `theme.toml`).

## Build, Test, and Development Commands
- `hugo build --ignoreCache`: **important** must be run inside of the `exampleSite` folder, Build the site (include drafts) to validate templates compile.
- `rg <pattern>`: Fast code search across the repository.
- Optional locally: `hugo server --ignoreCache` to run a live-reload dev server.
- `npm run`: discover available npm commands
- `npm run format`: format golang html templates after editing
- `npm run lint:css:fix`: format CSS after edits

## Coding Style & Naming Conventions
- Indentation: 2 spaces; keep templates readable and minimal.
- Hugo templates: Prefer partials and normalized inputs. Business logic in helpers; presentation in components.
- CSS: Component‑scoped rules; avoid heavy frameworks. Use semantic class names.
- ~~Images: Do not add Hugo image processing.~~ Changing as of Fall, 2026 due to Hugo now supporting AVIF via a WASM plugin. We'll be making changes to hugo-image-grid to support avif with a jpg fallback. This will also mean that we can support more build time photo processing, simplify gallery inputs, and extract exif data ahead of time.

## Testing Guidelines
- No formal test suite. Validate by running `hugo build --ignoreCache` within the `exampleSite` folder and inspecting output for errors.

## Commit & Pull Request Guidelines
- New work and features occur on branches that are only merged to main after local validation and a PR review on github
- Commits: Small, focused, imperative subject lines (e.g., "Refactor home grid items").
- PRs: Describe intent, scope, and user impact; link issues; include before/after screenshots for UI changes.

## Agent-Specific Instructions
- Single Responsibility: `image-grid.html` renders normalized items only; helper partials assemble data.
- Maintain accessibility: meaningful `alt`, semantic markup, no regressions.
