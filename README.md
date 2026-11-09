# bayareatrackclub.org

The Bay Area Track Club's site: one static page for high school athletes and their parents, covering what the program is, when it runs, what it costs and how to join. Coach bios have their own pages, for people searching a coach's name.

**Not live.** The domain still points at Squarespace. See `CLAUDE.md`, "Status", for what has to happen first.

Preview: run `python3 -m http.server 8000` in this folder, then open http://localhost:8000/.

| File | What |
|---|---|
| `index.html` | The program page |
| `patrick-wales-dinan/index.html` | Patrick Wales-Dinan's full bio (`/patrick-wales-dinan/`) |
| `sitemap.xml`, `robots.txt` | For search engines: the home page and the coach pages, never the stubs |
| `style.css` | The only stylesheet |
| `images/` | Photos and the Venmo QR, metadata stripped |
| `fonts/` | Fraunces and Jost (woff2) with their OFL licences |
| `about-batc.html`, `coaches.html`, `sign-up.html` | Redirect stubs for the old Squarespace addresses (see "Old addresses") |

## Photos

The originals are in `~/Developer/batc_archive/images/` and are never modified. Each repo copy below had its metadata stripped losslessly, and its decoded pixels were verified identical to the original.

| Repo file | On the page | Original | Taken | Credit |
|---|---|---|---|---|
| `images/2021-07-hillside-run.jpg` | Hero | `site-wide/instagram-4-CRb5WlxHA9p.jpeg`, 1440 × 1440. Squarespace's copy of an Instagram post; no metadata in the file. | Posted 17 Jul 2021 | **Unknown: gap** |
| `images/2022-06-sunset-workout.jpg` | Winter | `site-wide/instagram-2-CfJsuSKJmDr.jpeg`, 1440 × 1080. Squarespace's copy of an Instagram post; no metadata in the file. | Posted 23 Jun 2022 | **Unknown: gap** |
| `images/venmo-qr.png` | How to join (screens 760px and wider) | `sign-up/MyVenmoQRCode.png`, 978 × 1863 phone screenshot. Dropped the `eXIf`, `pHYs` and `iDOT` chunks and kept the colour profile. | — | Not a photo |

**The hero is below the 1920px minimum.** It's 1440px wide, the size Instagram keeps. On phones, the main audience, it's sharp: a 390px-wide screen at 3× density needs 1170px. On a 1280px desktop it's shown slightly enlarged, and on high-density desktop screens about 1.8×, so it looks a little soft there. If the original phone photo turns up, replace this file with a version cut from it.

It replaced the summer 2022 Mammoth Lakes group-run photo (`home/gallery-07-IMG_9565.jpg`), so that the hero shows ordinary training. The Summer section has no photo for now.

## Fonts

- **Fraunces** 600 for the wordmark, headings and figures.
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

These follow the mvxctf stubs' pattern: a canonical link to `https://www.bayareatrackclub.org/`, an instant meta refresh and a visible link. They have no header or footer, and stay out of any sitemap.

No other old address has a stub. That covers `/home`, the 2017 blog and the athlete pages listed in `~/Developer/batc_archive/REPORT.md`, which will return 404.

## Open gaps

These are marked on the page: `.gap` elements are missing pieces, and the `.confirm` block is unconfirmed copy from the old site.

- What BATC is and who it's for (being written).
- Summer: dates; the middle school line (wording, year and contact address); the Mammoth Lakes trip wording (no cost figure); the Twilight 5000m date and time. Where, when and cost are carried over from the old site and need confirming.
- How to join: who checks are made out to.
- Coaches: Patrick Wales-Dinan's photo (not chosen; a gap on both the home page and his page). Kinsey Pogue's photo, summary and bio page (none exist yet).
- Photo credits for both photos.
- Favicon.
