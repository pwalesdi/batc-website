# bayareatrackclub.org

The Bay Area Track Club's site: one static page for high school athletes and their parents, covering what the program is, when it runs, what it costs and how to join. Coach bios have their own pages, for people searching a coach's name.

**Live** at bayareatrackclub.org since 9 November 2026, on GitHub Pages from `main`. A push is public in about a minute, with no staging. See `CLAUDE.md`, "Status", for what's left: HTTPS, then cancelling the Squarespace website plan.

Preview: run `python3 -m http.server 8000` in this folder, then open http://localhost:8000/.

| File | What |
|---|---|
| `index.html` | The program page |
| `patrick-wales-dinan/index.html` | Patrick Wales-Dinan's full bio (`/patrick-wales-dinan/`) |
| `sitemap.xml`, `robots.txt` | For search engines: the home page and the coach pages, never the stubs |
| `CNAME` | GitHub Pages' custom domain, `bayareatrackclub.org`. Never delete or edit it |
| `style.css` | The only stylesheet |
| `images/` | Photos, the link-preview image and the Venmo QR, metadata stripped |
| `fonts/` | Fraunces and Jost (woff2) with their OFL licences |
| `about-batc.html`, `coaches.html`, `sign-up.html` | Redirect stubs for the old Squarespace addresses (see "Old addresses") |

## Photos

**The site's photos are Patrick Wales-Dinan's own, so they carry no credit line.** The owner confirmed this on 9 November 2026. Don't flag them as credit-pending. The exception is the coach portrait, whose photographer is unknown (see its row below).

Each repo copy below had its metadata stripped losslessly, and its decoded pixels were verified identical to its source. Sources are never modified.

| Repo file | On the page | Source | Taken |
|---|---|---|---|
| `images/2026-07-sierra-run-hero.jpg` | Hero on phones (under 760px) | `~/Developer/batc_archive/images/owner/2026-07-26-sierra-run.HEIC`, 4032 × 3024, an iPhone 14 Plus HEIC in Display P3, supplied by Patrick in November 2026. The 2560 × 1920 box from (280, 690), resized to 1296 × 972: the group head to toe, with the peaks behind. How it was made, and why it couldn't be lossless, is under the table. | 26 Jul 2026 |
| `images/2026-07-sierra-run-hero-wide.jpg` | Hero at 760px and wider: a banner the width of the text column (at most 1056px), never taller than half the window | The same source. The full-width 4032 × 1512 box from (0, 690), 8:3, resized to 2112 × 792: the sky above the peaks down to the runners' shins. No 8:3 box from this photo holds both the peaks and the feet. When the half-window cap shortens the banner, it loses sky and shin equally (`object-position` 50% 50%). **The shin cut is deliberate; don't revisit it.** On 9 November 2026 Patrick compared it with a crop that kept the runners whole, feet included. That crop lost the peaks' tips and, at 1280 × 720, needed the half-window cap removed. He chose this one. | 26 Jul 2026 |
| `images/2021-07-hillside-run.jpg` | Winter | `~/Developer/batc_archive/images/site-wide/instagram-4-CRb5WlxHA9p.jpeg`, 1440 × 1440. Squarespace's copy of an Instagram post; no metadata in the file. Shown 4:3 on the page (`object-fit`). | Posted 17 Jul 2021 |
| `images/coach-wales-dinan.jpg` | Coaches, and the top of `/patrick-wales-dinan/` | `~/Developer/mvxctf_website/assets/img/coaches/wales-dinan.jpg`, 710 × 887 (4:5). This is the Monte Vista site's coach card, cut from that repo's `2022-track-coach-wales-dinan.jpg`; reused on both sites by the owner's choice. **Photographer unknown, carried over from montevistaxc.com.** That doesn't block publishing it. If Patrick remembers who took it, add the credit. | 2022 track season |
| `images/link-preview.jpg` | Not on the page: it's the image shown when a page's link is shared (`og:image` and `twitter:image` on every page with a header) | Made from the Sierra run photo (`~/Developer/batc_archive/images/owner/2026-07-26-sierra-run.HEIC`, the hero's source), so it's a new image, not a stripped copy. A 2160 × 1890 box from (450, 700) of the sRGB decode (see below), resized to 720 × 630 (Lanczos), sits beside a 480px `--sun-amber` panel reading "BAY AREA / TRACK / CLUB" in the wordmark's style (Jost 600, capitals, letterspacing .2em, 60px, `--ink`). Rendered in headless Chrome at 1200 × 630, one JPEG encode (quality 88, 4:4:4 chroma), no metadata, 209 KB. Keep it under about 300 KB, WhatsApp's limit for previews. | 26 Jul 2026 (the photo) |
| `images/venmo-qr.png` | How to join (screens 760px and wider), shown 144px wide | `~/Developer/batc_archive/images/sign-up/MyVenmoQRCode.png`, a 978 × 1863 phone screenshot of Patrick's Venmo profile. Cut to the 659 × 659 square at (160, 801): the QR code plus its white quiet zone (4 modules). The avatar, name, handle, Venmo logo and caption are gone, because the Venmo button covers them. The crop was fully opaque, so the alpha channel was dropped. Its pixels match the source area exactly, and only the colour profile is kept. It decodes to the same payment link as the original (checked with Apple Vision), including from a 1× screenshot of the page. 324 KB. | Not a photo |

**How the Sierra run crops were made.** Only Safari shows HEIC, so the original can't be stripped losslessly and served as it is. Each crop therefore has one encode, the CLAUDE.md resize path:
1. Decode the standard image (the HDR gain map is ignored), and convert Display P3 to sRGB (relative colorimetric).
2. Crop, and resize with Lanczos.
3. Encode once as JPEG (quality 82, progressive, 4:2:0).
4. Run `jpegtran -copy icc -optimize -progressive`. The decoded pixels were checked unchanged by this step.

The results carry only a JFIF header: no Exif, XMP or IPTC. The original's GPS position, face regions and camera data are not in the repo. Sizes: phone crop 322 KB, wide crop 405 KB.

**Sharp at every size.** The wide crop is 2112px, the 1056px banner at 2× density. The phone crop is 1296px, a 432px-wide phone at 3×.

**The Monte Vista crest stays, by the owner's decision (9 November 2026).** The runner in the grey T-shirt wears a shield crest with Monte Vista's red Mustang. It's about 23px wide in the desktop banner, and it also shows in the link preview. This is an approved exception to CLAUDE.md's no-Monte-Vista-logos rule, for this photo only.

Earlier heroes:
1. The summer 2022 Mammoth Lakes group run (`home/gallery-07-IMG_9565.jpg`), swapped at the time for a photo of ordinary training. That was a preference, not a rule. The current hero is from the July 2026 Mammoth Lakes trip, and Patrick chose it knowing where it's from.
2. The hillside run, which moved to Winter.
3. The sunset crop (November 2026), which brought in the sunset palette. Neither sunset crop is in the repo any more. Their source is `~/Developer/batc_archive/images/site-wide/instagram-2-CfJsuSKJmDr.jpeg`; in the full frame, the shirtless foreground runner is the subject.

The Sierra run, from the July 2026 Mammoth Lakes trip, replaced the sunset crop in November 2026. The Summer section has no photo for now.

## Colours

The sunset palette, November 2026, replacing teal. It comes from the old site's banner (`~/Developer/batc_archive/images/home/banner-Golden_Gate_Bridge.jpeg`): deep orange through amber to yellow, the bridge's red as the accent, and dark slate for type. The old site's stylesheet was template greys; its warmth was all in that photo.

| Token | Hex | Use |
|---|---|---|
| `--paper` | #FFF6E6 | Page ground. Cream, deliberately: see CLAUDE.md, Identity |
| `--band` | #FFDB9A | Light amber: Winter and Coaches |
| `--sun-orange` | #F07A22 | Deep orange: Contact, step numbers |
| `--sun-amber` | #FBB124 | The header stripe, the link-preview panel |
| `--sun-yellow` | #FFD83A | The header stripe only. Never carries text |
| `--accent` | #C0362C | Bridge red: buttons, link underlines, focus rings |
| `--accent-ink` | #9E2B22 | Red for text: link and button hover |
| `--ink` | #222C33 | Dark slate: all type, the footer |
| `--ink-2` | #4A535B | Secondary slate: nav, coach roles |
| `--card` | #FFFFFF | How to join cards |
| `--line` | #E7C27E | Rules and card borders (decorative) |
| `--footer-ink` | #FFE6BA | Footer text |

Every text-on-background pair in use passes WCAG AA (4.5:1):

| Text | Background | Ratio | Where |
|---|---|---|---|
| `--ink` | `--paper` | 13.26 | Body text, headings, header |
| `--ink` | `--card` | 14.23 | How to join cards |
| `--ink` | `--band` | 10.74 | Winter, Coaches |
| `--ink` | `--sun-amber` | 7.73 | Link-preview wordmark |
| `--ink` | `--sun-orange` | 5.09 | Contact, step numerals |
| `--ink-2` | `--paper` | 7.31 | Nav |
| `--ink-2` | `--band` | 5.92 | Coach roles |
| white | `--accent` | 5.52 | Buttons |
| white | `--accent-ink` | 7.44 | Buttons, hover |
| `--accent-ink` | `--paper` | 6.94 | Link hover |
| `--accent-ink` | `--band` | 5.62 | Link hover |
| `--footer-ink` | `--ink` | 11.71 | Footer |

Non-text, 3:1 needed: `--accent` underlines and focus rings are 5.14 on `--paper` and 4.17 on `--band`. On `--sun-orange` they switch to `--ink` (5.09).

Never used, because they fail: `--ink-2` on `--sun-orange` (2.80), `--accent` on `--sun-orange` (1.97), `--accent-ink` on `--sun-orange` (2.66), and `--accent` as text on `--band` (4.17).

A new pair needs checking and adding here before use.

## Fonts

- **Jost** 600 in capitals, letterspaced .24em, for the wordmark. Jost is a Futura-style geometric sans, so the wide wordmark keeps the look of the old site's futura-pt title.
- **Fraunces** 600 for headings and figures.
- **Jost** 400 and 600 for everything else.

Both are latin subsets from @fontsource 5.3.0 (`fraunces-latin-600-normal.woff2`, `jost-latin-400-normal.woff2`, `jost-latin-600-normal.woff2`), under the SIL Open Font License 1.1. Their licences are `fonts/OFL-fraunces.txt` and `fonts/OFL-jost.txt`.

They replace the old site's freight-big-pro and futura-pt, which were licensed through Squarespace. The roles are deliberately the reverse of the Monte Vista site, which uses sans-serif headings over serif text.

## Old addresses

The old Squarespace pages people may have bookmarked each have a redirect stub that sends them to the matching section:

| Old address | Stub | Goes to |
|---|---|---|
| `/about-batc` | `about-batc.html` | `/#about` |
| `/coaches` | `coaches.html` | `/#coaches` |
| `/sign-up` | `sign-up.html` | `/#join` |

These follow the mvxctf stubs' pattern: a canonical link to `https://bayareatrackclub.org/`, an instant meta refresh and a visible link. They have no header or footer, and stay out of any sitemap.

No other old address has a stub. That covers `/home`, the 2017 blog and the athlete pages listed in `~/Developer/batc_archive/REPORT.md`, which will return 404.

## Settled (November 2026)

- **No Twilight 5K** on the page: it isn't scheduled for 2027.
- **No middle school line.**
- **Email**: patrick@bayareatrackclub.org everywhere on the site; info@ isn't used.
- **Photos**: Patrick's own, uncredited (see "Photos").
- **Mammoth Lakes trip**: one paragraph under Summer, with no cost figure.
- **Club number**: 38-1006 appears only in How to join.
- **Favicon**: none.
- **Checks**: the payee wording in How to join.
- **Palette**: the sunset palette (see "Colours"). Red is an accent only, in the bridge red, and the cream ground stays.
- **Hero**: the Sierra run, from the July 2026 Mammoth Lakes trip. Patrick's choice, made knowing where it's from. The desktop crop cuts the runners at the shins, by his choice over a feet-whole crop (see "Photos"). The Monte Vista crest on one runner's shirt stays (see "Photos").

## Outstanding

- **Kinsey Pogue**: the Coaches section shows only her name and "Assistant Coach". Her photo, a two- or three-sentence summary and her bio page at `/kinsey-pogue/` will follow once her bio exists.
- **Summer 2027**: the Summer section and its menu link are parked, commented out in the source and not shown. They stay that way until Patrick confirms the dates, location, days, times and price. The parked source keeps the gap, the "to confirm" block from the old site and the Mammoth Lakes paragraph. CLAUDE.md, "Summer section", says how to bring it back.

No gaps show on any page. The rendered-page check is in CLAUDE.md, "Status".
