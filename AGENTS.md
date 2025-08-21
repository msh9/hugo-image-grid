# AGENTS.md

A concise guide for a CLI coding agent collaborating on this project.

## Commands for agent to use in this project

* `ripgrep` and `grep -R`: for search recursively in files
* `hugo build -D`: to validate that the theme/site builds cleanly

## Project scope & tech

* This repo contains a **Hugo theme** (for the GoHugo static site generator).
* Files with the `.html` extension inside the theme are **Go `text/template` / `html/template`** files used by Hugo (i.e., Go template syntax lives inside HTML).
* The theme includes **JavaScript** (ES modules) and **CSS** (or Sass). Assume modern browsers.
* Images are provided **pre-rendered** in the content/static folders. Important: do **not** add Hugo image processing unless explicitly requested.
* Galleries/lightbox should rely on HTML (e.g., `<picture>` for AVIF/WebP/JPEG) and attributes in templates.

## How the agent should work (safe defaults)

* **No large deps by default.** Don’t add packages, heavy frameworks, or build steps unless requested.
* **Accessibility & semantics.** Use semantic HTML, alt text, and ARIA where relevant. Don’t regress a11y.
* **Performance-conscious.** Prefer lightweight JS (defer/async), CSS that’s scoped, and minimal DOM work.

## Code conventions (defaults unless told otherwise)

* **Templates:** Use Hugo blocks, partials, and shortcodes. Keep logic in templates minimal and readable.
* **JavaScript:** ES modules, no global leaks. Keep UI behavior progressive-enhancement friendly.
* **CSS:** Organize by component/page. Avoid utility frameworks unless already in use. Namespaced classes or BEM are fine.
* **Images:** Use `<picture>` with AVIF/WebP/JPEG sources when possible. Do not transform images at build time unless requested.

## When in doubt, ask

If requirements, structure, or tooling are unclear—stop and ask before changing files.
