---
name: workshop-cheatsheet
description: Generate a facilitator cheatsheet HTML from a workshop.md file. Block-focused view with timing, speaker notes, poll text, and keyboard navigation — designed for glancing at during live facilitation.
---

# Workshop Cheatsheet Generator

Generate a single-file HTML facilitator cheatsheet from a `workshop.md`. The cheatsheet shows one block at a time with everything the facilitator needs in that moment.

## When to use

- After creating or updating a `workshop.md` (via `/workshop-plan` or manually)
- Before rehearsing or delivering a workshop
- When the existing cheatsheet needs regenerating after content changes

## Input

Path to a `workshop.md` file. If not provided, ask the user.

## Process

### Step 1: Parse

Read the `workshop.md` and extract:
- **Meta:** Title, date, duration, format, audience
- **Blocks:** For each `## Block N:` section, extract:
  - Block name and duration (from the heading)
  - Start time (from the Agenda section)
  - Facilitator (from the **Who:** line)
  - Format (from the **Format:** line)
  - Script content (all numbered steps, quotes, narration cues)
  - Poll specifications (content inside code blocks starting with `POLL`)
  - Demo steps (numbered steps under demo headings)
  - Transition phrase (content after `> **Transition:**`)
  - Risk mitigations relevant to this block (from the Risk Mitigation table)
  - Fallback notes (lines containing "If it fails" or "backup" or "fallback")

### Step 2: Generate

Produce a single `cheatsheet.html` file. Read the companion `cheatsheet-template.md` for the full HTML/CSS/JS specification.

**Key UX requirements:**
- One block fills the entire screen — no scrolling within a block
- Left/right arrow keys navigate between blocks
- Progress bar shows position in workshop timeline
- Timer shows elapsed time within current block
- Clean, light design — this is a tool, not a presentation
- Each block shows: timing, speaker notes, poll text, demo steps, transition cue, fallback

### Step 3: Deliver

1. Write the file to the same directory as the `workshop.md`, named `cheatsheet.html`
2. Open it in the browser: `open cheatsheet.html`
3. Tell the user about keyboard shortcuts

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `←` / `→` | Navigate between blocks |
| `t` | Toggle timer (start/pause countdown for current block) |
| `n` | Preview next block (overlay) |
| `Escape` | Close next-block preview |
| `Home` | Jump to first block |
| `End` | Jump to last block |

## Design Principles

- **Teleprompter, not presentation.** The facilitator glances at it and instantly knows what to say and do.
- **One block = one screen.** Never scroll within a block. If content overflows, increase font hierarchy and trim.
- **Light theme only.** High contrast, readable text. The facilitator's screen might be in a bright room.
- **No animations.** Instant transitions between blocks. This is a utility.
- **Large type for speaker notes.** The facilitator is looking at participants, glancing at the cheatsheet.
