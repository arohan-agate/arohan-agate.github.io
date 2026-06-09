# arohan-agate.github.io

Personal academic site, live at **<https://arohan-agate.github.io/>**.

Dependency-free static HTML/CSS — no framework, no build step, nothing to
install. GitHub Pages serves the repo straight from the `main` branch (root
folder), so **publishing = commit + push to `main`**. Give it a minute or two.

```
index.html              ← all content lives here; edit this 99% of the time
404.html                ← not-found page (self-contained)
assets/css/style.css    ← all styling (design tokens at the top)
assets/fonts/*.woff2    ← self-hosted fonts (Inter, JetBrains Mono)
assets/img/             ← profilepic.jpg, og.png social card
assets/figs/            ← publication figures
favicon.svg / .ico / apple-touch-icon.png
robots.txt / sitemap.xml
.nojekyll               ← tells Pages to serve files as-is (no Jekyll)
```

**Layout:** a fixed left sidebar (`.rail`) holds your photo, name, blurb,
social links, and section nav; the right pane (`.content`) holds the sections.
The sidebar nav highlights whichever section you're viewing — a small
scroll-spy script at the bottom of `index.html`. Search `index.html` for
**`FILL IN:`** to find every spot meant for you.

## Recipes

### Add a publication

In `index.html`, find `SELECTED PUBLICATIONS`, copy a whole
`<article class="pub"> … </article>`, paste it (top = first), and edit:

1. **Figure** — drop an image at `assets/figs/<key>.png` (4:3 crop, ~600px
   wide) and set it as the `.pthumb` `<img src>` with descriptive `alt`.
2. **Title** (`h3`) — wrap in `<a href="…">` when there's a link, else plain.
3. **Authors** (`.auth`) — keep `<b>…</b>` around your own name.
4. **Venue** (`.ven`) — e.g. `CVPR 2026`; optional `<span class="tag">status</span>`.
5. **Summary** (`.sum`) — one or two lines; delete the `<p>` to omit.
6. **Links** (`.plinks`) — one `<a>` per link. For an unreleased item use
   `<span class="soon">paper</span>` (dashed, non-clickable).

### Add an experience / education / teaching entry

All three use the same `<article class="ent">` block. Copy one, paste
(newest first), and edit:

- `.ent-h` — organization (Experience/Education) or "Teaching Assistant"
  with a `<span class="muted">· CSE 123</span>` (Teaching)
- `.ent-s` — role / sub-line
- `.ent-d` — one-line description (optional; delete the `<p>` to omit)
- `.ent-w` — date; add a `<span>Location</span>` to put a place beneath it

### Add or remove a section

Each section is `<section id="x"> … </section>` in `.content` with an
`<h2>` heading. If you add/remove one, keep the sidebar `.toc` nav in sync —
each nav link's `data-sec` must match the section `id` for scroll-spy to work.

### Swap the profile photo

Save a square crop (≥ 184px) to `assets/img/profilepic.jpg`. It's shown as a
circle (`border-radius:50%` on `.photo` in `style.css`) — change that to e.g.
`14px` if you'd rather have a rounded square.

### Add your CV

Commit the PDF as `assets/resume.pdf` (the sidebar "Resume" link already
points there).

### Keep metadata honest

- Bump the sidebar footer date and `<lastmod>` in `sitemap.xml` on real updates.
- Social card is `assets/img/og.png` (1200×630), referenced by the `og:image`
  / `twitter:image` tags in `<head>`.
- New profile URLs go in both the sidebar `.social` nav and the JSON-LD
  `sameAs` array in `<head>`.

## Fonts

**Inter** (UI/body) and **JetBrains Mono** (labels, dates, nav) are
self-hosted in `assets/fonts/` as variable `woff2` (latin + latin-ext),
declared via `@font-face` at the top of `style.css` and preloaded in
`index.html`. No third-party requests at runtime.

## Design

Tokens (colors, fonts) are CSS custom properties at the top of `style.css`.
Palette: page `#fbfbfc`, ink `#15171d`, soft `#565b66`, accent `#2f54eb`.
The faint tone is `#6b707e` (not the mockup's `#8b909b`) so small text meets
WCAG AA contrast (4.8:1).

## Local preview

Live-reload while editing:

```sh
npx live-server          # opens the site, refreshes on save
```

or a plain server: `python3 -m http.server 8000` → <http://localhost:8000>.

## Deploying

```sh
git add -A && git commit -m "Update content" && git push
```

GitHub Pages redeploys `main` automatically — no Actions workflow, no build.
