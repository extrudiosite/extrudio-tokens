# Extrudio tokens

The design tokens of Extrudio's apps: the app, the site and the admin app share one set of values,
so the three don't drift. This package is made from the app's design system and published from
there. Don't edit it here: a change made here is lost at the next release.

Components and base styles (the focus ring, the page's background) are each app's own. Only the
values and the brand's files are shared.

## Files

| File | What it is |
|---|---|
| `tokens.json` | The tokens in the [W3C Design Tokens](https://www.designtokens.org/tr/drafts/format/) format, in three sets: `base` (both themes), `light` (every themed token) and `dark` (only what differs). A token's key is its CSS variable's name. |
| `tokens.css` | The same tokens as CSS variables: `base` and `light` on `:root`, `dark` on `.dark`. Generated from `tokens.json`. |
| `theme.css` | The Tailwind v4 theme. It maps utilities (`bg-background`, `text-muted-foreground`, `rounded-lg`, `shadow-md`, `ease-standard`, …) onto the variables, sets up the `dark:` variant for a `.dark` class, and switches off Tailwind's palette. |

## Install

A tag pins a version. To update, change the tag.

```bash
pnpm add github:extrudiosite/extrudio-tokens#v1.0.0
```

## Use

With Tailwind v4, in the stylesheet that imports Tailwind:

```css
@import "tailwindcss";
@import "@extrudio/tokens/tokens.css";
@import "@extrudio/tokens/theme.css";
```

- **Dark theme:** a `dark` class on `<html>`. With next-themes, set `attribute="class"`.
- **Typefaces:** `--font-sans` and `--font-mono` read `--font-geist-sans` and `--font-geist-mono`.
  Load Geist with `next/font` under those variable names; without them, the system stack shows.
- **Without Tailwind:** import `tokens.css` alone and use the variables, as in `var(--foreground)`.

## Brand

`brand/` holds the files of the L07 brand kit, the same the app uses:

- `brand/logos/`: the symbol, compact, horizontal and stacked logos and the name alone
  (`wordmark`), each in light, dark, black, white, blue and blue-dark SVG, with the lettering
  outlined.
- `brand/icons/`: `favicon.ico` (the 16 and 32 px marks), PNG icons of 16, 32, 180, 192 and
  512 px, the 3-layer `favicon.svg`, and the kit's `site.webmanifest`.
- `brand/social/`: the link preview (`og`, 1200 × 630) and the email header (640 × 120), light and
  dark.
- `brand/README.md`: the kit's rules on clear space, smallest sizes and colours.

On screen, use the light files on light surfaces and the dark files in the dark theme. Or inline an
SVG and fill its mark with `var(--brand)` and its name with `var(--foreground)`, as the app's
`Logo` does, so one file follows both themes. With pnpm the files are in
`node_modules/@extrudio/tokens/brand/`: copy the ones a page serves into its `public/`.

## Rules

- **Use the tokens, never raw values.** The palette is switched off, so only token colours exist.
- **Surfaces are neutral.** Every surface has zero chroma, so the chrome never tints a render; a
  test in the app fails otherwise. `stage` is the backdrop behind a render.
- **One accent.** `brand` (and `primary`, `ring`) is for actions, focus and progress, never for
  surfaces.
- **Pairs meet WCAG 2.2 AA.** Put text on its own pair: `foreground` on `background`,
  `card-foreground` on `card`, `primary-foreground` on `primary`, and so on.

## Versions

- A patch changes values.
- A minor adds tokens.
- A major renames or removes a token.

Each tag's commit says which commit of the app it came from.

A published tag is never moved or deleted, and the repo stays public. The apps' lockfiles pin each
tag's commit and integrity hash, and Vercel fetches the package on every build, so a moved tag
would break their builds. A fix is always a new version.

## Releasing

From the app repo, after the tokens are committed there:

```bash
gh repo clone extrudiosite/extrudio-tokens local/extrudio-tokens   # once
pnpm tokens:release 1.1.0
```

The script writes the package into the checkout and prints the commit, tag and push commands. It
refuses a version that isn't later than the published one, and uncommitted tokens.

Copyright Extrudio. All rights reserved. The repo is public so that the apps' builds can install it
without credentials.
