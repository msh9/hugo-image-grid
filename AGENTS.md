# AGENTS.md

A concise guide for a CLI coding agent collaborating on this project.

## Project scope & tech

* This repo contains a **Hugo theme** (for the GoHugo static site generator).
* Files with the `.html` extension inside the theme are **Go `text/template` / `html/template`** files used by Hugo (i.e., Go template syntax lives inside HTML).
* The theme includes **JavaScript** (ES modules) and **CSS** (or Sass). Assume modern browsers.
* Images are provided **pre-rendered** in the content/static folders. Do **not** add Hugo image processing unless explicitly requested.
* Galleries/lightbox should rely on HTML (e.g., `<picture>` for AVIF/WebP/JPEG) and attributes in templates.

## How the agent should work (safe defaults)

1. **Incremental, small-scope changes.** Prefer minimal diffs and short PRs that accomplish one thing.
2. **Ask first.** Before modifying or creating files for a *new* feature or behavior, post 2–6 clarifying questions to confirm intent, scope, and constraints. Proceed only after answers are received.
3. **Propose a plan.** When starting work, output a brief plan listing:

   * Goal and acceptance criteria
   * Files to touch/create
   * Any new templates/partials/shortcodes
   * Any new JS/CSS modules
4. **Show the diff.** Provide patch-style diffs (or file-by-file snippets) for review before writing to disk.
5. **Keep it reversible.** Avoid destructive changes. Don’t delete or rename files without explicit approval.
6. **Respect existing config.** If linters/formatters/tooling exist, use them. If not, suggest minimal configs (opt-in).
7. **No large deps by default.** Don’t add packages, heavy frameworks, or build steps unless requested.
8. **Accessibility & semantics.** Use semantic HTML, alt text, and ARIA where relevant. Don’t regress a11y.
9. **Performance-conscious.** Prefer lightweight JS (defer/async), CSS that’s scoped, and minimal DOM work.

## Code conventions (defaults unless told otherwise)

* **Templates:** Use Hugo blocks, partials, and shortcodes. Keep logic in templates minimal and readable.
* **JavaScript:** ES modules, no global leaks. Keep UI behavior progressive-enhancement friendly.
* **CSS:** Organize by component/page. Avoid utility frameworks unless already in use. Namespaced classes or BEM are fine.
* **Images:** Use `<picture>` with AVIF/WebP/JPEG sources when possible. Do not transform images at build time unless requested.

## Workflow checklist

1. Confirm task with questions (if feature/behavior is new).
2. Share a brief plan + file list.
3. Provide diffs for review.
4. Implement incrementally; run Hugo locally (`hugo server`) if applicable.
5. Include minimal test content/examples when helpful.
6. Write clear commit messages (Conventional Commits style recommended).

## When in doubt, ask

If requirements, structure, or tooling are unclear—stop and ask before changing files.
