# trawleryacht

The web page for a **44-foot steel long-range trawler yacht in build** — a static site
published with GitHub Pages, eventually to live as a subpage of
[gentectld.com](https://gentectld.com).

Full displacement · welded steel · ISO/CE Category A design target · 250 hp Cummins
6.7 L · 8 knots at 1,800 rpm · range approaching 1,000 nm · low-profile flybridge and
folding radar arch, Great Loop compatible. *Ship-like, not toy-like.*

## The page

| File | What it is |
| --- | --- |
| [`index.html`](index.html) | The page. Hand-written, one file, no JavaScript, no external requests. |
| [`assets/styles.css`](assets/styles.css) | All styling, with design tokens in `:root`. |
| [`assets/og-card.png`](assets/og-card.png) | 1200×630 social preview (source: `assets/og-card.svg`). |
| [`assets/favicon.svg`](assets/favicon.svg) | Favicon. |

Sections: hero with a technical-drawing profile and key figures → the boat → eight key
features → specification table → construction and finish → Great Loop → FAQ → enquiry.

## The agent layer

The page is published twice: once for people, once for machines.

| File | Purpose |
| --- | --- |
| [`llms.txt`](llms.txt) | [llms.txt](https://llmstxt.org) index: summary, key points, links. |
| [`llms-full.txt`](llms-full.txt) | Every Markdown file concatenated, for a single fetch. Generated. |
| [`index.md`](index.md) | Markdown twin of the page (`rel="alternate" type="text/markdown"`). |
| [`specifications.md`](specifications.md) | Every figure, each labelled `stated` / `derived` / `target`, plus the list of figures deliberately not published. |
| [`features.md`](features.md) | Features as checkable claims, ready-made descriptions, wording rules. |
| [`glossary.md`](glossary.md) | Plain definitions of air draft, hull speed, Category A, white metal and the rest. |
| [`data/boat.json`](data/boat.json) | Structured facts, features, FAQ and derived values. |
| [`AGENTS.md`](AGENTS.md) | How the repo is organised and how to change it without inventing facts. |

The HTML carries `Product`, `FAQPage`, `Organization` and `WebPage` JSON-LD, a real
specification `<table>` with `data-spec` / `data-value` / `data-unit` attributes, and
`<link>` elements pointing at the Markdown and JSON versions.

## Editing

```sh
python3 tools/build_llms_full.py    # rebuild llms-full.txt and run consistency checks
```

The checks verify that the HTML, the Markdown and the JSON agree on the published
facts, that the forbidden overstatements are absent, and that every `llms.txt` link
resolves. **Read [`AGENTS.md`](AGENTS.md) before changing numbers** — the rule is
simple: if the builder has not published a figure, the page says it is available on
request rather than guessing.

## Previewing

There is no build step; open `index.html` in a browser, or serve the folder:

```sh
python3 -m http.server 8000
# http://localhost:8000/
```

All internal links are relative, so the site works at a domain root and at a subpath.

## Deploying

GitHub Pages serves the root of `main` directly (Settings → Pages → Deploy from a
branch → `main` / `/`). `.nojekyll` disables Jekyll processing. No workflow, no build.

When the page moves to `gentectld.com`, update the absolute URLs listed in
[`AGENTS.md`](AGENTS.md#deploying).

## Original brief

[`new-page-info.txt`](new-page-info.txt) is the builder's original statement — the
primary source for every claim, kept unchanged for provenance.
