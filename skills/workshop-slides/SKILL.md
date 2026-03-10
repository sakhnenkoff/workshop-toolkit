---
name: workshop-slides
description: Generate a participant-facing HTML slide deck from a workshop.md file. Single self-contained file with keyboard navigation, style presets, narrative coherence checks, and workshop-specific slide types.
---

# Workshop Slides Generator

Generate a presentation slide deck from a `workshop.md`. Produces a single HTML file with zero dependencies — just open in a browser and present.

## When to use

- After creating or updating a `workshop.md` (via `/workshop-plan` or manually)
- When you need participant-facing slides for a workshop
- When regenerating slides after content changes

## Input

Path to a `workshop.md` file. If not provided, ask the user.

## Process

### Phase 1: Parse

Read the `workshop.md` and extract **participant-facing content only**:

- Title, date, format from meta section
- Narrative arc (if present) — this determines slide order, which may differ from block order
- Key content points from each block (NOT speaker notes, NOT facilitation cues)
- Poll questions (just the question, big and clear)
- Demo titles and what will be shown (not the detailed script)
- Closing action items / next steps

**Do NOT include in slides:**
- Speaker notes, narration cues, "say this" instructions
- "How to read results" for polls
- Facilitator assignments, risk tables, backup recording notes, pre/post comms

**Important:** Slides may **reinterpret** the workshop.md content. The facilitation doc is structured for the presenter; slides are structured for the audience. The narrative arc may require reordering, reframing, or adding new visual angles that aren't in the text.

### Phase 2: Style Selection

**Resolution order — check these in sequence:**

1. **CLAUDE.md** — if it exists in the repo root with design system info, use that theme
2. **Saved themes** — check `~/Developer/workshop-toolkit/themes/` for reusable theme files. If the user says "use Vend theme" or "same theme as last time", load the matching `.md` file from this directory
3. **User-specified brand** — if they name a design system (e.g., "use Warp/Vend tokens"), fetch tokens and create the theme
4. **Generic presets** — if none of the above, use the curated presets below

**Saved theme flow** (preferred for repeat workshops):
1. Read the theme file (e.g., `themes/vend.md`) — it has all CSS variables, fonts, component patterns, and slide-specific conventions
2. Generate a single preview using the saved theme
3. Ask: "Using the [theme name] theme. Want to adjust anything?"

**Generic preset flow:**
Generate 3 single-slide HTML previews. Open all three and ask the user to pick.

**Available style directions** (adapt, don't use verbatim):

1. **Clean Dark** — Dark background, green/blue accent, monospace numbers, subtle grid. Professional tech feel.
2. **Swiss Light** — White background, bold sans-serif, red accent, strong grid, Bauhaus-inspired.
3. **Terminal** — GitHub dark palette, terminal green, JetBrains Mono throughout. Developer-native.
4. **Warm Editorial** — Cream background, serif headlines, warm accent, generous whitespace.

Each preview must use the actual workshop title, not placeholder text.

**Saving new themes:** If the user creates a new theme (via brand tokens or customization), offer to save it to `~/Developer/workshop-toolkit/themes/[name].md` for reuse.

### Phase 3: Generate

Produce a single `slides.html` file with the selected style.

**Slide types:**

| Slide type | Content | When |
|------------|---------|------|
| **Title** | Workshop name, date, format, duration | First slide |
| **Setup / hook** | Relatable opening that creates curiosity | After title — replaces dry agenda slides |
| **Comparison** | Side-by-side cards contrasting two states | For "outside vs inside", "before vs after" |
| **Split layout** | Heading + explanation left, visual right | Architecture, diagrams, code previews |
| **Code preview** | Faux editor window with file content | Config files, skill files, actual code |
| **Content** | Key points (4-6 max per slide) | Within sections |
| **Key insight** | Single statement, inverted dark bg | "The one thing to remember" — dramatic pause |
| **Demo title** | Demo name + description, inverted dark bg | Before demo — signals energy shift |
| **Action / CTA** | Next steps cards + highlight banner | Closing |

**Layout variety is critical.** Alternate between centered, left-aligned, split, and inverted slides. Never use the same layout for 3+ consecutive slides.

**Content density rules:**
- Title slides: heading + subtitle only
- Content slides: 4-6 bullets OR 2 short paragraphs maximum
- If content exceeds limits, automatically split across slides

### Phase 4: Narrative Coherence Check

After generating, audit the full slide sequence:

1. **Repetition check:** Do any two slides show the same examples or make the same point? If so, differentiate them — each slide must add something new.
2. **Transition logic:** For each slide, ask "why does this follow the previous one?" If there's no clear answer, reorder or add a bridge.
3. **Density audit:** Flag any slide with fewer than 3 visual elements. Thin slides feel empty on a full viewport — enrich them or merge with adjacent slides.
4. **Audience test:** If multiple audience segments exist, verify that each group has at least one "I see myself" moment in the first few slides.

Report any issues to the user before delivering.

### Phase 5: Update CLAUDE.md

Create or update `CLAUDE.md` in the repo root with:
- Design system reference (colors, fonts, tokens, component patterns)
- Slide architecture (number, types, order)
- Available skills reference
- File map and conventions

**If CLAUDE.md already exists:** merge, don't overwrite.

### Phase 6: Generate AGENTS.md

Create or update `AGENTS.md` in the workshop directory:

```markdown
# AGENTS.md

## Available Skills

| Skill | Command | Purpose |
|-------|---------|---------|
| workshop-slides | `/workshop-slides` | Regenerate slide deck from workshop.md |
| workshop-cheatsheet | `/workshop-cheatsheet` | Generate facilitator cheatsheet from workshop.md |
| workshop-toggle-controls | `/workshop-toggle-controls` | Toggle keyboard controls on/off for presenting |

## Files

- `workshop.md` — source of truth (facilitation guide)
- `slides.html` — participant-facing slide deck
- `cheatsheet.html` — facilitator cheatsheet (if generated)

## Presenting

Before presenting, run `/workshop-toggle-controls` to disable keyboard intercepts so the browser handles them normally. Re-run after to restore.
```

### Phase 7: Deliver

1. Write `slides.html` to the same directory as the `workshop.md`
2. Clean up preview files (delete `preview-*.html`)
3. Open in browser: `open slides.html`
4. Tell the user: "Arrow keys to navigate. Press F for fullscreen."

## HTML Architecture

Follow the companion `viewport-base.css` for responsive scaling.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>[Workshop Title]</title>
  <!-- All CSS inline, all JS inline -->
</head>
<body>
  <div class="slide" id="slide-1">
    <div class="slide-inner"><!-- content --></div>
  </div>
  <div class="slide-counter">
    <span id="current">1</span> / <span id="total">N</span>
  </div>
</body>
</html>
```

## JavaScript Requirements

- Keyboard: ArrowRight/Space/ArrowDown = next, ArrowLeft/ArrowUp = prev, Home/End, F = fullscreen
- Intersection Observer: trigger `.visible` class for staggered entrance animations (`.reveal .d1-.d7`)
- Touch: swipe support
- Slide counter + progress bar updates

## Design Principles

- **Participant-facing.** Clean, clear, no facilitator noise.
- **One idea per slide.** If you're putting more than one concept, split it.
- **Viewport-locked.** Every slide is exactly `100vh`. Use `clamp()` for responsive typography.
- **Story, not list.** The slides tell a narrative. Each one connects to the next.
- **Distinctive, not generic.** Use curated style presets or brand tokens. Avoid default AI presentation aesthetics.
