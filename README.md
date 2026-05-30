# Brier Design

The shared design system for Brier — the **Clear Horizon** palette, type scale, and base
component styles used across every Brier property (brier.institute, brieralmanac.org, and the
Next.js apps). Single source of truth: edit here, bump the version, and every consumer updates.

## Files

- **`tokens.css`** — design tokens as `:root` custom properties: surfaces, borders, text,
  accent (rose) and horizon (blue) colors, and the four font stacks.
- **`base.css`** — reset, layout (`.wrap`), and shared components: header, hero, sections,
  cards (`.program` / `.pillar`), lineage strip, CTA, footer. Depends on `tokens.css`.

## Use it

### Static sites — via jsDelivr, version-pinned

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/MaxGhenis/brier-design@v1.0.0/tokens.css" />
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/MaxGhenis/brier-design@v1.0.0/base.css" />
```

Always pin to a tag (e.g. `@v1.0.0`) — never `@main`. That way a token edit never silently
restyles a live site; you bump the tag intentionally when you want consumers to update.

Fonts (Newsreader, IBM Plex Sans/Mono, Instrument Serif) are loaded by each page in `<head>`
so they can use `preconnect`; the tokens just reference the families.

### Next.js / Tailwind v4 apps

Install as a git dependency and `@import` the Tailwind theme:

```bash
bun add github:MaxGhenis/brier-design#v1.1.0
```
```css
@import "tailwindcss";
@import "brier-design/theme.css";   /* full Clear Horizon palette as @theme */
```

`theme.css` carries the full palette in Tailwind's `--color-*` / `--font-*` form so it
generates utilities; static sites use `tokens.css` (plain `:root` vars) instead. Same values,
two consumption styles.

## Versioning

Tagged releases (semver). To ship a change:

```
# edit tokens.css / base.css
git commit -am "…"
git tag v1.1.0
git push && git push --tags
# then bump @v1.0.0 → @v1.1.0 in each consumer
```
