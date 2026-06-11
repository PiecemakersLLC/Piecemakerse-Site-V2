# Piecemakers — Website (Static Build)

One-page static site built from the designer layout (`Assets/PMSiteLayoutV3.psd`) and the
Piecemakers Branding Guideline. No build step, no dependencies — open `index.html` in any
browser or drop the `site/` folder on any static host (Netlify, Vercel, S3, GitHub Pages, etc.).

## Files

```
site/
├── index.html        # all page markup
├── styles.css        # all styling (brand colors + fonts)
├── assets/           # logo artwork (transparent PNG, vector-sourced from the .ai files)
│   ├── wordmark.png      # hero PIECEMAKERS wordmark
│   ├── symbol.png        # circle/crescent icon (nav brand, favicon)
│   ├── symbol-grey.png   # grey icon used in WORK product placeholders
│   ├── primary-logo.png  # symbol + wordmark lockup (spare)
│   └── logomark.png       # "M" monogram mark (spare)
└── fonts/            # brand fonts, self-hosted
    ├── GillSansExtCondBold.ttf     # headlines / nav / labels
    ├── HelveticaNeue-Regular.ttf   # body
    ├── HelveticaNeue-Bold.ttf      # body bold
    └── HelveticaNeue-UltraLight.ttf# accent (available, not yet used)
```

## Brand system applied

Colors (CSS variables in `styles.css`):

| Token        | Hex       | Use                         |
|--------------|-----------|-----------------------------|
| Floppy Disk  | `#252523` | headings / heavy text       |
| Beige Box    | `#F2F0DA` | page background             |
| Microchip    | `#8B8986` | nav, footer, rules, borders |
| Cathode      | `#AF1959` | magenta accent              |
| Binary       | `#006074` | teal accent                 |

Type: Gill Sans MT Extra Condensed Bold for the all-caps headlines, nav and chip labels;
Helvetica Neue for body. Hex/font choices were sampled directly from the guideline artwork.

## Sections

`#about` · `#what-we-do` · `#why-were-great` · `#work` · `#contact` — the nav links jump to each.

## Where to plug in content

- **WORK / products.** Each artist block is `.artist` with a `.grid` of `.tile` anchors
  (placeholders). To add a product: set the tile's `href` to the product/checkout URL and drop
  an `<img>` inside the `<a class="tile">`. The first tile in Artist One/Two is `.tile--feature`
  (larger, currently shows the grey emblem + "Select Item"). Add or remove artist blocks by
  copying a `.artist` block. Real artist names (e.g. JID, Mariah the Scientist, EarthGang)
  replace the `Artist One/Two/Three` chip labels.
- **Comparison table.** Plain `<table class="compare">` — edit rows directly. The Piecemakers
  column uses classes `yes-pm` / `val-pm` (magenta highlight); competitor columns use `yes` / `no`.
- **Email.** `info@piecemakers.cc` is wired as a `mailto:` in `#contact` and in the meta.

## Notes / decisions

- "GreatMerch" placeholder copy from the PSD was replaced with **Piecemakers** throughout, per
  brand standard. Competitor table columns kept as designed: "Merch Company A" / "Indie Merch Company B".
- The brand wordmark's accent dot is rendered in black (from the official vector wordmark). The
  PSD comp showed it in magenta — easy to swap if you want the magenta dot on the hero.
- **Font licensing:** Helvetica Neue and Gill Sans are commercial fonts. They're self-hosted here
  because they're your licensed brand fonts — confirm your license covers web/`@font-face`
  embedding before public deployment. If not, swap to a licensed web equivalent in the `@font-face`
  blocks (Arial Narrow Bold / Arial are the brand-approved fallbacks and are already set).
- Responsive: collapses to single-column versus list and 2-up product grids under 720px.

## Not yet done (needs your input)

- Real product images, prices, and checkout/links for the WORK grids.
- Final artist roster + ordering.
- Hosting/domain setup.
