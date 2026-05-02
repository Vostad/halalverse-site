# Digital Finance Alliance — Site Audit

**Audited:** 2026-05-01
**Auditor:** Claude (read-only sweep, no changes)
**Project root:** `/Users/zahidvostad/Downloads/Claude Projects/dfa-fork`

---

## 1. Project Setup & Where Things Live

| | |
|---|---|
| **Framework** | None. Vanilla HTML / CSS / JS. |
| **Language** | HTML5 + CSS3 + ES5-style JS (inline `<script>` IIFEs). No TypeScript. |
| **Styling system** | Per-page **inline `<style>` blocks** (~95% of CSS lives there) + **one shared `image-system.css`** stylesheet (~290 lines, image-frame utilities). No Tailwind, no preprocessor, no PostCSS. |
| **Package manager** | None. No `package.json`, no `node_modules`, no lockfile. |
| **Disk path** | `/Users/zahidvostad/Downloads/Claude Projects/dfa-fork` (sibling of read-only `cw-repo/` and `dfa-repo/`) |
| **Dev server** | `python3 -m http.server 8002` (run from project root). Saved to `.claude/launch.json`. |
| **Build command** | None. Files served as-is. |
| **Build output** | N/A — no build step. |
| **Git status** | **Not a git repo.** No `.git` directory. No remote, no branch, no commit history. Fork lives outside version control. |
| **Deployment** | Configured for **Vercel** via `vercel.json` (`cleanUrls:true`, `trailingSlash:false`) — but **not yet deployed**. No `.vercel` folder, no project linked. |

---

## 2. File Structure Map

```
dfa-fork/
├── .claude/                       # Claude config (just launch.json so far)
│   └── launch.json                # python3 http.server config
├── about/                         # 7 VOSTAD timeline photos (vostad-2013.jpg → vostad-today.jpg)
├── assemblies/                    # Event card images + assemblies-hero video
│   ├── abu-dhabi.jpg              # real DFA skyline (sourced from dfa-repo)
│   ├── riyadh.jpg                 # PLACEHOLDER (copy of abu-dhabi)
│   ├── singapore.jpg              # PLACEHOLDER (copy of abu-dhabi)
│   └── assemblies-hero.compressed.mp4
├── attendees-logo/                # 18 partner logos (1.png … 18.png) — DFA partners, color
├── brochure/                      # Locked DFA Abu Dhabi 2026 sponsorship PDF (124 KB)
├── council/                       # Carryover from CW — discussion.jpg, value.jpg
├── events/                        # Event detail pages (3)
│   ├── abu-dhabi.html             # canonical 10-section template
│   ├── riyadh.html                # parity with Abu Dhabi, Riyadh copy
│   └── singapore.html             # ⚠️ STALE — still on old CW structure
├── images/
│   ├── dfa/                       # Brand assets: 3 SVG logos (white/dark/color), 3 favicons (legacy, orphan), 1 og-image, 2 lockup variants (orphan)
│   ├── speakers/                  # 15 speaker portraits (10 .webp + 5 .jpg)
│   ├── card-attend.jpg            # apply-section image (placeholder)
│   ├── card-speak.jpg             # apply-section image (placeholder)
│   ├── card-partner.jpg           # apply-section image (placeholder)
│   ├── discussion-01.jpg          # CW carryover used as placeholder in 4 places
│   ├── discussion-02.jpg          # CW carryover, placeholder
│   ├── awards-1.jpg               # ORPHAN (referenced nowhere)
│   ├── awards-2.jpg               # used in awards page Global Stage section
│   └── awards-hero.compressed.mp4 # awards page hero video
├── favicon.ico                    # New DFA brand
├── favicon-16x16.png
├── favicon-32x32.png
├── favicon-48x48.png
├── apple-touch-icon.png
├── android-chrome-192x192.png
├── android-chrome-512x512.png
├── site.webmanifest               # PWA manifest, theme #0E1830
├── hero-video-com.compressed.mp4  # homepage hero video (CW reused)
├── authority.jpg                  # homepage hero <video poster> fallback
├── image-system.css               # only external stylesheet (image utilities)
├── vercel.json                    # cleanUrls + trailingSlash config
├── index.html                     # homepage
├── about.html
├── events.html                    # events index
├── ledger.html                    # the Ledger (was Council)
├── contact.html
└── digital-finance-awards.html    # was Davos page
```

---

## 3. Pages / Routes Built

| URL (Vercel cleanUrl) | Backing file | Status | One-liner |
|---|---|---|---|
| `/` | `index.html` | ✅ Complete | Homepage — hero, trust grid, 3-card events, authority, how-it-works, voices, access CTA, final strip, footer |
| `/about` | `about.html` | ✅ Complete | VOSTAD origin story, 7-row timeline (1 row points to DFA), 4 stats, trust grid, final statement |
| `/events` | `events.html` | ✅ Complete | Events index — 3 city cards, "What Happens at Events", "Who Attends", trust grid |
| `/ledger` | `ledger.html` | ✅ Complete | Ledger landing — about-the-ledger split, logo marquee, email-only Notify form |
| `/contact` | `contact.html` | ✅ Complete | 3-column contact paths (Request Access / Events / Awards) + general inquiry form |
| `/digital-finance-awards` | `digital-finance-awards.html` | ⚠️ Complete with broken form | Awards landing — recognized dimensions, global stage, **2 nomination forms wired to placeholder Formspree** (mxxxxxxx — submissions will 404) |
| `/events/abu-dhabi` | `events/abu-dhabi.html` | ✅ Complete | 10-section event detail — hero, 2 marquees (logos + speakers), market reality, why summit, key themes, who attends, apply, testimonials, final CTA |
| `/events/riyadh` | `events/riyadh.html` | ✅ Complete | Identical structure to Abu Dhabi, Riyadh-specific copy |
| `/events/singapore` | `events/singapore.html` | 🚧 **Structurally stale** | Still on old CW 6-section structure (positioning/themes/who-attends/beyond/trust/dubai-final). Color tokens updated but page architecture is 2 generations behind Abu Dhabi/Riyadh. |
| `/request-access` | **MISSING** | ❌ Does not exist in fork | Referenced from 40+ links across all pages. Expected to come from the legacy `dfa-repo` at deploy time, or needs to be created here. |

**Total pages:** 9 in fork + 1 missing dependency.

---

## 4. Components Built

This is a vanilla site — there are **no JavaScript components**. There are reusable **CSS-defined visual patterns** that recur via copy-paste markup. Listing them as "components" anyway, since they're the de-facto building blocks:

| Pattern | Selector(s) | Where used | Status |
|---|---|---|---|
| **Nav** (fixed, dark gradient → opaque on scroll) | `.nav`, `.nav-inner`, `.nav-links`, `.nav-cta` | Every page | ✅ |
| **Mobile menu** (full-screen overlay) | `.mobile-menu`, `.mobile-menu-list` | Every page | ✅ |
| **Hero** (full-bleed video + scrim) | `.hero`, `.dubai-hero`, `.council-page-hero`, `.davos-hero` | Homepage, event pages, ledger, awards | ✅ |
| **Section header** (eyebrow + H2) | `.section-header`, `.section-eyebrow`, `.section-title` | New event-page sections | ✅ |
| **Card grid** (3-col, hairline gap, mono number) | `.cards-grid`, `.cards-grid--three`, `.card`, `.card-number` | Event pages (Market Reality, Key Themes) | ✅ Padding fix applied (scoped via `.cards-grid .card`) |
| **Apply-CTA card** (image-anchored, hover lift) | `.apply-cta-grid`, `.apply-cta-card`, `.apply-cta-image` | Event pages apply section | ✅ |
| **Two-column split** (text + image) | `.split-2`, `.split-text`, `.split-image` | Why Summit section | ✅ Image is placeholder |
| **70/30 audience split** | `.audience-split`, `.audience-primary/secondary`, `.audience-tag` | Event pages Who Will Attend | ✅ |
| **Bullet list with green-rule pseudo-element** | `.bullet-list` | Why Summit, Who Will Attend | ✅ |
| **Featured-marquee** (color logo carousel, cream bg) | `.featured-marquee`, `.featured-marquee__track` | Event pages (above speakers marquee) | ✅ |
| **Speakers-marquee** (monochrome portrait carousel, cream bg, green edition rule) | `.speakers-marquee`, `.speakers-marquee__card`, `.speakers-marquee__edition::before` | Event pages | ✅ Hardcoded 15 speakers, all 3 event pages share the same roster |
| **Testimonial thumbnail row** | `.testimonial-row`, `.testimonial-card`, `.testimonial-thumb`, `.testimonial-play` | Event pages | ⚠️ All 3 thumbnails + 3 YouTube URLs are placeholders |
| **Final CTA band** (cerulean bg, white text) | `.final-cta`, `.final-cta-headline`, `.btn-on-accent` | Event pages | ✅ |
| **Form** (Formspree-handled) | `.inquiry-form`, `.access-form`, `.nom-form` | contact.html, ledger.html, digital-finance-awards.html | ✅ Contact + Ledger live; ⚠️ Awards on placeholder endpoint |
| **Footer** (4-col grid) | `<footer>`, `.footer-grid`, `.footer-col` | Every page | ✅ |
| **Buttons** | `.btn-primary`, `.btn-secondary`, `.btn-ghost`, `.btn-on-accent`, `.btn-on-dark` | Hero, CTAs, forms | ✅ |

**Inline JS IIFEs** present on every page (none reusable across pages — copy-pasted):

| IIFE | What it does | Pages |
|---|---|---|
| Nav scroll-state | Toggles `.is-scrolled` on `<nav>` past 40px scroll | All |
| Mobile-menu toggle | Open/close hamburger overlay, Esc-key close, body-scroll lock | All |
| Reveal-on-scroll | `IntersectionObserver` adds `.is-visible` to `.reveal` / `.reveal-stagger` elements | Most (not contact, not ledger) |
| Formspree handler | `fetch()` POST, replaces form with success message, error handling | contact, ledger, awards |
| Awards tab toggle | Switches between Nominate / Request Access form panels | awards page only |

---

## 5. Brand & Design System State

### Tokens (CSS custom properties on `:root`)

**Defined inline at the top of every HTML file's `<style>` block** (no shared tokens file — each page has its own `:root` declaration). 19 properties:

```css
--white: #FFFFFF
--light-grey: #F4F6F8
--soft-grey: #E7EBF0
--cream: #FAF6F2          /* primary cream section bg */
--text: #0F1720           /* alias: --text-primary */
--text-secondary: #5B6470 /* alias: --text-muted */
--blue: #1C3553
--blue-2: #2A4A6A
--blue-deep: #0F2236      /* dark hero / dark sections */
--blue-tint: #EDF3F8
--accent: #1F6FB0         /* sovereign cerulean — brand */
--accent-hover: #5BA3D9
--accent-micro: #1F6FB0
--border: rgba(15,23,32,0.08)
--max: 1240px
--content: 1160px
--pad: 120px (responsive: 100/84/72)
--text-muted: var(--text-secondary)
--text-primary: var(--text)
```

**Drift risk:** since tokens are duplicated per file, a token change requires editing all 9 files. There's no single source of truth. Recently bitten by this when missing `--blue-deep` was discovered on 6 of 7 interior pages (now fixed).

### Fonts

- **Loaded:** Inter (Google Fonts) — weights 300/400/500/600/700.
- **Mono fallback chain:** `'JetBrains Mono', 'SF Mono', Menlo, monospace` — used for eyebrows, card numbers, edition labels. **JetBrains Mono is NOT loaded** as a webfont; users see SF Mono on Mac, Menlo elsewhere.
- **Aspirational fallbacks** in body font stack (`Söhne`, `Neue Haas Grotesk`, `General Sans`) — listed but not loaded.

### Logos (just installed today)

| Slot | File | Status |
|---|---|---|
| Nav (white-on-dark) | `images/dfa/logo-white.svg` (1014×320 stacked lockup) | ✅ Wired up (40px height; 32px on mobile) |
| Mobile-menu bar | Same `logo-white.svg` | ✅ Wired up |
| Footer (navy-on-cream) | `images/dfa/logo-dark.svg` | ✅ Wired up (36px height) |

The brand-text `<span>` (which used to render "Digital Finance Alliance" twice) was removed — the lockup SVG now carries the wordmark. ✅

### Favicon / PWA

| Slot | File | Status |
|---|---|---|
| `/favicon.ico` | multi-size | ✅ |
| 16/32/48px PNG | favicon-{16,32,48}x{16,32,48}.png | ✅ |
| iOS home-screen | apple-touch-icon.png | ✅ |
| PWA Android | android-chrome-{192,512}x{192,512}.png | ✅ |
| Manifest | site.webmanifest (theme #0E1830, bg #0E1830) | ✅ |
| `<meta name="theme-color">` | Set on every page | ✅ |

### Honest assessment of the design system

- **Positives:** Tokens are named consistently, sharp 0px corners are enforced site-wide via `image-system.css`, button variants are distinct, mono caps for eyebrows reads institutional. Cerulean accent appears predictably in CTAs, hover states, edition rules.
- **Negatives:**
  - **No shared CSS file for tokens** — each page redefines `:root`. A real design system would extract tokens to a `tokens.css` and link it (which would also save ~70 lines per page).
  - **CSS class names retain CW lineage**: `.dubai-hero`, `.dubai-final`, `.davos-hero`, `.davos-positioning`, `.council-page-hero` are still in the markup. They function correctly but bear DFA's commodity-trading ancestor's name. Cosmetic but worth a renaming pass before launch.
  - **Dead CW CSS** at lines ~610–625 of every event page (`.card`, `.card:first-child`, `.card:last-child`, `.card + .card`) is still present, defeated only by the newer `.cards-grid .card` scoping. Cleanup opportunity.
  - **Inline `<style>` everywhere** — slow first-paint cost amortized across 1500–2800 lines per page, no caching benefit. Acceptable for low-page-count marketing site, but worth knowing.

---

## 6. What's Actually Working vs. Broken

### Top-level pages

| Page | Status | Notes |
|---|---|---|
| `/` (homepage) | ✅ Working | All sections render, all internal links resolve except `/request-access`. |
| `/about` | ✅ Working | Timeline reads cleanly, 4 stats, logo grid present. |
| `/events` | ✅ Working | Hero, 3 event cards link to detail pages, what-happens grid, who-attends list, trust grid. |
| `/ledger` | ✅ Working | Hero, about-the-ledger split, logo marquee animates, Notify form posts to Formspree `mdaybbbp`. |
| `/contact` | ✅ Working | 3-col path cards, inquiry form posts to Formspree `xbdqwwwk`. |
| `/digital-finance-awards` | ⚠️ Form broken | Page renders fine BUT both forms POST to `formspree.io/f/mxxxxxxx` which is a placeholder ID. Submissions will 404 silently and trigger the "Something went wrong" error UX. |
| `/events/abu-dhabi` | ✅ Working | Canonical 10-section template. All sections render, marquees animate, hover states work. |
| `/events/riyadh` | ✅ Working | Same as Abu Dhabi with Riyadh copy. |
| `/events/singapore` | 🚧 Structurally stale | Page loads (HTTP 200), but it's the OLD CW 6-section structure (positioning/themes/who-attends/beyond/trust/dubai-final). Doesn't have any of the 7 new market-driven sections. Color tokens were updated to cerulean but the architecture is 2 generations behind its sibling pages. |

### Universal / cross-page

| | Status | Notes |
|---|---|---|
| Brand logos in nav/footer | ✅ Working | Stacked lockup, white in nav, navy in footer. Heights 40/36/32px. |
| Favicons & manifest | ✅ Working | All 7 favicon variants serve 200, manifest is valid JSON, theme-color set. |
| `request-access.html` link target | ❌ **Broken** | Referenced from **40+ places** (top hero CTAs, footer columns, contact paths, apply cards, final CTA). All 404 in the fork. Intentional cross-project link expected to be merged from `dfa-repo` at deploy time, or needs to be created here. |
| Console errors | ✅ None observed | No `console.log`, no `debugger`, no `alert` in any HTML/JS. |
| Mobile responsive | ✅ Mostly works | All pages have `@media (max-width: 768px)` overrides for grids, padding, font sizes. Singapore is on old responsive rules (different from new sections). |
| Accessibility — alt text | ⚠️ Partial | 367 `<img>` tags total: 0 missing alt, 224 use `alt=""` (acceptable for decorative — partner logos and speaker marquee duplicates), 143 have descriptive alt text. |
| Accessibility — aria | ⚠️ Partial | `aria-current="page"` is set on most active nav links, mobile-menu has `aria-hidden`/`aria-expanded` toggling. Missing: skip-to-content link, form fieldset legends, role attributes on custom tab/marquee patterns. |
| Accessibility — keyboard | ⚠️ Likely fine | All CTAs are real `<a>` or `<button>` elements (not div clicks). Mobile-menu close on Esc. Awards tabs are `<button role="tab">` with `aria-selected`. |
| Performance | ⚠️ Image-heavy | Hero videos load eagerly (1.4 MB / 3 MB / 3 MB), partner logos × 18 + speaker portraits × 15 = 33 raster files per event page. `loading="lazy"` is on marquee imgs and most card imgs. No lazy loading on hero videos. |

---

## 7. Hooked Up to Real Data vs. Hardcoded

**Everything is hardcoded.** No CMS, no database, no API, no JSON data files. Content lives in the HTML markup itself.

### Forms (only "real data" surface)

| Form | Endpoint | Status |
|---|---|---|
| Contact inquiry (5 fields) | `formspree.io/f/xbdqwwwk` | ✅ Live (verified existing in `dfa-repo`) |
| Ledger Notify (email-only) | `formspree.io/f/mdaybbbp` | ✅ Live |
| Awards Nominate | `formspree.io/f/mxxxxxxx` | ❌ Placeholder — submissions will fail |
| Awards Request Access | `formspree.io/f/mxxxxxxx` | ❌ Same — placeholder |

### Hardcoded content inventory

- All copy on every page — heroes, section bodies, CTAs, footer
- 18 partner logos in trust grids (real DFA partner files, color)
- 15 speaker entries (name, role, organization, photo, edition year) — duplicated identically across all 3 event pages
- 6 cards each in Market Reality + Key Themes sections
- 4 timeline rows of factually-true VOSTAD history (kept verbatim from CW source)
- All testimonial YouTube URLs (`PLACEHOLDER1/2/3`)
- Footer email `hello@digitalfinancealliance.com`
- All canonical URLs `https://digitalfinancealliance.com/...`

---

## 8. What's NOT Built Yet

**Concrete missing pieces** for an institutional event site to be launch-ready:

| Missing | Severity |
|---|---|
| `request-access.html` page | 🔴 Critical (40+ broken links) |
| Real Formspree endpoint for Awards forms | 🔴 Critical (forms silently fail) |
| Singapore page — market-driven 10-section rebuild | 🔴 Critical (visible inconsistency vs sibling pages) |
| Real testimonial YouTube videos + thumbnails | 🟡 Visible placeholder |
| Real Riyadh + Singapore skyline imagery | 🟡 Visible placeholder (currently using Abu Dhabi for all 3) |
| Real DFA event photography for Why Summit + Beyond split sections | 🟡 Visible placeholder (currently `discussion-01.jpg` from CW) |
| Sitemap.xml | 🟡 SEO baseline missing |
| robots.txt | 🟡 SEO baseline missing |
| 404 page (`404.html`) | 🟡 Missing — Vercel will fall back to default plain page |
| Open Graph image at `/images/dfa/og-image.jpg` | ✅ Exists, all pages reference it |
| Per-page custom OG images (event-specific) | 🟢 Nice-to-have, all pages currently share one OG |
| Newsletter / email capture beyond Ledger Notify | 🟢 Nice-to-have |
| Analytics — GA4, Plausible, or similar | 🟡 None installed; pre-launch decision |
| Cookie consent banner / privacy policy | 🟡 Required if shipping to EU/UAE residents |
| Speaker detail pages (currently marquee only) | 🟢 Nice-to-have — pattern supports it |
| Per-event agenda page | 🟢 Nice-to-have — none exist |
| Per-event sponsor inquiry flow distinct from "Apply to Partner" | 🟢 Nice-to-have |
| Multi-language (en/ar) for MENA audience | 🟢 Strategic decision, not started |
| Search functionality | 🟢 Static site — would need indexing |
| Vercel project linked + first deployment | 🔴 Site is local-only |

---

## 9. Dependencies & Risks

### Dependencies

- **Zero third-party JS dependencies.** No npm packages, no CDN libraries.
- **One external resource:** Google Fonts (Inter) via `https://fonts.googleapis.com/css2?...` and `https://fonts.gstatic.com`. Both `<link rel="preconnect">` declared.
- **One inline external script tag:** none. (Verified — 0 `<script src=...>` references across all pages.)

### TODO / FIXME / PLACEHOLDER inventory (26 hits across the codebase)

| Location | Type | Description |
|---|---|---|
| `index.html:1035` | PLACEHOLDER | Riyadh skyline image — replace `assemblies/riyadh.jpg` |
| `index.html:1053` | PLACEHOLDER | Singapore skyline image — replace `assemblies/singapore.jpg` |
| `index.html:1143` | PLACEHOLDER | Voices quotes (rewritten CW originals) |
| `events.html:1202` | PLACEHOLDER | Riyadh skyline (events index) |
| `events.html:1216` | PLACEHOLDER | Singapore skyline (events index) |
| `ledger.html:1340` | TODO | Replace `council/discussion.jpg` with DFA-specific photo |
| `digital-finance-awards.html:1677` | TODO | Replace `images/awards-2.jpg` with DFA-specific awards photo |
| `digital-finance-awards.html:1699` | TODO | **Create real Formspree project, replace `mxxxxxxx`** |
| `events/abu-dhabi.html:2515` | TODO | Why-Summit `discussion-01.jpg` → DFA event photo |
| `events/abu-dhabi.html:2604` | TODO | Apply-section card images (3 × placeholders) |
| `events/abu-dhabi.html:2652–2670` | TODO | 3 testimonial YouTube URLs (`?v=PLACEHOLDER1/2/3`) |
| `events/riyadh.html:2516` | TODO | Same Why-Summit image TODO |
| `events/riyadh.html:2605` | TODO | Same apply-card images TODO |
| `events/riyadh.html:2653–2670` | TODO | Same 3 YouTube URLs |
| `events/singapore.html:2063` | TODO | Old CW positioning section image — N/A after rebuild |

### Other risk findings

- **No `console.log`, `debugger`, or `alert`** in any code. Clean.
- **No hardcoded API keys, credentials, or `.env` references.** Formspree IDs are public form IDs (acceptable in client-side code).
- **`.DS_Store` files** at root (10 KB) and possibly in subdirectories — macOS metadata, should be `.gitignore`'d **if** the project ever gets git-tracked.
- **Orphan assets** (in repo but not referenced anywhere): 11 files
  - `council/value.jpg`
  - `images/awards-1.jpg`
  - `images/dfa/favicon-{16,32,180}.png` (legacy CW favicons, replaced by new `favicon-*.png` at root)
  - `images/dfa/lockup-dfa.svg`, `lockup-dfs.svg` (early DFA brand experiments)
  - `images/dfa/logo-color.png` and `.svg` (full color brand variant — installed but not currently used)
  - `images/dfa/logo-dark.png`, `logo-white.png` (raster fallbacks — SVG is what's wired up)
- **Dead CW CSS** at lines ~610–625 of each event page: `.card:first-child`, `.card:last-child`, `.card + .card`, `.card:hover`. Functionally defeated by the newer `.cards-grid .card` scoping; cosmetically still in the file. ~15 lines × 3 event pages.
- **Stale CSS class names**: `.dubai-hero`, `.dubai-final`, `.davos-hero`, `.davos-positioning`, `.davos-final-statement`, `.council-page-hero` — function correctly, document the page's CW lineage.
- **No git** = no history, no rollback, no blame, no diff. Substantial risk for a multi-person project. Initialize a repo before further work.

---

## 10. Recommendation: Top 5 Things to Fix First

In priority order (impact × ease):

### 1. 🔴 Resolve `request-access.html` (Critical — 40+ broken links)
Either:
- **(a) Create `request-access.html`** in this fork — likely a single form page with the existing DFA Formspree endpoint `xjgjllla` (from the legacy `dfa-repo`). 1–2 hours.
- **(b) Set up a Vercel rewrite/redirect** in `vercel.json` to route `/request-access` to the legacy DFA project's URL. 15 minutes if the legacy project is already deployed.

This is the single biggest visible gap. Every "Apply to Attend" button currently 404s locally.

### 2. 🔴 Rebuild Singapore page to match Abu Dhabi / Riyadh
Singapore is the only event page on the old CW 6-section structure. It looks visibly different from its siblings — same hero/marquee treatment but old content scaffold below. ~30 minutes following the same `cp abu-dhabi.html → singapore.html` pattern then applying Singapore-specific copy overrides (which the brief in chat memory has the spec for).

### 3. 🔴 Provision a real Formspree project for the Awards page
Both `.nom-form` instances on `digital-finance-awards.html` POST to `formspree.io/f/mxxxxxxx`. Submissions will fail silently and show the user the error message. Sign up for a Formspree project, swap the placeholder ID, and update both `_subject` hidden inputs if the new Formspree dashboard expects different conventions. 30 minutes.

### 4. 🟡 Initialize git + first deployment to Vercel
Right now there's no version control and no live URL. A single `git init && git add -A && git commit -m "DFA fork initial commit"` + `vercel deploy` would establish:
- A rollback safety net
- A shareable preview URL for stakeholders
- Auto-deployments on future commits
- Resolves request-access.html if the legacy project is also Vercel-deployed under the same domain

### 5. 🟡 Extract `:root` tokens to a shared `tokens.css` file
Right now a token change (color, spacing, font) means editing 9 files. This is precisely how the missing-`--blue-deep` and orange→cerulean swap caused friction recently. Extracting to a single file and linking it from each page's `<head>` would:
- Make brand updates a one-file change
- Reduce ~70 lines of duplication per page
- Give a real "single source of truth" for design tokens

A modest refactor (~1 hour). Pairs nicely with #4 since both are pre-launch hygiene.

---

### Honorable mentions (do these next, not first)

- Replace 6+ placeholder images (Riyadh/Singapore skylines, event photos, voices, testimonial thumbs)
- Add real testimonial YouTube videos
- Add Open Graph per-event images (currently all pages share one OG image)
- Add `sitemap.xml`, `robots.txt`, `404.html`
- Decide on analytics (GA4 vs Plausible vs none) and install
- Rename `.dubai-*` and `.davos-*` CSS classes to event-neutral names for self-documentation
- Delete dead CW `.card:first-child` / `:last-child` / sibling rules from the event pages
- Delete 11 orphan asset files
- Add a skip-to-content link for accessibility

---

**End of audit.**
