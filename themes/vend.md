# Theme: Vend (Warp Design System)

Sourced from `warp-ds/tokens/vend-light`. Use this theme for iOS community workshops and Vend-branded presentations.

## Color Tokens

```css
:root {
  /* Grays */
  --white: #ffffff;
  --gray-50: #fafafb;
  --gray-100: #efeff2;
  --gray-200: #e5e5ea;
  --gray-300: #c2c2c9;
  --gray-400: #a0a0a8;
  --gray-500: #84848f;
  --gray-600: #5c5c66;
  --gray-700: #47474f;
  --gray-800: #2b2b30;
  --gray-900: #1b1b1f;
  --gray-950: #121212;

  /* Brand accent (secondary semantic color) */
  --brown-50: #f6e6e6;
  --brown-100: #e7c1bf;
  --brown-200: #d69e9b;
  --brown-400: #ac5f5a;
  --brown-500: #94433d;
  --brown-600: #7a2822;   /* ← primary accent */
  --brown-700: #711e17;
  --brown-800: #5a0d08;

  /* Semantic colors */
  --forest-50: #ebfaed;
  --forest-100: #c7ebcf;
  --forest-400: #55b866;
  --forest-500: #2fa944;

  --blue-50: #e4f0fa;
  --blue-500: #4091dd;

  --purple-50: #efe8fa;
  --purple-500: #8355df;

  --red-50: #fbe9e9;
  --red-500: #e53f3e;
  --red-600: #e22d2c;

  /* Semantic mappings */
  --accent: var(--brown-600);
  --accent-light: var(--brown-50);
  --accent-border: var(--brown-100);
  --border: var(--gray-200);
}
```

## Typography

| Role | Font | Source | Weight range |
|------|------|--------|-------------|
| Display headlines | Outfit | Google Fonts | 700-900 |
| Body text | Inter | Google Fonts | 300-700 |
| Code / labels | JetBrains Mono | Google Fonts | 300-600 |

```html
<link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;500;600;700;800;900&family=Inter:wght@300;400;500;600;700&family=JetBrains+Mono:wght@300;400;500;600&display=swap" rel="stylesheet">
```

```css
--font-display: 'Outfit', system-ui, sans-serif;
--font-body: 'Inter', system-ui, sans-serif;
--font-mono: 'JetBrains Mono', monospace;
```

Note: Vend's native font is 'VendSansText' (not publicly available). Outfit is the web substitute — geometric sans with similar character.

## Component Patterns

### Pills / badges
- `border-radius: 999px` (Vend button convention — fully rounded)
- Variants: `.dark` (gray-900 bg), `.accent` (brown-50 bg, brown-600 text), `.green` (forest-50 bg), `.purple` (purple-50 bg)

### Cards
- `border-radius: 12px`
- `background: gray-50`
- `border: 1px solid gray-200`
- Hover: `border-color: gray-200` (if initially transparent)

### Code preview (faux editor)
- `border-radius: 12px`
- `background: gray-900` (dark)
- Header with 3 dots (gray-600) + filename (gray-400)
- Code body: heading (#e6edf3), line (gray-300), highlight (brown-200), comment (gray-500)

### Accent line
- `width: 32px; height: 3px; background: brown-600; border-radius: 999px`

## Slide-Specific Patterns

### Inverted slides (key insight, demo card)
- `background: gray-900; color: white`
- Accent text uses `brown-200` (lighter shade for contrast on dark)
- Used for dramatic pauses and energy shifts

### Progress bar
- `height: 2px` at top of viewport
- Fill color: `brown-600`

### Slide counter
- `mix-blend-mode: difference` (works on both light and dark slides)

### Entrance animations
- `.reveal` class with `translateY(20px)` + `opacity: 0`
- Staggered delays: `.d1` through `.d7` (0.08s increments)
- Easing: `cubic-bezier(0.16, 1, 0.3, 1)`

## Cheatsheet Styling

Same fonts and accent color as slides, but:
- **Light background only** (white)
- Speaker quotes: `brown-50` background, `brown-600` left border
- Stage directions: `gray-400` italic
- Demo cards: `forest-50` background, `forest-100` border

## Origin

Colors sourced from `github.com/warp-ds/tokens` → `tokens/vend-light/colors.json`
Semantic mappings from `tokens/vend-light/semantic.json`
Button radius from `warp-ds/css` → `tokens/vend.com/base.yml`
