---
name: marquee-fix
description: Fix continuously scrolling text or logo marquees that show blank tails or jump at the loop, especially when a short row meets a wide viewport. Use for CSS and vanilla-JS tickers, not paged carousels.
---

# Marquee Fix

Repair the loop while preserving the page's content, spacing, direction, and visual style. First measure the clipped viewport and one complete source row. A two-row marquee fails when the row is narrower than the viewport: near the reset, the track ends before the viewport does.

## The coverage rule

Let `W` be the marquee's `clientWidth` and `R` the rendered width of one complete row, including its trailing seam space. If `R` can fall below `W`, create two identical halves with:

```text
rowsPerHalf = ceil((W + 1) / R)
totalRows = 2 * rowsPerHalf
```

The extra pixel covers fractional layout rounding. Animate the track from `0` to `translateX(-50%)`: one half then replaces the other at exactly the same visual position. Keep seam spacing inside each row, such as `padding-right`, so all copies have identical geometry. A fixed number of copies or `overflow: hidden` alone cannot guarantee coverage at wide widths.

## Apply it

1. Keep one source row in the HTML. Clone it until `totalRows` is reached; mark every clone `aria-hidden="true"`. A single source prevents two hand-written halves from drifting apart.
2. Keep the CSS animation paused until the copies are ready. Set its duration from travel distance divided by a chosen pixel speed, so shortening the text does not make the marquee nearly stationary.
3. Recalculate when the clip or source row changes size. A `ResizeObserver` on both covers viewport changes and late font or image sizing. Guard a zero-width row.
4. For reduced motion, stop the animation and allow horizontal scrolling so every original item remains reachable.

If a row is proven wider than the viewport at every supported size, two static copies may be enough. Use measured cloning when that condition can change. Adapt the selectors to the existing page rather than replacing unrelated markup.

## Verify the result

Check a narrow viewport, a normal desktop, and at least 5120 CSS pixels wide; use 7680 pixels when stress testing. After load and after resizing, confirm each half covers the clip, the two halves have identical content, clones are hidden from assistive technology, and the page has no horizontal overflow. In browser automation, wait for the resize observer's rendering update before measuring; an immediate DOM query can see the previous copies. Inspect several animation phases, especially just before reset: no growing empty tail should appear, and the first item of the next half should align with the first item at time zero. Check reduced-motion behavior separately.

## Examples

- Three short names in a 5120px clip: if one row is about 336px wide, 16 rows per half give about 5376px of coverage; the track needs 32 identical rows. At 24px/s, one full cycle takes about 224 seconds.
- A 900px row in a 375px clip needs one row per half, so two copies suffice.
- [Runnable three-name HTML example](references/minimal-example.html) contains the CSS, vanilla JS, resize handling, and reduced-motion fallback.
