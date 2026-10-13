# Golden Porsche 911 GT3 RS

Scroll-controlled 4K film built from image frames drawn on a canvas, with a glass navigation bar, specs section and footer.
Plain HTML, CSS and JavaScript. No build step.

## Files

```
index.html        the whole site (HTML + CSS + JS)
frames/           put your frame images here
.nojekyll         tells GitHub Pages to serve the files as they are
README.md         this file
```

## 1. Make the frames

Frames must be named `frame_0001.webp`, `frame_0002.webp`, ... with no gaps, and placed inside `frames/`.

Recommended settings for the 48.8 second, 30fps, 3840x2160 source video:

| Setting | Value |
|---|---|
| Frame rate to extract | 15 fps (every second frame) |
| Total frames | 732 |
| Format | WebP, quality 85 |
| Size | 3840 x 2160 (keep full size) |
| Expected total size | about 105 to 110 MB |

With ffmpeg:

```
mkdir frames
ffmpeg -i Golden_Porsche_03.mp4 -vf fps=15 -c:v libwebp -quality 85 -compression_level 4 frames/frame_%04d.webp
```

Check how many files you got. If it is not 732, open `index.html` and change `FRAME_COUNT` at the top of the script.

For maximum smoothness you can extract all 1,463 frames (`-vf fps=30`, about 215 MB) and set `FRAME_COUNT = 1463`.
If you use `.jpg` or `.png` instead, change `FRAME_EXT` too.

## 2. Test locally

Open the folder through a local web server, not by double-clicking `index.html`:

```
npx serve
```

## 3. Put it on GitHub

The frames are hundreds of files, and the GitHub website only accepts 100 files per upload. Use git or GitHub Desktop:

```
git init
git add .
git commit -m "Golden Porsche site"
git branch -M main
git remote add origin https://github.com/YOUR-USER/YOUR-REPO.git
git push -u origin main
```

Then turn on GitHub Pages: repository Settings, Pages, Source "Deploy from a branch", branch `main`, folder `/ (root)`.

## Settings you can change (top of the script in index.html)

- `FRAME_COUNT` number of frames in `frames/`
- `INITIAL_FRAMES` frames loaded before the page opens (default 60, the rest load in the background)
- `HOLD` share of the scroll used by the film (default 0.88, the last frame then holds while the title shows)
- Scroll length: the `.track` height in the CSS (default 760vh). Larger means a slower film.
