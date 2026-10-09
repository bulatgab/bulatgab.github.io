# bulatgab.github.io

Personal link page. One static `index.html`, no build step.

- **Edit** `index.html` and push to `main`. GitHub Pages serves the files as they are
  (`.nojekyll` switches off Pages' built-in Jekyll processing).
- **Preview locally:** `python3 -m http.server 8000`, then open <http://localhost:8000>.
- **Avatar:** `avatar.jpg` is 320×320, resized from the original with
  `magick original.jpeg -resize 320x320 -quality 85 -strip avatar.jpg`.
- **Favicon:** `favicon.svg` is the source. The raster fallbacks are rendered from it with
  [ImageMagick](https://imagemagick.org/):

  ```sh
  magick -background none -density 600 favicon.svg -define icon:auto-resize=48,32,16 -depth 8 favicon.ico
  sed 's/rx="14"/rx="0"/' favicon.svg | magick -background '#3b5bdb' -density 600 svg:- -resize 180x180 -alpha off -depth 8 -strip apple-touch-icon.png
  ```
- **Project thumbnails** live in `img/` as square WebP at 480 and 960 px (`srcset`).
  The Life in Weeks tile is a headless-Chrome shot of the app at an 800×880 window,
  2× device scale (that height makes the grid come out about square), with
  `#fab, #share-fab, #stats, #legend` hidden via an injected `<style>`, cropped tight
  to the dots left and right and padded to a square with the app's background
  (`-crop 1538x1538+31+55`: outer dot columns at x = 31 and 1569), then
  `magick tile.png -resize 960x960 -define webp:method=6 -quality 42 img/lifeinweeks-960.webp`
  (480 px at quality 50). The card shows it as `class="thumb inset"`: CSS frames it
  with the card's text padding in its background colour (`--inset-bg: #1a0b2e`), so
  the dots line up with the text at every width. The URL with the sample life is in
  the lifeinweeks README (the chart goes after `#` there).
  The Art Decoded tile is the live app (https://art-decoded.pages.dev/) at an 800×880
  window, 2× device scale, after clicking the blue-cloak couple in *Netherlandish
  Proverbs* (CSS point 330, 690). Flutter paints the painting only after its tiles
  load, which plain `--screenshot` does not wait for, so it was captured over the
  Chrome DevTools protocol after a 15 s real-time wait. Cropped
  `-crop 1460x1460+20+95` (drops the floating buttons), then the same `magick` commands.
