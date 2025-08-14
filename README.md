# image-grid (Hugo theme)

A minimal, no-JS theme that renders images placed in `content/` as a responsive grid.

Key points:
- No image processing or resizing (serves original files).
- Single CSS file at `themes/image-grid/assets/css/theme.css`.
- No JavaScript, no external fonts or build tools.

## Usage

1. In your `hugo.toml`, set:

   ```toml
   theme = "image-grid"
   ```

2. Place images alongside a page bundle (recommended) so Hugo can treat them as page resources. Two simple patterns:
   - Leaf bundle: `content/my-album/index.md` with images in the same folder.
   - Section bundle: `content/photos/_index.md` with images in the same folder.

3. The theme will:
   - Home (`/`): aggregate and display all images from the site’s pages and the home page’s own resources.
   - Single page: display that page’s images in a grid, and render page content above the grid.
   - List/section page: display section images plus images from descendant pages.

Alt text uses the resource title when available, or falls back to the filename.

## Guardrails

- No `.Resize`, `.Fit`, `.Filter`, or any other image processing is used.
- No `<script>` tags.
- No external webfonts or CSS frameworks.

## Attribution

Authored for this site; not copied from other themes.

