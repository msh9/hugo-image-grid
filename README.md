# hugo-image-grid (Hugo theme)

A minimal, no-JS theme that renders images placed in `content/` as a responsive grid.

Key points:
- No image processing or resizing (serves original files).
- Single CSS file at `themes/image-grid/assets/css/theme.css`.
- No JavaScript, no external fonts or build tools.

## Usage

1. In your `hugo.toml`, set:

   ```toml
   theme = "hugo-image-grid"
   ```

2. Place images alongside a page bundle (recommended) so Hugo can treat them as page resources. Two simple patterns:
   - Leaf bundle: `content/my-album/index.md` with images in the same folder.
   - Section bundle: `content/exampleSection/_index.md` with images in the same folder.

   Sections are treated as separate albums. On the home page, each top‑level section is shown in its own block, with its title linking to that section’s page. The section page itself displays the section’s images (and, by default, images from descendant pages).

   You can set the section’s title/description in its `_index.md` front matter:

   ```md
   ---
   title: My Example Section Title
   description: This is the description of my example section.
   ---
   ```

3. The theme will:
   - Home (`/`): group by top‑level section; for each section, display all images found in that section and its descendant pages. The section title links to that section’s page.
   - Single page: display that page’s images in a grid, and render page content above the grid.
   - List/section page: display section images plus images from descendant pages.

Alt text uses the resource title when available, or falls back to the filename (without extension). Images use `loading="lazy"` and `decoding="async"` for better performance.

### Image discovery and grid defaults

- Images are discovered only via page resources: `*.{jpg,jpeg,png,webp,avif,gif,bmp}` (case‑insensitive). No image processing or transforms are performed.
- Default grid uses CSS Grid; no JS and no external frameworks. 

### Thumbnails

The theme can use pregenerated thumbnails on the home page and section pages. If pregenerated thumbnails are not provided, the original images are used as-is.

How it works:
- Provide two files per image within the same bundle: the original and its thumbnail.
- Name the thumbnail with `.thumbnail.` right before the file extension (case-insensitive match on the word `thumbnail`).
- Thumbnails can use a different extension than the original.
- In grids (home/section pages), the tile links to the original image but displays the thumbnail when available.
- Single pages continue to display the original images; thumbnails are not used on single pages.

Example:

```
/exampleSite/content/myalbum/
photo1.avif
photo1.thumbnail.avif
photo2.webp
photo3.jpg
photo3.thumbnail.jpg
```

In the above example, thumbnails are used for photo1 and photo3; the original is used for photo2.

###  Gallery Hero/Featured Image(s)

hugo-image-grid treats page and section bundles as galleries within the directory structure. For example,

```
/exampleSite/content/
photo1.avif
myAlbum/photo2.avif <-- Gallery in main site
myAlbum/photo3.avif
someSection/_index.md <-- Gallery in main site
someSection/anotherAlbum/photo4.avif <-- Gallery in 'someSection'
someSection/anotherAlbum/photo5.avif
```

In each gallery you can choose to either display all photos of each immediate child gallery *or* display a thumbnail of one image from each child gallery that links to the child gallery. In the above example the home page can be configured to show `photo1.avif` and *all* of the photos in `myAlbum` and photos in the `someSection` bundle or to just show `photo1.avif` and one featured thumbnail for each of `myAlbum` and `someSection`. In either case photos from `another Album` are not immediately shown on the home page.

This choice can be set site wide via the site configuration file or on a per section basis. To configure site wide,

```toml
[params]
  [params.modules]
    [params.modules.hugoImageGrid]
      [params.modules.hugoImageGrid.display]
        useFeaturedImages = true
```

To configure use front matter,

```yaml
---
params:
   modules:
      hugoImageGrid:
         display:
            useFeaturedImages = true
```

## Guardrails

- No `.Resize`, `.Fit`, `.Filter`, or any other image processing is used.
- No `<script>` tags.
- No external webfonts or CSS frameworks.

## Attribution

Authored for this site; not copied from other themes.
