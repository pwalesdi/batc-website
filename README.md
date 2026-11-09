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

**The site's photos are Patrick Wales-Dinan's own, so they carry no credit line.** The owner confirmed this on 9 November 2026. Don't flag them as credit-pending.

Each repo copy below had its metadata stripped losslessly, and its decoded pixels were verified identical to its source. Sources are never modified.

| Repo file | On the page | Source | Taken |
|---|---|---|---|
| `images/2021-07-hillside-run.jpg` | Hero | `~/Developer/batc_archive/images/site-wide/instagram-4-CRb5WlxHA9p.jpeg`, 1440 × 1440. Squarespace's copy of an Instagram post; no metadata in the file. | Posted 17 Jul 2021 |
| `images/2022-06-sunset-workout.jpg` | Winter | `~/Developer/batc_archive/images/site-wide/instagram-2-CfJsuSKJmDr.jpeg`, 1440 × 1080. Squarespace's copy of an Instagram post; no metadata in the file. | Posted 23 Jun 2022 |
| `images/coach-wales-dinan.jpg` | Coaches, and the top of `/patrick-wales-dinan/` | `~/Developer/mvxctf_website/assets/img/coaches/wales-dinan.jpg`, 710 × 887 (4:5). This is the Monte Vista site's coach card, cut from that repo's `2022-track-coach-wales-dinan.jpg`; reused on both sites by the owner's choice. It's a photo of Patrick, so not taken by him, and neither site records the photographer. | 2022 track season |
| `images/venmo-qr.png` | How to join (screens 760px and wider) | `~/Developer/batc_archive/images/sign-up/MyVenmoQRCode.png`, 978 × 1863 phone screenshot. Dropped the `eXIf`, `pHYs` and `iDOT` chunks and kept the colour profile. | Not a photo |

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

## Outstanding

- **Kinsey Pogue**: the Coaches section shows only her name and "Assistant Coach". Her photo, a two- or three-sentence summary and her bio page at `/kinsey-pogue/` will follow once her bio exists.

Still marked on the page (`.gap` is a missing piece; `.confirm` is unconfirmed copy from the old site):

- **Summer 2027 dates**: unknown.
- **Summer details**: where, when and cost, carried over from the old site and not yet confirmed.
- **How to join**: who checks are made out to.
