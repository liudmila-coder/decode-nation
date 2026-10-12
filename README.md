# Decode Nation — landing page (Manifesto v9)

Static one-page site for Decode Nation, a women-owned California social enterprise. This is the direction the client chose ("Manifesto"). v9 is the calm "culture fundamental" pass from `ТЗ для Claude Code.md` (02.10) on top of v8 (still live in its own repo): exactly two fonts (Playfair Display 600 + Helvetica Neue) and exactly seven type styles (display, headline, statement, section-label, body, small, button — CSS variables `--fs-*` in `:root`, nothing else sets a size); body text 18/17px in #1A1A1A; one headline per card, section names live only in the burgundy label; a thin hand-drawn burgundy stroke (≈2.5px, like the card frame, slightly uneven) under women / women’s in the hero and three headlines only; burgundy as an accent (no solid blocks, one filled button — the hero CTA); more air inside and between cards. Background and the double sketch frames are unchanged from v8. Copy is verbatim. There is no build step: open `index.html` or serve the folder from any static host (GitHub Pages works, and `.nojekyll` is included).

## Structure

```
index.html        markup, meta, OG and JSON-LD
css/style.css     design tokens in :root, layout, motion, reduced-motion rules
js/main.js        scroll reveal + contact form
assets/           bg-public-space.webp (+ -600, fixed background), station.webp,
                  founder-*.webp (+ -640 variants for srcset), logo.jpg (favicon)
```

## Contact form

At the top of `js/main.js`:

```js
var FORM_ENDPOINT = '';
```

- **Empty (the current setting):** a valid submit opens the visitor's mail client. The mail goes to `contact@decodenation.com`, with the subject and body already filled in.
- **Set to a URL** (Formspree, Netlify function and so on): the form POSTs JSON `{name, organization, intent, message}` to it. The button shows the pending, success ("Thank you — we’ll be in touch") and error states. Any non-2xx response counts as an error.

Name and Message are required. Organization and interest are optional. The form also has a honeypot field called `website`.

## Before launch

- [ ] Remove `<meta name="robots" content="noindex, nofollow">` from `index.html`.
- [ ] Add the real LinkedIn and Instagram URLs. Each is marked `<!-- TODO client: URL -->` and currently points to `#contact`.
- [ ] Connect the form: set `FORM_ENDPOINT`, or keep the mailto fallback on purpose.
- [ ] Decide on the hero CTA "Explore What We Do →". Its copy is provisional. To remove it, delete the block between the `PROVISIONAL hero CTA` comments.
- [ ] Self-host Playfair Display (loads from Google Fonts for now). Helvetica Neue is used as a system font (macOS/iOS); Windows/Android fall back to Helvetica/Arial. If the exact face is required everywhere, buy a webfont licence (or pick a free near-equivalent).
- [ ] Get a vector logo (SVG) and replace the `logo.jpg` favicon.
- [ ] Confirm image rights. The background is AI-generated and was supplied by the client; also confirm the portraits and the station render.
- [ ] The background source is 941×1671 (portrait). On wide desktop screens it is upscaled ~1.5× and cropped; a landscape original ≥2400px wide would be sharper.
- [ ] Switch OG image to an absolute URL once the domain is known (some scrapers ignore relative `og:image`).
