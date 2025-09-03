# Repository Guidelines

## Project information and goals
- Reference `README.md` for information about the goals and features of the project

## Project Structure & Module Organization
- Theme root: Hugo templates in `layouts/` (Go HTML templates).
- Partials: `layouts/_partials/` (e.g., `image-grid.html`, `home-grid-items.html`, `list-grid-items.html`, `single-grid-items.html`).
- Pages: `layouts/home.html`, `layouts/list.html`, `layouts/single.html`, `layouts/baseof.html`, `layouts/section.html`
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
- Images: Do not add Hugo image processing. 

## Testing Guidelines
- No formal test suite. Validate by running `hugo build --ignoreCache` within the `exampleSite` folder and inspecting output for errors.

## Commit & Pull Request Guidelines
- Commits: Small, focused, imperative subject lines (e.g., "Refactor home grid items").
- PRs: Describe intent, scope, and user impact; link issues; include before/after screenshots for UI changes.

## Agent-Specific Instructions
- Single Responsibility: `image-grid.html` renders normalized items only; helper partials assemble data.
- Do not introduce new dependencies or image processing.
- Maintain accessibility: meaningful `alt`, semantic markup, no regressions.
