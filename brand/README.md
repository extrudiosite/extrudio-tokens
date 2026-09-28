# Brand (L07)

The brand's files, from the L07 brand kit of 2026-09-28 (Ishai's logo package). They are copied
unchanged and checked against the kit's `SHA256SUMS.txt`, except that their names drop the
product's, so a rebrand replaces files and not references. The kit's guidelines PDF, social covers,
watermarks and presentation files stay with Ishai.

## Files

| Folder | What it holds |
|---|---|
| `logos/` | The symbol, compact, horizontal and stacked logos and the name alone (`wordmark`), each in light, dark, black, white, blue and blue-dark SVG. The lettering is outlined Sora 600, so no font is needed. |
| `icons/` | `favicon.ico` (16 px with 3 layers, 32 px with 7), `favicon-16.png`, `favicon-32.png`, `favicon.svg` (the 3-layer micro mark only), `apple-touch-icon.png` (180 px), `icon-192.png`, `icon-512.png`, and the kit's `site.webmanifest`. |
| `social/` | The link preview (`og`, 1200 × 630) and the email header (640 × 120), light and dark. |

## In the app

- On screen, use the `Logo` component (`components/brand/logo.tsx`). It draws these logos from
  their geometry (`logo-art.ts`) in the tokens' colours, so it follows the theme. The SVG files are
  for places the tokens don't reach: emails, other apps, print.
- The app serves copies of some of them, and `src/app/brand-files.test.ts` checks that they match:
  - `favicon.ico`, `apple-icon.png` and `opengraph-image.png`;
  - `/brand/icon-192.png`, `/brand/icon-512.png` and `/brand/email-header.png`.
- The shared tokens package carries this folder for the site and the admin app (`brand/`).

## Rules, from the kit

- Never stretch the logo, re-space its letters or colour a layer on its own.
- Leave clear space of at least an eighth of the symbol's size around the logo: 8 px for a 64 px
  symbol, 4 px for the compact files.
- The smallest sizes on screen:
  - the symbol 64 px (its compact form 32 px; the 3-layer micro mark is for 16 px favicons only);
  - the horizontal logo 540 px wide, the compact one 240 × 56, the stacked one 192 px wide;
  - the name alone 160 px wide.
- Colours:
  - light: the mark `#295EE3` (the `brand` token) and the name `#0D0D0D` (`foreground`), on
    `#FCFCFC` or white;
  - dark: the mark `#6C9BFE` and the name `#F5F5F5`, on `#161616`.

  Blue backgrounds are brand material, never app surfaces: the chrome around renders stays
  neutral.
- Write the name "Extrudio" in text. The logo's uppercase is lettering, not a way to write the
  name.
- Sora (SIL OFL 1.1) is the logo's lettering only. The app's type stays Geist.
