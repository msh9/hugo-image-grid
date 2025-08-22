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

3. The theme will (defaults):
   - Home (`/`): shows a root gallery (images at the content root) and a block per top‑level section. By default, each block displays the current bundle’s images and one featured thumbnail per immediate child gallery (both subsections and leaf bundles). Section titles link to their pages.
   - Single page: displays that page’s images in a grid above the content; thumbnails are not used.
   - List/section page: by default, displays the current bundle’s images and one featured thumbnail per immediate child gallery. Set `params.modules.hugoImageGrid.display.useFeaturedImages` to `false` (site‑wide or per bundle) to show all photos from immediate child galleries instead.

Alt text uses the resource title when available, or falls back to the filename (without extension). Images use `loading="lazy"` and `decoding="async"` for better performance.

### Image discovery and grid defaults

- Images are discovered only via page resources
- No image processing or transforms are performed.
- Default grid uses CSS Grid; no JS and no external frameworks. 

### Size aware images

The theme uses HTML picture and source elements to help deliver (more) optimally sized images based on the rendered size of the gallery in the user agent. The theme can use up to three files per image format. As an example, if I have an image in a resource bundle called 'photo1.avif' then I can also provide 'small-photo1.avif' and 'medium-photo1.avif'. Generally, the theme expects 'small-*' image to be be ~400px wide and 'medium-*' images to be 800px wide.

How it works:
- Provide up to three files per image within the same bundle: the original, small, and medium
- 'small-' should be 400px wide
- 'medium-' should be 800px wide
- All images should be of the same file type and use the same file extension, e.g. all '...jpg' or '...avif' etc.
- You can provide less than three, e.g. the original and just a 'small-' image.

Example:

```
/exampleSite/content/myalbum/
picture1.avif
small-picture1.avif
photo2.webp
photo3.jpg
small-photo3.avif
medium-photo3.avif
photo4.jpg
medium-photo4.avif
```

### Alternate fallback format

The theme additionally uses the HTML picture and source elements to optionally deliver a backup file format. The theme is optimally designed for use with a modern, widely supported, image format like webp or avif. It can be useful though to provide a backup in the unlikely event that a client does not support these. The backup file should be the same dimensions as the original image, use the same name prefixed with 'alt-'. Please see the following example,

```
/exampleSite/content/myalbum/
picture1.avif
alt-picture1.jpg
small-picture1.avif
small-picture1.jpg
photo2.webp
photo3.avif
alt-photo3.png
small-photo3.avif
medium-photo3.avif
photo4.jpg
medium-photo4.avif
```

####

**Limitations** the theme does not consider the back up format for use in size aware delivery. The back up image is used for gallery featured images and gallery tiles. When the user clicks on the image in a gallery though they will be taken to the primary format file.

###  Gallery Featured Image(s)

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

In each gallery you can choose to either display all photos of each immediate child gallery *or* display a featured image from each child gallery that links to the child gallery. In the above example the home page can be configured to show `photo1.avif` and *all* of the photos in `myAlbum` and photos in the `someSection` bundle or to just show `photo1.avif` and one featured image for each of `myAlbum` and `someSection`. In either case, photos from `another Album` are not immediately shown on the home page. By default, the featured image used will be from the first photograph in the bundle based on lexicographic order. In the above example, the featured image for `myAlbum` will be of `photo2.avif` and the featured image for `someSection` will be `photo4.avif`.

This choice can be set site wide via the site configuration file or on a per section basis. To configure site wide,

```toml
[params]
  [params.modules]
    [params.modules.hugoImageGrid]
      [params.modules.hugoImageGrid.display]
        useFeaturedImages = true
```

To configure per-bundle in front matter (YAML), use:

```yaml
---
params:
  modules:
    hugoImageGrid:
      display:
        useFeaturedImages: true
---
```

The front matter configuration overrides the site configuration for that bundle only. If not configured in either location, the theme defaults to using featured thumbnail images (i.e., `useFeaturedImages: true`).

#### Home page root images

To display images that live at the content root on the home page, create a branch bundle at `content/_index.md`. Place your root images alongside that file, for example:

```
content/
  _index.md
  photo1.avif
  photo2.jpg
```

Those images are treated as the root gallery and are shown on the home page according to the `useFeaturedImages` setting.

## Guardrails

- No `.Resize`, `.Fit`, `.Filter`, or any other image processing is used.
- No `<script>` tags.
- No external webfonts or CSS frameworks.

## Attribution

Authored for this site; not copied from other themes.
