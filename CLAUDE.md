# CLAUDE.md

Working rules for this repo. Photo sources, credits and the font decision are in `README.md`.

## Status

The site is **live at bayareatrackclub.org** (GitHub Pages, served from `main`, folder `/`), since 9 November 2026. A push to `main` is on the public web in about a minute. There is no staging, so test locally first: `python3 -m http.server 8000` from the repo root, then load the pages you touched at http://localhost:8000/ and check the server log for 404s. Never delete or edit `CNAME`.
- **No other preview exists.** https://pwalesdi.github.io/batc-website/ redirects to the domain, and root-absolute paths don't resolve from `file://`. The local server doesn't serve `/coaches` from `coaches.html` the way GitHub Pages does, so test the stubs locally as `/coaches.html`.
- **No gaps on any rendered page, before every push.** This must print nothing:
  `for f in $(git ls-files '*.html'); do perl -0777 -pe 's/<!--.*?-->//gs' "$f" | grep -HnE --label="$f" 'class="gap|class="confirm'; done; git grep -n 'GAP:' -- '*.html'`
  - The first part strips HTML comments before searching, because commented-out markup doesn't render. The parked Summer section's gap and "to confirm" block therefore don't count.
  - The second part catches `<!-- GAP: -->` notes, which are comments by design.
  - `README.md`, "Outstanding", lists what's still open.
- The repo is `origin`, https://github.com/pwalesdi/batc-website, and it's public. Note the hyphen: the local folder is `batc_website`, with an underscore. `gh` isn't installed here, so the owner changes repo and Pages settings on github.com.
- **DNS** is at Squarespace Domains, the registrar.
  - The apex's A records point at GitHub Pages: `185.199.108.153`, `185.199.109.153`, `185.199.110.153` and `185.199.111.153`.
  - `www` is a CNAME to `pwalesdi.github.io`, and GitHub redirects it to the apex.
  - **Leave the MX and SPF records alone**: info@ and patrick@ mail runs on Google Workspace.

Still to do, in this order:

1. **HTTPS.** GitHub issues a certificate for bayareatrackclub.org once it has seen the new DNS. Until then, https gives a certificate error and the site works over http only.
   - Once the certificate is issued, the owner ticks **Enforce HTTPS** in the repo's Pages settings.
   - Then check: https://bayareatrackclub.org/ and https://www.bayareatrackclub.org/ load with a valid certificate, and http redirects to https.
2. **Then cancel Squarespace: the website plan only.** Keep the domain registration (it renews 2027-08-09) and Google Workspace, whichever account bills them.
   - The old site's four pages are archived in `~/Developer/batc_archive/`.
   - The 13 unlinked pages listed in its `REPORT.md` were not archived, and disappear with the plan.

When both are done, delete this list.

## Git

- **Never `git add` a directory** (`git add .`, `git add images`, `git commit -a`). Stage files by name.
- Commit only what the task asked for.

## Structure

- **One page for the program**: `index.html`. Sections in this order: what it is (`#about`), `#winter`, `#summer` (parked, see "Summer section"), `#join`, `#coaches`, `#contact`. No further program pages unless the owner asks.
- **Coach bios live on their own pages** at `/<first>-<last>/index.html`: `/patrick-wales-dinan/` now, and `/kinsey-pogue/` once her bio exists. They serve a different search from the program page, which is why they're separate.
  - Each has its own `<title>`, meta description, canonical link and link-preview tags (see Paths), and is listed in `sitemap.xml`.
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
- **Canonical host: `https://bayareatrackclub.org/`**, the apex, never `www` (the owner's choice). The old Squarespace site used `www`, so `www` must redirect to the apex once DNS moves. Full addresses only where a spec requires them: canonical links (on every page, including the stubs), the link-preview tags, `sitemap.xml` and `robots.txt`.
- **Link previews (Open Graph and Twitter tags)** are on every page with a header, and never on the stubs.
  - The tags are `og:title`, `og:description`, `og:url`, `og:image` with its width, height and alt, `twitter:card` (`summary_large_image`) and `twitter:image`.
  - `og:title`, `og:description` and `og:url` repeat the page's `<title>`, meta description and canonical word for word. Change them together.
  - The image is `https://bayareatrackclub.org/images/link-preview.jpg` on every page (README, "Photos"). A new coach page gets the same set.

## Layout

- **Phone first.** The base CSS is the phone layout; wider layouts are added with `min-width` media queries.
- **Verify at 390px and 1280px** after every change, with no sideways scroll at 390. Check the server log for 404s.
  - 1280: `"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new --hide-scrollbars --window-size=1280,5000 --screenshot=<scratch dir>/1280.png http://localhost:8000/`. The layout uses no `vh` heights, so a tall window gives a true full-page shot.
  - 390: **`--window-size=390` doesn't work.** Chrome won't make a window narrower than 500px, so it lays the page out at 500 and crops the picture, which hides real overflow. Instead, screenshot a scratch page holding `<iframe src="http://localhost:8000/" width="390" height="6000">` at window width 500, and crop to 390. Measure overflow inside that iframe: `scrollWidth` must equal `clientWidth`.

## Identity

- **Not a Monte Vista property, and must not look like one.** No Monte Vista names, logos or uniforms in photos, and none of the Monte Vista site's fonts (Archivo, Source Serif 4) or its look (condensed uppercase labels, crimson on white, grey-white panels).
- **Red is permitted as an accent only**, in the bridge red `--accent` #C0362C, with `--accent-ink` #9E2B22 for red text.
  - Use it for buttons, link underlines and focus rings.
  - Never use it as the lead colour, a band or section background, or on headings, the header or the nav.
  - **Why the distinction matters:** Monte Vista's site leads with crimson (#C0102A) on white. This red-orange comes from the Golden Gate Bridge in the old site's banner. Kept small inside a sunset palette, it reads as part of the sunset. Give it a bigger role, or shift it toward crimson, and the two sites start to look alike.
- **The cream page ground, `--paper` #FFF6E6, is deliberate** (the owner's decision, November 2026). Monte Vista's panels are #F6F3F1, a greyer off-white. Under the orange palette, this one reads nothing like theirs.
- **Colours are the tokens at the top of `style.css`**: the sunset palette. `README.md`, "Colours", has the hex values and every contrast ratio. Use the tokens; don't add one-off colours.
  - Yellow never carries text; it's the stripe under the header.
  - Deep orange carries slate type only: no red, and no secondary slate.
  - Any new text-on-background pair needs 4.5:1. Check it and add it to the README table first.
- **Fonts**:
  - Jost 600 in capitals, letterspaced .24em, for the wordmark; Fraunces 600 for headings and figures; Jost 400 and 600 for everything else.
  - They're self-hosted in `/fonts/` (latin subsets from @fontsource 5.3.0) with their OFL licences. Each page with a header preloads Jost 400, Jost 600 (the wordmark) and Fraunces 600.
  - Bold is 600; there is no 700, so the browser would fake it. Add a font file before using a new weight or italic.

## Content

- **Nothing invented.** Copy comes from the owner, or from the old site's archive once the owner has decided to keep it. Carry nothing over from the old site that hasn't been decided.
- **Gaps are marked, never filled with placeholder prose.** A missing piece is a `.gap` element saying what's missing (`<span class="gap">` inline). Unconfirmed copy carried over from the old site sits inside a `.confirm` block. Gaps in `<head>` are `<!-- GAP: ... -->` comments. Nothing goes live with any of the three on a rendered page. Markup inside an HTML comment, like the parked Summer section, doesn't render.
- **Final copy** is verbatim and changes only on the owner's instruction. That covers the opening section (`#about`, what BATC is and who it's for, which has no heading), the Winter section, the Mammoth Lakes paragraph in Summer, the checks wording in How to join, and Patrick Wales-Dinan's bio, which is on `/patrick-wales-dinan/` in full with nothing hidden.
  - The bio links "Monte Vista High School" to https://montevistaxc.com/team/patrick-wales-dinan/ on purpose: a cross-domain link for search. It stays with the bio, on the bio page only. Keep the address exact; it is that page's canonical.
  - The home page summary is drawn from the bio's own opening paragraph, with no new claims. If the opening changes, check the summary.
- One fact, one place: a date or price is stated once. The old site gave the 5K two different dates. The club number, 38-1006, appears only in How to join, where people use it.
- Brandon Lawrence is off the site entirely. The Mammoth trip never shows a cost figure. There's no Twilight 5K (not scheduled for 2027) and no middle school line.
- **Email is patrick@bayareatrackclub.org everywhere on the site.** info@ isn't used, though its mailbox still exists (see Status, DNS).
- The Oak Hill Park map link is `https://www.google.com/maps/search/?api=1&query=37.843143%2C-121.984186`. Never a goo.gl short link.

## Summer section (parked)

The Summer section and its menu link are commented out on every page with a header until the 2027 summer program is set. The opening section already tells readers that summer runs from June into August.

The full source is kept in `index.html`, between `<!-- PARKED: the Summer section` and `END PARKED Summer section -->`:
- the "Summer dates" gap
- the "From the old site · to confirm" block (Oak Hill Park, Monday through Saturday 7:45am, $500)
- the final Mammoth Lakes paragraph

**To bring it back, the owner must confirm all five: the 2027 dates, the location, the days, the times and the price.** Then, in one commit:

1. Replace the gap and the `.confirm` block with the confirmed copy, leaving no markers.
2. Remove the comment wrapper around the section, and the one around the Summer menu link on every page with a header, so the headers stay identical.
3. Check that the opening section's "from June into August" still agrees with the dates.
4. Recheck the section colours, so no two neighbouring sections share a background.
   - Now, with Summer parked: about on paper, Winter `band`, How to join on paper, Coaches `band`, Contact `band-deep`.
   - With Summer back between Winter and How to join: Summer on paper, How to join `band`, Coaches on paper. Contact stays `band-deep`.
5. Verify at 390 and 1280, and run the gap check in Status.

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
- **Photo credits**: the site's photos are Patrick Wales-Dinan's own and carry no credit line, by the owner's instruction (recorded in `README.md`, "Photos"). Don't flag them as credit-pending. A photo by anyone else:
  - **Known photographer**: must be credited before the photo is pushed, as "Photo: Name" in its `figcaption` and recorded in `README.md`.
  - **Unknown photographer**: recorded as unknown in `README.md`. That doesn't block pushing it.
  - If an unknown photographer becomes known, add the credit. That applies to the coach portrait, if Patrick remembers who took it.

## Working style

- Report judgment calls rather than deciding silently: what you chose, and why.
- If an instruction contradicts what's on disk, stop and say so before acting.
- Say plainly when something didn't work or wasn't done.
