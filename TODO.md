# Before next feature
- Refactor usage of image-grid partial, separate dict keys for tiles and images are likely redundant AI generated code
- Determine if implementing <picture> elements can replace the current thumbnail implementation otherwise clean up thumbnail implementation so that rendering images is not a n^2 operation with a regex search in the inner loop
- Improve rendering on list/section pages and home page when useFeaturedImage is enabled. Right now galleries are rendered vertically stacked due to use of <section>

# Next feature
Implement use of <picture> element to support user agent aware delivery of different formats. Primarily content size and format (between jpb and avif). This implementation may possibly replace the existing thumbnail implementation.