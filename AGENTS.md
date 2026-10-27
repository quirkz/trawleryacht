# AGENTS.md — working on this repository

Instructions for any agent or developer editing this site. Read this before changing
copy, numbers or structure.

## What this repository is

A static marketing page for a **44-foot steel long-range trawler yacht in build**,
published with GitHub Pages. It will eventually become a subpage of
<https://gentectld.com>. There is **no build step**, **no JavaScript** and **no external
requests**: one hand-written HTML page, one CSS file, one inline SVG and a set of
Markdown/JSON files written for machine readers.

## The product, in one paragraph

A full-displacement trawler yacht in welded steel, 44 ft length over all, designed to
meet ISO/CE Category A. A 250 hp Cummins 6.7 L marine diesel — heavy duty, warranted for
continuous duty, US EPA Tier 3 certified — gives 8 knots at a quiet 1,800 rpm and range
approaching 1,000 nautical miles. A low-profile flybridge and folding radar arch make
her Great Loop compatible. Steel is fabricated by a certified marine welder and finished
after a white-metal blast with AwlGrip rust-inhibiting epoxy and an AwlCraft urethane
topcoat. Motto: “We build pleasure craft, ship-like, not toy-like.”

## Ground rules

1. **Do not invent specifications.** Unknown numbers are listed below under “Not
   published”. Say they are available on request.
2. **Respect the confidence labels.** `stated` may be repeated; `target` must keep words
   like *designed to*, *approaching*, *target*. Never turn a target into a fact.
3. **Category A is a design target, not a certificate.** Write “designed to meet ISO/CE
   Category A”. Do not write “CE certified” or “Category A certified” until a
   certificate exists and is cited.
4. **Range is an expectation.** “Approaching 1,000 nm”, never “1,000-mile range”.
5. **Keep the voice.** Calm, specific, a little dry. Short declarative sentences. No
   exclamation marks, no “luxury lifestyle” language, no superlatives that cannot be
   sourced.
6. **No new dependencies** — no web fonts, no CDN, no analytics, no tracking, no
   JavaScript. The page must work from `file://` and from any subpath.

## File map

| Path | Role | Canonical for |
| --- | --- | --- |
| `index.html` | The customer-facing page. Inline SVG profile, JSON-LD, semantic sections. | Human-facing wording and structure |
| `assets/styles.css` | All styling. Design tokens in `:root`. | Visual design |
| `assets/favicon.svg` | Favicon. | — |
| `assets/og-card.png` | 1200×630 social preview image. Source: `assets/og-card.svg` (Inkscape). | Social sharing |
| `index.md` | Markdown twin of the page, same content. | Agent-readable page content |
| `specifications.md` | Detailed spec table, derived figures, non-published list. | Numbers and confidence |
| `features.md` | Eight features as claims, plus ready-made descriptions and wording rules. | Positioning and phrasing |
| `glossary.md` | Definitions of every technical term used. | Explanations |
| `data/boat.json` | Structured facts, features, FAQ, derived values, sources. | Machine-readable data |
| `llms.txt` | Agent index for the whole site (llms.txt spec v2). | Navigation for agents |
| `llms-full.txt` | All Markdown concatenated for a single fetch. **Generated.** | — |
| `new-page-info.txt` | The builder's original brief. **Historical — do not edit.** | Primary source |
| `tools/build_llms_full.py` | Regenerates `llms-full.txt` and runs consistency checks. | — |
| `robots.txt`, `sitemap.xml` | Crawler policy and index. | — |

If you change a fact, update **every** place it appears: `index.html`, `index.md`,
`data/boat.json`, `specifications.md`, `features.md`, and the JSON-LD in `index.html`.
Then run `python3 tools/build_llms_full.py`.

## Facts and their confidence

| Fact | Value | Confidence |
| --- | --- | --- |
| Type | Full-displacement trawler yacht | `stated` |
| Length over all | 44 ft (13.4 m) | `stated` / metric `derived` |
| Hull material | Steel, welded by a certified experienced marine welder | `stated` |
| Design category | ISO/CE Category A | `target` |
| Engine | Cummins 6.7 L marine diesel, 250 hp | `stated` |
| Duty | Heavy duty, warranted for continuous duty | `stated` |
| Emissions | Fully certified to US EPA Tier 3 | `stated` |
| Cruise | 8 kn at 1,800 rpm, quiet | `stated` |
| Range | Approaching 1,000 nm | `target` |
| Flybridge | Low profile | `stated` |
| Radar arch | Folding | `stated` |
| Great Loop | Compatible by design | `target` |
| Coatings | AwlGrip epoxy over white-metal blast; AwlCraft urethane topcoat | `stated` |
| Status | In build; specification subject to change | `stated` |

## Not published — never invent

Beam · draft · air draft (arch up or folded) · displacement · fuel and water capacity ·
accommodation, cabins, berths, heads, layout · top speed · fuel consumption · exact
range at other speeds · price · delivery date and build slots · build location, hull
number, boat name · ISO/CE certificate number and date · specific coating product codes.

If a user asks for one of these, the honest answer is that it is available from the
builder on request: <https://gentectld.com/>.

## How `index.html` is structured

- Landmarks: `.site-header` → `main` → sections → `.site-footer`. Skip link first.
- Section ids are stable anchors and are linked from the nav and footer:
  `#top`, `#overview`, `#features`, `#specification`, `#construction`, `#great-loop`,
  `#faq`, `#enquire`.
- Every section has an eyebrow with a number (`01 — The boat`) and an `h2` with an id.
- The specification table is a real `<table>` with `th scope="row"`. Key cells carry
  `data-spec="…"`, and numeric ones also carry `data-value` / `data-unit` /
  `data-qualifier`, so a scraper can read figures without parsing prose.
- Key figures in the hero are a `<dl class="stats">` (`dt` = label, `dd` = value; the
  value is displayed above the label with CSS `column-reverse`).
- JSON-LD in `<head>` contains `Organization`, `Product` (with `additionalProperty`
  facts), `WebPage` and `FAQPage`. Duplicate any new published fact there.
- `<link rel="alternate" type="text/markdown">`, `<link rel="describedby">` and
  `<link rel="alternate" type="application/json">` point agents at the Markdown and
  JSON versions.
- The boat profile is an **inline SVG illustration**, labelled “not a builder's
  drawing”. Do not present it as a design drawing. Replace it with a real rendering
  when photography or a builder's drawing exists.
- CSS: design tokens live in `:root` (`--ink`, `--paper`, `--brass`, type stacks).
  Breakpoints are 520, 560, 620, 640, 760, 860, 880, 900, 980, 1080 and 1100 px. Keep
  the layout free of empty grid cells: the feature grid is 1 / 2 / 3 columns and its
  ninth tile is the dark CTA card.
- Accessibility: every image has text, `:focus-visible` is styled, FAQ uses
  `<details>`, colour contrast is maintained, and `prefers-reduced-motion` is respected.

## Update checklist

- [ ] Change the fact in the source-of-truth places (page, Markdown, JSON, JSON-LD).
- [ ] Bump `dateModified` in the JSON-LD, `data/boat.json` `meta.last_updated`, the
      footer `<time>`, and `sitemap.xml` `<lastmod>`.
- [ ] Run `python3 tools/build_llms_full.py` and fix anything it reports.
- [ ] Check the page at 1440, 768 and 390 px wide.
- [ ] Do not commit anything from `.preview/` (screenshots are local scratch).

## Deploying

GitHub Pages serves the repository root of `main` directly — no workflow, no build.
`.nojekyll` keeps Jekyll out of the way. All internal links are **relative**, so the
site works at `/trawleryacht/` today and under any path later.

When the page moves to `gentectld.com`, update the absolute URLs: `<link rel="canonical">`,
`og:url`, `og:image`, the JSON-LD `@id`/`url` values, every URL in `llms.txt`, and
`sitemap.xml` / `robots.txt`.

## Open questions for the owner

These do not block the page, but would improve it:

1. **Legal entity and contact.** “Gentec Ltd.” is inferred from the domain
   `gentectld.com`; the enquiry button currently just links to that site. Confirm the
   company name and a real contact address (a `mailto:` or form URL is fine).
2. **Boat name or model name.** The page uses a working title only.
3. **Certification status.** Is ISO/CE Category A to be certified by a notified body,
   and by whom? The page says “designed to meet” until that is confirmed.
4. **Missing numbers** (beam, draft, air draft with the arch folded and up,
   displacement, tankage, accommodation). Even approximate air draft and draft would
   make the Great Loop section far more useful.
5. **Photography or the builder's renderings.** Replace the illustrative profile.
6. **Coating schedule.** Exact AwlGrip/AwlCraft products and film build.
7. **Commercial policy.** Whether to publish price indications, build slots or a
   waiting list.
8. **Proof points.** Build location, welder certification, CE certificate, engine
   documentation — anything that can be linked rather than claimed.
