# Piecemakers one-sheet — web handoff

Everything needed to publish the one-sheet as an unlisted page. Self-contained: no
build step, no dependencies, no framework. Drop it in and it works.

## What's in here

```
WEB - one-sheet/
├── index.html                 13 KB   the page
├── robots-snippet.txt                 lines to append to the site's robots.txt
└── assets/                    2.4 MB  total
    ├── gill-ext-condensed-bold.ttf    headline font (already @font-face'd)
    ├── piecemakers-wordmark.png       cream wordmark, transparent
    ├── jid-merch.mp4          1.0 MB  hero video, muted autoplay loop
    ├── hero-poster.jpg                video poster + print fallback
    ├── jid-merch-wall.jpg             lower band
    ├── jid-crowd.jpg                  JID case panel
    └── fans-cap.jpg                   Mariah case panel
```

## Deploy

1. Copy the whole `WEB - one-sheet` folder into the site repo as a subdirectory,
   e.g. `one-sheet/` (or something less guessable, see below).
2. Keep `index.html` and `assets/` together. Paths inside are relative, so the
   folder works at any depth without edits.
3. Do **not** add a nav link anywhere. The page is reached by direct URL only.
4. Append the contents of `robots-snippet.txt` to the site's `robots.txt`,
   adjusting the path to match the directory name chosen.
5. Confirm the site's sitemap generator doesn't pick it up. If the sitemap is a
   static file, just don't add it.

Live at `piecemakers.cc/one-sheet/` once pushed.

## Keeping it unlisted

`index.html` already sets:

```html
<meta name="robots" content="noindex,nofollow,noarchive,nosnippet,noimageindex">
<meta name="googlebot" content="noindex,nofollow">
<meta name="referrer" content="no-referrer">
```

`noindex` keeps it out of search results. `no-referrer` means that if someone
clicks a link from this page, the destination's analytics won't log where they
came from, so the URL doesn't leak that way.

**Use an unguessable directory name.** `one-sheet/` is the first thing anyone
would try. Something like `s/2026-pm-4a7c/` is meaningfully better — it's the
only real barrier a static host provides.

**Understand the limit.** This is obscurity, not access control. There's no
login. Anyone with the URL can open it, and anyone they forward it to can too.
If the repo is public, the file is also visible by browsing the repo regardless
of whether anything links to it. If stronger protection is wanted later, the
options are Cloudflare Access in front of the path, or a host with native
password protection. Neither is available on plain GitHub Pages.

## Notes

- The video is muted and `playsinline`, which is what lets it autoplay on iOS
  Safari and Chrome. Don't add `controls` or remove `muted` — either breaks
  autoplay.
- `preload="metadata"` means the 1 MB video doesn't download until needed. Fine
  on mobile data.
- Print styles are included: printing the page swaps the video for the poster
  frame and drops the page background so it doesn't dump ink.
- Responsive down to phone width. Case panels stack, the four-channel band goes
  to two columns, the stat cells stack rather than compress.
- Fonts: Gill Sans Extra Condensed Bold is bundled. Body copy is Helvetica Neue
  from the system stack with Arial fallback, so nothing else to load.

## If the page needs changing later

Don't hand-edit `index.html` — it's generated. The source of truth is
`build_html_v4.py` in the one-sheet working session, which produces the
self-contained version; `build_web.py` then splits the assets back out and adds
the noindex tags. Editing the HTML directly means the next regeneration
silently overwrites the change.
