# Notions tokens

The source of truth for Notions Design System. Exported from the Figma file on Nov 6, 2026, with light values taken from the Semantic theme table (Figma Starter has no modes).

Format: [W3C Design Tokens](https://design-tokens.github.io/community-group/format/). References look like `{color.neutral.900}`. Every token's CSS name is in `$extensions["com.alygates.notions"].css`.

| File | What's in it |
|---|---|
| `primitives.json` | Color scales (`color.*`, 100–900), alpha scales (`alpha.*`, a100–a900), radius (t-shirt), spacing (Tailwind steps), icon and control sizes, durations, breakpoints |
| `semantic.json` | Tokens that don't change by theme: focus width and offset, motion, overlay blur |
| `theme.dark.json` | Semantic colors for dark mode (the default) |
| `theme.light.json` | Semantic colors for light mode. Same names, different primitives. |
| `typography.json` | Font families, the font-size scale, weights, and the 13 text styles |

## Build

```
node scripts/build-tokens.mjs
```

Writes two files to `dist/`:

- **`tokens.css`**: primitives as plain `:root` variables, and semantic colors as `--notions-*` variables that switch between `.dark` (default), `.light`, and the system setting.
- **`theme.css`**: Tailwind v4 `@theme inline`. Clears Tailwind's default colors and radius, then maps semantic tokens to utilities.

Checked against Tailwind 4.1: `bg-surface-raised`, `text-ink-subtle`, `border-line-strong`, `bg-accent-poppy-subtle`, `text-danger-strong`, `rounded-lg`, `size-icon-md`, `font-display`, and `text-title` all work. `bg-poppy-400`, `bg-neutral-500`, `text-red-500`, and `rounded-2xl` don't exist, so components can't skip the semantic layer.

## Using it in an app

```css
@import "tailwindcss";
@import "@alygates/notions/tokens.css";
@import "@alygates/notions/theme.css";

/* Optional: this app's primary. Point all five primary tokens at the same accent. */
:root, .dark {
  --notions-primary: var(--color-avocado-400);
  --notions-primary-strong: var(--color-avocado-300);
  --notions-primary-subtle: var(--color-avocado-a200);
  --notions-primary-line: var(--color-avocado-500);
}
.light {
  --notions-primary: var(--color-avocado-600);
  --notions-primary-strong: var(--color-avocado-700);
  --notions-primary-line: var(--color-avocado-500);
}
```

Apps load the fonts themselves (for example with `next/font`) and set `--font-family-display`, `--font-family-body`, and `--font-family-label`. Without them, the fallback stacks are used.

## Changing a token

1. Edit the JSON here.
2. Run the build.
3. Update the Figma variable (and the theme table for light values) to match.
