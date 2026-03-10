---
name: workshop-sync
description: Audit and fix discrepancies between slides.html, workshop.md, and cheatsheet.html. Use after editing any one file to keep all three consistent.
---

# Workshop Sync

Audit the three workshop files for consistency and fix any discrepancies. The slides are the visual source of truth — workshop.md and cheatsheet.html must match.

## When to use

- After editing slides.html (titles, content, slide order, adding/removing slides)
- After editing workshop.md (script changes that should reflect in cheatsheet)
- Before presenting — final consistency check
- When you suspect the files have drifted apart

## Files

All three files live in the same workshop directory:

| File | Role | Authority |
|------|------|-----------|
| `slides.html` | Visual source of truth | Slide titles, order, content, and count are canonical |
| `workshop.md` | Facilitation guide | Must reference correct slide numbers, titles, and content |
| `cheatsheet.html` | Quick-glance presenter notes | Must reference correct slide numbers and match speaking notes to actual slide content |

## Audit Checklist

For each slide in `slides.html`, verify:

### 1. Slide count and numbering
- Count total slides in `slides.html` (look for `id="slide-N"`)
- Verify `workshop.md` narrative arc has correct slide ranges
- Verify `workshop.md` block slide references (e.g., "**Slides:** 3-11") match
- Verify `cheatsheet.html` format badges (e.g., "Slides 3-11") match
- Verify `cheatsheet.html` inline references ("Slide 12 should be on screen") match

### 2. Slide titles
- Extract each slide's heading text from `slides.html`
- Check `workshop.md` section headings match (e.g., `### Slide 5 — "Title Here"`)
- Check `cheatsheet.html` section labels match (e.g., `Slide 5 — Title`)

### 3. Content accuracy
For each slide, read the actual HTML and verify the speaking notes match what's visually on screen:

- **Layout references**: If the cheatsheet says "columns" but the slide uses cards, that's stale. If it says "two cards" but the slide has a grid of four, that's wrong. Match the actual visual structure.
- **Visual elements**: If a slide has a code preview, callout card, comparison cards, terminal mockups, or a grid — the cheatsheet should mention them so the presenter knows what to point at.
- **Text content**: Check that specific examples mentioned in speaking notes match what's actually written on the slide (e.g., if the slide says "Drive" but the notes say "shared folder").
- **Pill/badge text**: Verify pill text matches (e.g., "The fix" vs "How it works" vs "Contributing").
- **Stale references**: Search all three files for removed content (old tool names, old channel names, old slide structures like "MCP", wrong skill counts).
- **CTA cards**: If the closing slide has 3 cards, the cheatsheet should walk through all 3 — not summarize differently.

**This is the most important check.** Number and title mismatches are easy to spot. Content drift is subtle and causes the presenter to describe something that isn't on screen.

### 4. Structural consistency
- Each slide should have its own section heading in `workshop.md` (not lumped together unless they're genuinely a pair)
- Each slide should have a section label in `cheatsheet.html`
- `workshop.md` narrative arc table should have correct slide ranges per beat

### 5. Cross-references
- Demo slide number in cheatsheet matches actual demo slide
- Close/CTA slide number matches
- Any "advance to slide X" instructions use correct numbers

## Fix Procedure

1. Read all three files completely
2. Build a comparison table: slide number → title → workshop.md reference → cheatsheet reference
3. Report all discrepancies to the user
4. Fix them (update workshop.md and cheatsheet.html to match slides.html, unless the user says otherwise)
5. Summarize what was changed

## Output

Report in this format:

```
SYNC AUDIT — [workshop name]
Slides: [N] total

DISCREPANCIES FOUND: [count]
1. [file]: [what's wrong] → [fix applied]
2. ...

ALL SYNCED: slides.html ↔ workshop.md ↔ cheatsheet.html
```
