# Notions Design System

Design tokens and React components behind [alygates.com](https://www.alygates.com) and the small apps I build. In sewing, notions are the small parts that finish a garment: buttons, zippers, snaps.

- **Figma:** the Notions Design System file (Tokens, Components, Exploration)
- **Package:** `@alygates/notions`
- **Built for:** React and Tailwind v4

## What's here

| Folder | What it is |
|---|---|
| `tokens/` | The source of truth, in the W3C design token format. See [tokens/README.md](tokens/README.md). |
| `scripts/` | `build-tokens.mjs` turns the tokens into CSS. No dependencies. |
| `dist/` | The built CSS that apps import: `tokens.css` and `theme.css`. |

Components, Storybook, and tests are next.

## Build the tokens

```
npm run build:tokens
```

## Use it in an app

```css
@import "tailwindcss";
@import "@alygates/notions/tokens.css";
@import "@alygates/notions/theme.css";
```

Then use the semantic classes: `bg-surface-raised`, `text-ink-subtle`, `border-line-strong`, `bg-primary text-on-primary`.

## How the tokens are organized

- **Primitives** are raw values: color scales (neutral, poppy, mist, avocado, cherry, fern, marigold), alpha scales, radius, spacing, sizes. They aren't Tailwind classes.
- **Semantic tokens** name a job and point at a primitive. Backgrounds are `surface`, text is `ink`, borders are `line`. `subtle` means less contrast and `strong` means more.
- **Components** use semantic tokens only.

Dark mode is the default. Add `.light` to switch, or leave it to the system setting.
