# bulatgab.github.io

Personal link page. One static `index.html`, no build step.

- **Edit** `index.html` and push to `main`. GitHub Pages serves the files as they are
  (`.nojekyll` switches off Pages' built-in Jekyll processing).
- **Preview locally:** `python3 -m http.server 8000`, then open <http://localhost:8000>.
- **Favicon:** `favicon.svg` is the source. The raster fallbacks are rendered from it with
  [ImageMagick](https://imagemagick.org/):

  ```sh
  magick -background none -density 600 favicon.svg -define icon:auto-resize=48,32,16 -depth 8 favicon.ico
  sed 's/rx="14"/rx="0"/' favicon.svg | magick -background '#3b5bdb' -density 600 svg:- -resize 180x180 -alpha off -depth 8 -strip apple-touch-icon.png
  ```
