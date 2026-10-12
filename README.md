# hugo-image-grid (Hugo theme)

Opinionated theme that renders images into a center aligned grid with a modal lightbox.

Key points:
- Simple HTML/CSS brick-like layout with two different row heights based on device viewing size (see (Photos @ michaelonrandom)[https://photos.michaelonrandom.com] for example)
- Inputs are generally expected to be high resolution, high quality, photographic images which the theme with resize and encode to avif with jpg backups. Images should be in [Hugo processable format](https://gohugo.io/quick-reference/glossary/#processable-image).
- If present, the theme will attempt to use image metadata to provide contextual information. At this time, we look for 'title' and 'copyright' fields.
- Image lightbox using [Lightbox2 with tags](https://github.com/msh9/lightbox2)
  - Currently using v3.0.4

## Usage

1. In your `hugo.toml`, set:

   ```toml
   theme = "hugo-image-grid"
   ```

2. Place images alongside a page bundle (recommended) so Hugo can treat them as page resources. Two simple patterns:
   - Leaf bundle: `content/my-album/index.md` with images in the same folder.
   - Section bundle: `content/exampleSection/_index.md` with images in the same folder.

   Sections are treated as separate albums. On the home page, each top‑level section is shown in its own block, with its title linking to that section’s page. The section page displays the section’s own images and, depending on configuration, either a single featured image per immediate child gallery or full grids for each immediate child gallery. Deeper descendants are not included.

   You can set the section’s title/description in its `_index.md` front matter:

   ```md
   ---
   title: My Example Section Title
   description: This is the description of my example section.
   ---
   ```

3. The theme will (defaults):
   - Home (`/`): shows a root gallery (images at the content root) and a block per top‑level section. By default, each block displays the current bundle’s images and one featured thumbnail per immediate child gallery (both subsections and leaf bundles). Section titles link to their pages.
   - Single page: displays that page’s images in a grid below the content; thumbnails are not used.
   - List/section page: by default, displays the current bundle’s images and one featured thumbnail per immediate child gallery. Set `params.modules.hugoImageGrid.useFeaturedImages` to `false` (site‑wide or per bundle) to show all photos from immediate child galleries instead.
   - Each set of images from a gallery will be enabled to be displayed in a lightbox. When `useFeaturedImages` is false, images displayed from child galleries will be displayed in a lightbox when clicked on. When `useFeaturedImages` is true, images from child galleries will be links to the child gallery.
   - The lightbox will attempt to read image tag data in browser. Tags for 'title' and 'Copyright' are checked and, if present, displayed in the lightbox. An example of this can be seen in the example site under 'another gallery' and 'ImgD'.

Alt text comes from the image 'caption' metadata followed by the resource name (`.Name` in Hugo) as a backup.

## Size aware images

The theme uses HTML picture and source elements to help deliver (more) optimally sized images based on the rendered size of the gallery in the user agent. Images are processed by hugo and delivered using HTML srcsets as AVIF by default with a JPG backup; we avoid webp due to a longstanding implementation bug that inadvertently changes the image contrast. Quality and encoder hints can be set via Hugo's builtin [image processing configuration](https://gohugo.io/configuration/imaging/) otherwise Hugo defaults are used.

## Alternate fallback format

By default the theme generates a backup JPG image.

##  Gallery Featured Image(s)

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
      useFeaturedImages = true
```

To configure per-bundle in front matter (YAML), use:

```yaml
---
params:
  modules:
    hugoImageGrid:
      useFeaturedImages: true
---
```

The front matter configuration overrides the site configuration for that bundle only. If not configured in either location, the theme defaults to using featured thumbnail images (i.e., `useFeaturedImages: true`).

#### Featured image gallery cards

When `useFeaturedImages` is enabled, each immediate child gallery is represented by a featured image shown as a “card” in the grid. The card displays the child gallery’s title in an overlay, and both the title and the entire card link to the child gallery. Non‑featured images continue to open in a lightbox.

You can customize card sizing and readability via CSS variables (set in your site CSS if you want to override the defaults):

- `--hig-card-min-width`: minimum card width (default `260px`)
- `--hig-card-min-height`: minimum card height (default `180px`)
- `--hig-card-title-height`: overlay title bar height (default `56px`)
- `--hig-card-overlay-bg`: overlay background color (supports alpha)
- `--hig-card-title-color`: overlay title text color

These card styles apply only to featured thumbnails for immediate child galleries. Root images and regular in‑bundle images keep their existing behavior and lightbox interactions.

### Home page root images

To display images that live at the content root on the home page, create a branch bundle at `content/_index.md`. Place your root images alongside that file, for example:

```
content/
  _index.md
  photo1.avif
  photo2.jpg
```

Those images are treated as the root gallery and are always shown on the home page. The `useFeaturedImages` setting only affects how immediate child galleries are represented (featured tiles vs full grids), not whether root images are shown.

## Limitations

- The lightbox implementation does not support fallback image formats
