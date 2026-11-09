# CLAUDE.md

Working rules for this repo. Photo sources, credits and the font decision are in `README.md`.

## Status: NOT LIVE

**This site is not live.** bayareatrackclub.org still points at the old Squarespace site; nothing in this repo is deployed, and there is no remote yet. Work locally: `python3 -m http.server 8000` from the repo root, then http://localhost:8000/ (root-absolute paths don't resolve from `file://`). The local server doesn't serve `/coaches` from `coaches.html` the way GitHub Pages does, so test the stubs as `/coaches.html`.

Before it goes live, in this order:

1. **No gaps left**: `grep -rnE 'class="gap|class="confirm|GAP:' --include='*.html' .` prints nothing (see Content). `README.md`, "Outstanding", lists what's still open.
2. **GitHub Pages**: create the GitHub repo, add the remote, push `main`, turn on Pages from `main`, and set the custom domain to `bayareatrackclub.org`, the apex and the canonical host (see Paths), with a matching `CNAME` file. Check the site on its github.io address first.
3. **DNS**: at Squarespace Domains (the registrar), point the apex's A and AAAA records at GitHub Pages. Make `www` a CNAME to the GitHub Pages host, so `www` addresses redirect to the apex. The old site's `www` URLs are the ones search engines have indexed. **Leave the MX and SPF records alone**: info@ and patrick@ mail runs on Google Workspace. Wait until https://bayareatrackclub.org serves this site with a valid certificate.
4. **Then cancel Squarespace: the website plan only.** Keep the domain registration (it renews 2027-08-09) and Google Workspace, whichever account bills them. The old site's four pages are archived in `~/Developer/batc_archive/`; the 13 unlinked pages listed in its `REPORT.md` were not archived and disappear with the plan.

When it goes live, rewrite this section.

## Git

- **Never `git add` a directory** (`git add .`, `git add images`, `git commit -a`). Stage files by name.
- Commit only what the task asked for.

## Structure

- **One page for the program**: `index.html`. Sections in this order: what it is (`#about`), `#winter`, `#summer`, `#join`, `#coaches`, `#contact`. No further program pages unless the owner asks.
- **Coach bios live on their own pages** at `/<first>-<last>/index.html`: `/patrick-wales-dinan/` now, and `/kinsey-pogue/` once her bio exists. They serve a different search from the program page, which is why they're separate.
  - Each has its own `<title>`, meta description and canonical link, and is listed in `sitemap.xml`.
  - The home page's Coaches section stays short: photo, name, title, two or three sentences, and a link to the full bio.
- **The header and footer are the same on every page**, except the wordmark: `<h1 class="wordmark">` on the home page, `<p class="wordmark"><a href="/">` elsewhere. Nav links are root-absolute (`/#winter`), so they work from any page. Change the header or footer on every page in the same commit.
- **`sitemap.xml`** lists the home page and each coach page, and never the stubs. `robots.txt` points to it.
- **No favicon**, by the owner's decision. Each page with a header carries `<link rel="icon" href="data:,">` so browsers don't request `/favicon.ico`. The stubs don't, like the mvxctf stubs.
- **Redirect stubs** for the old Squarespace addresses, in the mvxctf stubs' pattern:
  - `about-batc.html` goes to `/#about`, `coaches.html` to `/#coaches`, and `sign-up.html` to `/#join`.
  - Each is a canonical link to the home page, an instant meta refresh and a visible link. No header, footer or stylesheet.
  - GitHub Pages serves `/coaches` from `coaches.html`, so the old addresses resolve without `.html`.
  - Leave them in place, and keep them out of any sitemap.
  - The other old addresses (`/home`, the 2017 blog and athlete pages) have no stub.
- `style.css` is the only stylesheet. No inline `style=""`, no `<style>` blocks.
- **No frameworks, no build step.** No JavaScript unless something genuinely needs it.
- **No third-party embeds**: no Google Fonts or CDN links, no map, Instagram or Facebook embeds, no analytics or tracking. Plain links out are fine. Fonts are self-hosted woff2 with their OFL licence.

## Paths

- **Root-absolute**: `/style.css`, `/images/2021-07-hillside-run.jpg`. Never relative paths, never `github.io` URLs.
- **Canonical host: `https://bayareatrackclub.org/`**, the apex, never `www` (the owner's choice). The old Squarespace site used `www`, so `www` must redirect to the apex once DNS moves. Full addresses only where a spec requires them: canonical links (on every page, including the stubs), Open Graph (none yet), `sitemap.xml` and `robots.txt`.

## Layout

- **Phone first.** The base CSS is the phone layout; wider layouts are added with `min-width` media queries.
- **Verify at 390px and 1280px** after every change, with no sideways scroll at 390. Check the server log for 404s.
  - 1280: `"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new --hide-scrollbars --window-size=1280,5000 --screenshot=<scratch dir>/1280.png http://localhost:8000/`. The layout uses no `vh` heights, so a tall window gives a true full-page shot.
  - 390: **`--window-size=390` doesn't work.** Chrome won't make a window narrower than 500px, so it lays the page out at 500 and crops the picture, which hides real overflow. Instead, screenshot a scratch page holding `<iframe src="http://localhost:8000/" width="390" height="6000">` at window width 500, and crop to 390. Measure overflow inside that iframe: `scrollWidth` must equal `clientWidth`.

## Identity

- **Not a Monte Vista property, and must not look like one.** No Monte Vista names, logos or uniforms in photos, no red accent, and none of the Monte Vista site's fonts (Archivo, Source Serif 4) or its look (condensed uppercase labels, warm off-white panels).
- Colours are the tokens at the top of `style.css`. Use them; don't add one-off colours.
- **Fonts**:
  - Fraunces 600 for the wordmark, headings and figures; Jost 400 and 600 for everything else.
  - They're self-hosted in `/fonts/` (latin subsets from @fontsource 5.3.0) with their OFL licences, and the page preloads Jost 400 and Fraunces 600.
  - Bold is 600; there is no 700, so the browser would fake it. Add a font file before using a new weight or italic.

## Content

- **Nothing invented.** Copy comes from the owner, or from the old site's archive once the owner has decided to keep it. Carry nothing over from the old site that hasn't been decided.
- **Gaps are marked, never filled with placeholder prose.** A missing piece is a `.gap` element saying what's missing (`<span class="gap">` inline). Unconfirmed copy carried over from the old site sits inside a `.confirm` block. Gaps in `<head>` are `<!-- GAP: ... -->` comments. Nothing goes live with any of the three.
- **Final copy** is verbatim and changes only on the owner's instruction. That covers the opening section (`#about`, what BATC is and who it's for, which has no heading), the Winter section, the Mammoth Lakes paragraph in Summer, and Patrick Wales-Dinan's bio, which is on `/patrick-wales-dinan/` in full with nothing hidden.
  - The bio links "Monte Vista High School" to https://montevistaxc.com/team/patrick-wales-dinan/ on purpose: a cross-domain link for search. It stays with the bio, on the bio page only. Keep the address exact; it is that page's canonical.
  - The home page summary is drawn from the bio's own opening paragraph, with no new claims. If the opening changes, check the summary.
- One fact, one place: a date or price is stated once. The old site gave the 5K two different dates. The club number, 38-1006, appears only in How to join, where people use it.
- Brandon Lawrence is off the site entirely. The Mammoth trip never shows a cost figure. There's no Twilight 5K (not scheduled for 2027) and no middle school line.
- **Email is patrick@bayareatrackclub.org everywhere on the site.** info@ isn't used, though its mailbox still exists (see Status, DNS).
- The Oak Hill Park map link is `https://www.google.com/maps/search/?api=1&query=37.843143%2C-121.984186`. Never a goo.gl short link.

## Photos

- **Originals live outside the repo**, in `~/Developer/batc_archive/images/` (listed in its `manifest.csv`). Never modify them. Repo copies in `images/` are derivatives; `README.md` maps each to its original.
- **Image metadata stripped losslessly, never by re-encoding.**
  - JPEG: `jpegtran -copy icc -optimize`, plus `-progressive` when the original is progressive. Match the scan type: Apple's decoder renders baseline and progressive versions of the same data slightly differently.
  - PNG: drop the ancillary chunks and keep IHDR, PLTE, tRNS, iCCP, sRGB, gAMA, cHRM, IDAT and IEND.
  - Check the Exif rotation flag before stripping, or the photo turns sideways.
  - `sips` keeps GPS and adds Exif of its own, so it is never the last step.
  - The Squarespace originals carry GPS coordinates.
- **Verify after stripping**: no Exif, XMP or IPTC remains, and the decoded pixels match the original. Hash the decoder's raw samples; a BMP or TIFF export carries DPI in its header and gives false mismatches.
- **Size**: in-page photos at most 1600px on the long edge; a full-bleed hero at least 1920px wide. If a photo must be resized, resize (one encode, quality about 82), then strip losslessly.
- **Photo credits**: the site's photos are Patrick Wales-Dinan's own and carry no credit line, by the owner's instruction (recorded in `README.md`, "Photos"). Don't flag them as credit-pending. A photo from anyone else is credited ("Photo: Name" in its `figcaption`, recorded in `README.md`) and doesn't go live until it is.

## Working style

- Report judgment calls rather than deciding silently: what you chose, and why.
- If an instruction contradicts what's on disk, stop and say so before acting.
- Say plainly when something didn't work or wasn't done.
