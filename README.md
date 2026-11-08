# lucascaldentey.dev

A retro, playable personal website: you fall from orbit, past Earth and through the
clouds, landing on a plucked piano-chord "string" at the end of each section, and
finish at home on the ground floor, where a cave opens once enough coins are found.
A **Classic mode** button shows everything as a normal web page.

No build step and no dependencies: it's plain HTML, CSS and JavaScript.

## Files

| Path | What it is |
|---|---|
| `index.html` | The whole site: content, styles and game code |
| `favicon.svg` | Browser-tab icon |
| `CNAME` | Tells GitHub Pages to serve the site at `lucascaldentey.dev` |
| `.nojekyll` | Tells GitHub Pages to serve the files as-is |
| `audio/` | Your songs (`song-1.mp3`, …) |
| `images/` | Photos and pictures |

## Run it locally

1. Open this folder in VS Code.
2. Install the **Live Server** extension.
3. Right-click `index.html` → **Open with Live Server**. The page reloads every time you save.

(Opening `index.html` by double-clicking also works, but songs may not play from `file://`.)

## Editing content

Search `index.html` for `[` — every placeholder is in square brackets. Sections are
marked with comments like `<!-- ============ 2. EDUCATION ============ -->`.

| You want… | Use |
|---|---|
| A box (bump it for a coin) | `<div class="block" data-solid><h3>TITLE</h3><p>Short text</p></div>` |
| A **＋** box (bump to open more info) | `<div class="block expand" data-solid><span class="icon">＋</span><h3>TITLE</h3><p>Short</p><div class="more">Longer text…</div></div>` |
| A **↗** link box (opens a new tab) | `<a class="block link" data-solid href="https://…" target="_blank" rel="noopener"><span class="icon">↗</span><h3>TITLE</h3><p>…</p></a>` |
| A **♪** song box | `<div class="block track" data-solid data-src="audio/song.mp3"><span class="icon">♪</span><h3>TITLE</h3><p>…</p><div class="prog"><i></i></div></div>` |
| A **→** room (bump to enter more boxes) | A box with `class="block portal" data-room="room-x"`, plus a `<div class="row room" id="room-x" data-title="NAME">` after the section's main row. Start the room with the `← BACK` box (copy one from Hobbies). |
| A background picture | Any element **without** `data-solid` |

Rules that keep the game playable:

- About **4 boxes per row** at most, so every box stays at bumping height.
- Keep box text short; put long text in a `＋` panel or a `→` room.
- Each section ends with `<div class="string" data-chord="…"></div>`. Chords available:
  `Cmaj9`, `Am9`, `Fmaj9`, `G13sus`, `Cadd9` (add more in `CHORDS` in the script).
- The cave opens with 60% of all coins. To set a number, add `data-cost="10"` to `<div class="gate" …>`.

If something breaks, open the browser console (Cmd+Option+I / F12): it shows the error and line.

## Publish on GitHub Pages

1. Commit and push all files (including `CNAME` and `.nojekyll`) to the `main` branch.
2. On GitHub: **Settings → Pages → Build and deployment → Source: Deploy from a branch**,
   branch `main`, folder `/ (root)` → Save.
3. Still in **Settings → Pages**, check that **Custom domain** reads `lucascaldentey.dev`
   (the `CNAME` file fills it in) and click Save if needed.

## Point the domain at GitHub (at your registrar's DNS settings)

| Type | Host | Value |
|---|---|---|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `YOUR-GITHUB-USERNAME.github.io` |

Optional (IPv6) AAAA records for `@`: `2606:50c0:8000::153`, `2606:50c0:8001::153`,
`2606:50c0:8002::153`, `2606:50c0:8003::153`.

Remove any old parking/forwarding records for `@` or `www` that the registrar added.

Recommended: verify the domain under your **GitHub account → Settings → Pages → Add a
domain** (it gives you a TXT record to add), which prevents anyone else claiming it.

Then wait for GitHub to issue the certificate (often under an hour, DNS can take up to
24 h) and tick **Enforce HTTPS**. `.dev` sites only load over HTTPS, so the site appears
once the certificate is ready.

## Updating

Edit → check in Live Server → commit and push. The live site updates in a minute or two.
