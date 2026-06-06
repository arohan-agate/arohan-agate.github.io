# arohan-agate.github.io

Personal academic site, live at **<https://arohan-agate.github.io/>**.

Dependency-free static HTML/CSS — no framework, no build step, nothing to
install. GitHub Pages serves the repo straight from the `main` branch (root
folder), so **publishing = commit + push to `main`**. Give it a minute or two
to deploy.

```
index.html              ← all content lives here; edit this 99% of the time
404.html                ← not-found page
assets/css/style.css    ← all styling (design tokens at the top)
assets/fonts/*.woff2    ← self-hosted fonts (Fraunces, Newsreader, JetBrains Mono)
assets/img/             ← og.png social card; your portrait + pub figures go here
favicon.svg / .ico / apple-touch-icon.png
robots.txt / sitemap.xml
.nojekyll               ← tells Pages to skip Jekyll and serve files as-is
```

Every editable spot in `index.html` is marked with a comment starting with
**`FILL IN:`** — searching for that string is the fastest tour of what's left
to do. Repeatable sections also have a template note explaining how to add
another block.

## Recipes

### Add a publication

In `index.html`, find the `SELECTED PUBLICATIONS` section, copy any whole
`<article class="pub"> … </article>` block, paste it where you want it
(they appear in page order), and edit:

1. **Thumbnail** — drop a figure at `assets/pubs/yourkey.jpg` (4:3 crop,
   ~600px wide), then replace the placeholder `<div class="thumb g1">` with:

   ```html
   <img class="thumb" src="assets/pubs/yourkey.jpg"
        alt="Key figure from PAPER TITLE" width="592" height="444">
   ```

   Until you have a figure, the placeholder gradients `g1` / `g2` / `g3` work.
2. **Title** — text plus the `href` (project page, arXiv, or PDF).
3. **Authors** — keep `<b>…</b>` around your own name.
4. **Venue** — e.g. `CVPR 2026`; optional chip: `<span class="tag">oral</span>`.
5. **Summary** — one or two lines; delete the `<p>` if you don't want one.
6. **Links** — keep only the tags you have (`paper / arXiv / code /
   project page / poster / bibtex`). For bibtex, the simple approach is to
   commit a plain-text file (e.g. `assets/bib/yourkey.txt`) and link to it.

### Add an experience or teaching entry

Both sections use the same block. Copy a whole
`<article class="entry"> … </article>`, paste (newest first), and edit:

- `role` — job title; the optional `<span>· incoming</span>` renders softer
- `org` — organization — team or lab
- `when` — right-aligned date, e.g. `2024 – present`
- `desc` — optional one-liner; delete the `<p>` if unwanted

### Swap in your profile photo

1. Save a portrait crop (roughly 5:6, at least 500px wide) to
   `assets/img/portrait.jpg`.
2. In the `<header>` of `index.html`, delete the placeholder
   `<div class="portrait …">your photo</div>` and uncomment the `<img>`
   right below it.

### Add your CV

Commit the PDF as `assets/cv.pdf` and point the header's `CV (PDF)` pill at
`assets/cv.pdf` (it's an `href="#"` placeholder right now, like Email,
Google Scholar, and LinkedIn — all marked `FILL IN:`).

### Enable the News section

A ready-made `NEWS` section sits commented-out between About and
Publications. Remove the wrapping comment markers and add one
`<div class="news-row">` per item, newest first.

### Keep the metadata honest

- When you fill in Scholar/LinkedIn, also append the URLs to `"sameAs"` in
  the JSON-LD `<script>` in `<head>`.
- Bump the footer's "last updated" line and `<lastmod>` in `sitemap.xml`
  when you publish meaningful changes.
- The social-preview card is `assets/img/og.png` (1200×630), referenced from
  the `og:image` / `twitter:image` tags.

## Fonts

Fraunces (display), Newsreader (body), and JetBrains Mono (labels) are
**self-hosted** in `assets/fonts/` as variable-weight `woff2` files
(latin + latin-ext subsets, fetched once from Google Fonts), declared via
`@font-face` at the top of `style.css`, and preloaded in `index.html`.
No third-party requests at runtime. They're static assets — there's nothing
to maintain unless you want different fonts.

## Design

All tokens (colors, font stacks) are CSS custom properties at the top of
`assets/css/style.css`. Palette: paper `#f7f4ec`, ink `#211e1a`, soft ink
`#5c544a`, rust accent `#a8421f`. One deliberate deviation from the original
mockup: the faint label tone is `#756c5f` instead of `#938a7c` so small text
meets WCAG AA contrast (4.7:1).

## Local preview

```sh
python3 -m http.server 8000
# → http://localhost:8000
```

(Plain `file://` mostly works too, but `http.server` matches how Pages
serves the root-absolute paths in `404.html`.)

## Deploying

```sh
git add -A && git commit -m "Update content" && git push
```

GitHub Pages redeploys `main` automatically — no Actions workflow, no build.
