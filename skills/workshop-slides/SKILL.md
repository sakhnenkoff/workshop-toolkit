---
name: workshop-slides
description: Generate a participant-facing HTML slide deck from a workshop.md file. Single self-contained file with keyboard navigation, style presets, and workshop-specific slide types (polls, demos, agenda).
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
- Block names and durations from Agenda
- Key content points from each block (NOT speaker notes, NOT facilitation cues)
- Poll questions (just the question, big and clear — not facilitation notes about reading results)
- Demo titles and what will be shown (not the detailed script)
- Closing action items / next steps
- Series context if present

**Do NOT include in slides:**
- Speaker notes, narration cues, "say this" instructions
- "How to read results" for polls
- Facilitator assignments
- Risk mitigation tables
- Backup recording notes
- Pre/post workshop comms

### Phase 2: Style Selection

**Check for existing design context first:**
- If a `CLAUDE.md` exists with design system info (colors, fonts, tokens), use those as the starting point
- If the user specifies a brand (e.g., "use Warp/Vend tokens"), fetch tokens from the relevant source (npm, GitHub, or companion files)
- If neither, use the curated presets below

**Brand preset flow** (when user specifies a design system):
1. Look up the brand's color tokens, typography, and component conventions
2. Generate a single preview using the brand's actual tokens
3. Ask: "I've matched your brand tokens. Want to adjust anything?"
4. Proceed to generation with the brand palette

**Generic preset flow** (when no brand is specified):
Generate **3 single-slide HTML preview files** showing different visual styles. Save as `preview-1.html`, `preview-2.html`, `preview-3.html`.

Open all three in the browser and ask: "Which style do you prefer? Or pick elements from multiple."

**Available style directions** (adapt, don't use verbatim):

1. **Clean Dark** — Dark background, green/blue accent, monospace numbers, subtle grid texture. Professional tech feel.
2. **Swiss Light** — White background, bold sans-serif, red accent, strong grid, Bauhaus-inspired. Clean and precise.
3. **Terminal** — GitHub dark palette, terminal green accent, JetBrains Mono throughout, scan line effects. Developer-native.
4. **Warm Editorial** — Cream background, serif headlines, warm accent, generous whitespace. Approachable and calm.

Each preview must use the actual workshop title and meta, not placeholder text.

### Phase 3: Generate

Produce a single `slides.html` file with the selected style. Follow the companion files for CSS and JS patterns.

**Slide types to generate:**

| Slide type | Content | When |
|------------|---------|------|
| **Title** | Workshop name, date, format, duration | First slide |
| **Agenda** | Timeline bar + block list with timing | Second slide |
| **Section opener** | Block name, large, with timing badge | Before each content section |
| **Content** | Key points from the block (4-6 max per slide) | Within sections |
| **Split layout** | Heading + explanation left, visual element right | For architecture, diagrams, code previews |
| **Code preview** | Faux editor window showing actual file content | When showing config files, skill files, code |
| **Before/after** | Side-by-side comparison cards | When contrasting two states (e.g., with/without context) |
| **Poll prompt** | Just the question, large and centered, with format indicator | When a poll occurs |
| **Demo title** | Demo name + what will be shown, inverted dark bg | Before demo sections — signal energy shift |
| **Key insight** | Single impactful statement, inverted dark bg | For "the one thing to remember" moments |
| **Action / CTA** | Next steps cards + highlight banner | Closing slides |

**Layout variety is critical.** Alternate between centered, left-aligned, split, and inverted slides. Never use the same layout for 3+ consecutive slides.

**Content density rules:**
- Title slides: heading + subtitle only
- Content slides: 4-6 bullets OR 2 short paragraphs maximum
- Poll slides: question only (+ format badge like "Word Cloud" or "Scale 1-5")
- If content exceeds limits, automatically split across multiple slides

**Required features:**
- Keyboard navigation: arrow keys, space to advance, Home/End for first/last
- Slide counter (current / total) in bottom corner
- Each slide fits exactly in viewport (`100vh`, no scrolling)
- `prefers-reduced-motion` support
- All fonts from Google Fonts or Fontshare (no system fonts for display)
- Well-commented CSS and JS for easy manual tweaking

### Phase 4: Update CLAUDE.md

After generating slides, create or update the `CLAUDE.md` in the repo root with:
- Design system reference (selected style preset, color tokens, typography, component patterns)
- Slide architecture (number of slides, types, order)
- Available skills reference
- File map (which files exist, what they do)
- Conventions (viewport rules, animation classes, keyboard shortcuts)

This ensures future Claude Code sessions in the repo have full context about design decisions.

**If CLAUDE.md already exists:** merge new design information into it, don't overwrite unrelated sections.

### Phase 5: Generate AGENTS.md

Create or update an `AGENTS.md` in the workshop directory (same level as `slides.html`) that lists available workshop skills for any Claude Code session working in that directory:

```markdown
# AGENTS.md

## Available Skills

| Skill | Command | Purpose |
|-------|---------|---------|
| workshop-slides | `/workshop-slides` | Regenerate slide deck from workshop.md |
| workshop-cheatsheet | `/workshop-cheatsheet` | Generate facilitator cheatsheet from workshop.md |
| workshop-toggle-controls | `/workshop-toggle-controls` | Toggle all keyboard controls on/off for presenting |

## Files

- `workshop.md` — source of truth (facilitation guide)
- `slides.html` — participant-facing slide deck
- `cheatsheet.html` — facilitator cheatsheet (if generated)

## Presenting

Before presenting, run `/workshop-toggle-controls` to disable keyboard intercepts (arrows, Space, Home/End, F) so the browser handles them normally. Re-run after presenting to restore controls for development.
```

**If AGENTS.md already exists:** merge the skills table and presenting section, don't overwrite other content.

### Phase 6: Deliver

1. Write `slides.html` to the same directory as the `workshop.md`
2. Clean up preview files (delete `preview-*.html`)
3. Open the slides in the browser: `open slides.html`
4. Tell the user: "Arrow keys to navigate. Press F for fullscreen."

## HTML Architecture

Follow the patterns from the companion `viewport-base.css` (in this skill directory) for responsive scaling.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>[Workshop Title]</title>
  <!-- Google Fonts link -->
  <!-- All CSS inline -->
</head>
<body>
  <div class="slide" id="slide-1">
    <div class="slide-content">
      <!-- Slide content here -->
    </div>
  </div>
  <!-- More slides... -->

  <div class="slide-counter">
    <span id="current">1</span> / <span id="total">N</span>
  </div>

  <div class="nav-dots" id="dots">
    <!-- Generated by JS -->
  </div>

  <!-- All JS inline -->
</body>
</html>
```

## JavaScript Requirements

```javascript
class SlidePresentation {
  // Keyboard: ArrowRight/Space = next, ArrowLeft = prev, Home/End
  // Touch: swipe left/right on mobile
  // Mouse wheel: scroll between slides
  // Progress dots: clickable navigation
  // Intersection Observer: trigger .visible class for entrance animations
  // Slide counter: update current/total display
}
```

## Design Principles

- **Participant-facing.** This is what people see on the shared screen. Clean, clear, no facilitator noise.
- **One idea per slide.** If you're putting more than one concept on a slide, split it.
- **Viewport-locked.** Every slide is exactly `100vh`. Content must fit. Use `clamp()` for responsive typography.
- **Distinctive, not generic.** Avoid the default AI presentation look. Use the curated style presets.
- **Code-friendly.** Use monospace for code snippets, file paths, command examples. Good syntax highlighting.
