## Reflection

### 6. Element, class, and ID selector specificity

If I have `p { color: red }` and `.intro { color: blue }`, and my HTML is `<p class="intro">`,
the text will be **blue**. This is because of CSS specificity — the browser doesn't just apply
rules in the order they're written, it weighs how *specific* each selector is. An element
selector like `p` targets every paragraph on the page, so it has low specificity. A class
selector like `.intro` targets only elements with that exact class, so it's more specific and
overrides the element selector, regardless of which rule appears first in the stylesheet. If I
had used an ID selector instead (e.g. `#intro`), it would beat both the element and the class
rule, because IDs are even more specific — they're meant to target a single unique element.

### 7. rem units vs px

`rem` stands for "root em" — it's a font size defined relative to the font-size set on the root
`<html>` element (which defaults to 16px in most browsers, but the user can change it). `px`
(pixels), by contrast, is a fixed, absolute unit that never changes no matter what the user does
in their browser settings.

The advantage of `rem` for accessibility is that it respects the user's own preferences. Someone
with low vision might increase their browser's default font size to make text easier to read
everywhere. If my page is sized in `rem`, all my text scales up proportionally along with that
setting. If I had used `px` instead, the text would stay locked at the exact pixel size I chose,
ignoring the user's accessibility settings entirely.

If a user changes their browser's default font size to 20px, then `1rem` no longer equals 16px —
it now equals 20px, and everything on my page sized in `rem` grows proportionally (e.g. a
heading set to `2rem` would go from 32px to 40px). Text sized in `px` would not change at all.

### 8. Google Fonts and no internet access

Google Fonts are hosted on Google's CDN, so the browser has to download the font files from
Google's servers the first time it loads my page. If a user in a rural area of Malawi has no
internet connection, that request fails, and the custom fonts (Spectral, Source Serif 4, IBM
Plex Mono) simply won't load.

This doesn't break the page, though, because of the *font stack* I wrote in my CSS — for example
`font-family: "Spectral", Georgia, serif;`. When the first font in the list can't load, the
browser falls back to the next one it can find. Since I listed generic fallback fonts (like
`serif` and `monospace`) after each Google Font, the browser falls back to whatever serif or
monospace font is already installed on the user's device. The typography wouldn't look exactly
as designed, but the text would still render and stay fully readable — nothing would be missing
or blank. To make a page more resilient offline, I could also self-host the font files locally
instead of relying on the CDN.

### 9. HSL color format

HSL stands for hue, saturation, and lightness, and each value controls a different aspect of
the color:
- **Hue** (0–360°) is the actual color itself — its position on the color wheel (0° = red,
  120° = green, 240° = blue, and so on).
- **Saturation** (0–100%) is the intensity or purity of the color — 0% is completely gray/dull,
  and 100% is the most vivid, pure version of that hue.
- **Lightness** (0–100%) is how light or dark the color is — 0% is always black, 100% is always
  white, and 50% is the "normal" full-strength version of the color.

`hsl(120, 100%, 50%)` is a pure, fully saturated green. To make the *same* color much lighter
while keeping it recognizably the same hue, I would change the **lightness** value — for example
raising it from 50% to around 85–90% — while leaving the hue (120) and saturation (100%) alone.
Changing the hue would turn it into a different color entirely, and changing the saturation
would just make it duller, not lighter.