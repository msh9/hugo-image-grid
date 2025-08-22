# Fixit
- fallback image doesn't work as intended due to 'group' dict implementation. Line #87 of prepare-bundle-images is an example. The group is slice of dicts generated earlier. It's mean to contain the fallback image but instead just ends up containing both primary and secondary. More generally the handling of images in both prepare-bundle- and prepare-feature- seems to be written. Codex is using multiple lookup dictionaries when one could suffice. The regexes are also too loose and should be checking for specific sizes. Generally it should just be one dict that maps from name to resource pointer. With that a series of O(1) checks can be made when image processing and building the data dict that is later used for rendering.

# Next feature
