# TODO

- Add `width` and `height` attributes to grid `<img>` elements to prevent layout shift while images load. Hugo processing now provides the dimensions, but the attributes interact with the current `width: 100%; object-fit: scale-down` rules in `theme.css`, so the layout needs to be checked when adding them.
