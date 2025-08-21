# Repository Guidelines

## Project Structure & Module Organization
- Theme root: Hugo templates in `layouts/` (Go HTML templates).
- Partials: `layouts/_partials/` (e.g., `image-grid.html`, `home-grid-items.html`, `list-grid-items.html`, `single-grid-items.html`).
- Pages: `layouts/home.html`, `layouts/list.html`, `layouts/single.html`, `layouts/baseof.html`.
- Assets: CSS in `assets/css/` (e.g., `theme.css`). No JS by default.
- Config/examples live alongside in repo (`hugo.toml`, `theme.toml`).

## Build, Test, and Development Commands
- `hugo build -D`: Build the site (include drafts) to validate templates compile.
- `rg <pattern>`: Fast code search across the repository.
- Optional locally: `hugo server -D` to run a live-reload dev server.

## Coding Style & Naming Conventions
- Indentation: 2 spaces; keep templates readable and minimal.
- Hugo templates: Prefer partials and normalized inputs. Business logic in helpers; presentation in components.
- CSS: Component‑scoped rules; avoid heavy frameworks. Use semantic class names.
- Images: Do not add Hugo image processing. Thumbnails are pre-generated and detected via `.thumbnail.` naming (e.g., `photo.thumbnail.avif`).

## Testing Guidelines
- No formal test suite. Validate by running `hugo build -D` and inspecting output for errors.
- For changes to grids, verify item generation partials return normalized items: `[{ src, href, alt }]`.
- Keep performance in mind: avoid N² loops in templates.

## Commit & Pull Request Guidelines
- Commits: Small, focused, imperative subject lines (e.g., "Refactor home grid items").
- PRs: Describe intent, scope, and user impact; link issues; include before/after screenshots for UI changes.
- Acceptance: CI equivalent is a clean `hugo build -D` with no warnings/errors.

## Agent-Specific Instructions
- Single Responsibility: `image-grid.html` renders normalized items only; helper partials assemble data.
- Do not introduce new dependencies or image processing.
- Maintain accessibility: meaningful `alt`, semantic markup, no regressions.
