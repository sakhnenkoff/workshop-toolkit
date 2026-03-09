# Workshop Slide Style Presets

Curated subset of visual themes for tech workshops. Use these as starting points — adapt colors, fonts, and details to the specific workshop context.

## Preset 1: Clean Dark

**Mood:** Professional, focused, modern tech
**Best for:** Technical deep-dives, developer-facing workshops

```css
:root {
  --bg-primary: #0a0a0f;
  --bg-secondary: #12121a;
  --bg-card: #1a1a26;
  --text-primary: #e8e8f0;
  --text-secondary: #8888a0;
  --text-dim: #555568;
  --accent: #6ee7b7;
  --accent-dim: #2d6a52;
  --accent-glow: rgba(110, 231, 183, 0.08);
  --border: #2a2a3a;
  --font-display: 'DM Sans', system-ui, sans-serif;
  --font-body: 'DM Sans', system-ui, sans-serif;
  --font-mono: 'JetBrains Mono', monospace;
}
```

**Visual elements:**
- Subtle grid background (60px, low opacity)
- Green accent for highlights and badges
- Monospace for timestamps, code, and labels
- Cards with subtle borders and raised surfaces

---

## Preset 2: Swiss Light

**Mood:** Clean, precise, confident
**Best for:** Mixed audiences, introduction workshops, broad presentations

```css
:root {
  --bg-primary: #ffffff;
  --bg-secondary: #fafafa;
  --bg-card: #f5f5f5;
  --text-primary: #1a1a1a;
  --text-secondary: #666666;
  --text-dim: #999999;
  --accent: #ff3300;
  --accent-dim: #cc2900;
  --accent-glow: rgba(255, 51, 0, 0.06);
  --border: #e5e5e5;
  --font-display: 'Archivo', system-ui, sans-serif;
  --font-body: 'Nunito', system-ui, sans-serif;
  --font-mono: 'JetBrains Mono', monospace;
}
```

**Visual elements:**
- Pure white background, strong black text
- Red accent sparingly (for emphasis only)
- Visible grid structure, asymmetric layouts
- Large section numbers, bold typography

---

## Preset 3: Terminal

**Mood:** Developer-native, hacker aesthetic
**Best for:** Developer-only audiences, CLI/tooling workshops

```css
:root {
  --bg-primary: #0d1117;
  --bg-secondary: #161b22;
  --bg-card: #21262d;
  --text-primary: #c9d1d9;
  --text-secondary: #8b949e;
  --text-dim: #484f58;
  --accent: #39d353;
  --accent-dim: #238636;
  --accent-glow: rgba(57, 211, 83, 0.1);
  --border: #30363d;
  --font-display: 'JetBrains Mono', monospace;
  --font-body: 'JetBrains Mono', monospace;
  --font-mono: 'JetBrains Mono', monospace;
}
```

**Visual elements:**
- GitHub dark palette
- Terminal green for all accents
- All-monospace typography
- Subtle scan line effect (optional)
- Code block styling matches actual terminal

---

## Preset 4: Warm Editorial

**Mood:** Approachable, calm, thoughtful
**Best for:** Non-technical audiences, onboarding, culture workshops

```css
:root {
  --bg-primary: #faf9f7;
  --bg-secondary: #f5f3ee;
  --bg-card: #eee9e0;
  --text-primary: #1a1a1a;
  --text-secondary: #555555;
  --text-dim: #888888;
  --accent: #c41e3a;
  --accent-dim: #9e1830;
  --accent-glow: rgba(196, 30, 58, 0.06);
  --border: #e0dbd2;
  --font-display: 'Fraunces', serif;
  --font-body: 'Work Sans', system-ui, sans-serif;
  --font-mono: 'JetBrains Mono', monospace;
}
```

**Visual elements:**
- Warm cream background
- Serif headlines, sans-serif body
- Generous whitespace and padding
- Pull quotes with left border accent
- Elegant horizontal dividers

---

## Workshop-Specific Slide Components

These components should be available in all presets:

### Timeline Bar
Horizontal bar showing workshop blocks with proportional widths and color coding. Used on the Agenda slide.

### Poll Prompt
Full-screen question with format badge (Word Cloud, Scale 1-5, Multi-select). Large centered text, accent color for the question.

### Demo Title Card
Demo name with badge (DEMO A, DEMO B), brief description, and file path in monospace.

### Key Insight
Single statement, large text, centered, with accent color or background highlight. Used for "the one thing to remember" moments.

### Section Divider
Block name in large type with timing badge. Marks transitions between workshop blocks.
