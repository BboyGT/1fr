# Why `1fr` Isn't Actually "One Fraction"

Companion demo project for the CSS-Tricks article by [Godstime Aburu](https://github.com/BboyGT).

## What This Is

Four interactive demos that isolate the `1fr` minimum sizing bug in CSS Grid — showing exactly how it breaks, what causes it, and how to fix it.

## Demos

| Demo | What It Shows |
|------|--------------|
| [Demo 1 — Image Overflow](demo-1-image-overflow.html) | A 400px image inside a `1fr` column sets the track minimum to 400px and escapes the container |
| [Demo 2 — Three Fixes](demo-2-three-fixes.html) | `1fr` (broken), `minmax(0, 1fr)` (fixed), `min-width: 0` (fixed) — same content, three outcomes |
| [Demo 3 — Nested Grid](demo-3-nested-grid.html) | An image inside an inner grid cascades its minimum up through both grids |
| [Demo 4 — pre Block](demo-4-pre-block.html) | A `pre` block's longest line sets the track minimum |

## The Core Bug

`1fr` resolves to `minmax(auto, 1fr)` under the hood — not `minmax(0, 1fr)`. The `auto` minimum means a track will never shrink below its content's intrinsic size. Images, `pre` blocks, and anything with `white-space: nowrap` all have large intrinsic minimum sizes that trigger this behaviour.

## The Fix

```css
/* Before */
.grid {
  grid-template-columns: 1fr 1fr;
}

/* After */
.grid {
  grid-template-columns: minmax(0, 1fr) minmax(0, 1fr);
}
```

Or on the item:

```css
.grid-item {
  min-width: 0;
}
```

## Running Locally

No build step needed. Clone the repo and open `index.html` in your browser.

```bash
git clone https://github.com/BboyGT/1fr-demos.git
cd 1fr-demos
open index.html
```

## Article

Read the full article on CSS-Tricks — [Why `1fr` Isn't Actually "One Fraction" (And When It Silently Breaks Your Grid)](https://css-tricks.com)

## Author

**Godstime Aburu** — Frontend Developer & Technical Writer  
[GitHub](https://github.com/BboyGT)
