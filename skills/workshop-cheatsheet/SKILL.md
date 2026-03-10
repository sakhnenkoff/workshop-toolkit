---
name: workshop-cheatsheet
description: Generate a facilitator cheatsheet HTML from a workshop.md file. Conversational speaking notes with slide references, block-focused view, timer, and keyboard navigation — reads like a teleprompter in the presenter's voice.
---

# Workshop Cheatsheet Generator

Generate a single-file HTML facilitator cheatsheet from a `workshop.md`. Shows one block at a time with everything the facilitator needs: what to say, which slide they're on, and when to transition.

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
- **Blocks:** For each `## Block N:` section:
  - Block name, duration, start time (from Agenda)
  - Facilitator (from **Who:**), format (from **Format:**)
  - Slide references (from **Slides:** line)
  - Script content — all speaking notes, quotes, narration cues
  - Demo steps
  - Transition phrases (from `> **Transition:**`)

### Step 1.5: Read context

Style the cheatsheet consistently with the slides. Check these in order:
1. **CLAUDE.md** in the repo root — if it has design system info, use it
2. **Saved themes** in `~/Developer/workshop-toolkit/themes/` — if the user specifies a theme name, load it
3. **Slides file** — if `slides.html` exists in the same directory, extract font and color choices from it

The cheatsheet should feel like it belongs to the same visual family as the slides — same fonts and accent colors — but with a light, utility-focused design. Theme files include a "Cheatsheet Styling" section with specific guidance.

### Step 2: Generate

Produce a single `cheatsheet.html` file. Read the companion `cheatsheet-template.md` for HTML/CSS/JS patterns.

**Key UX requirements:**
- One block fills the entire screen — no scrolling within a block
- Left/right arrow keys navigate between blocks
- Progress bar shows position in workshop timeline
- Timer shows elapsed time within current block

**Content style — this is critical:**

Speaker notes must be written as **conversational speech in the presenter's voice**, not as formal instructions. The facilitator should be able to glance at the cheatsheet and read directly from it.

| Wrong (instructions) | Right (speech) |
|---|---|
| "Acknowledge the tools the audience uses" | "So, most of us already use some form of AI when we code — ChatGPT, Copilot, whatever works for you." |
| "Explain the key insight about context" | "Same question to Claude. Completely different answer. And you get this for free." |
| "Transition to the demo section" | "But instead of me just talking about it — Benjamin is going to show you." |

**Note types:**
- **Quotes** (accent left border) — what to actually say, in the presenter's natural voice
- **Small italic text** — stage directions (advance slide, pause, point at something)
- **Note items** (gray left border) — reminders about what's on screen or what to do

**Per-block content:**
- **Slide references** — which slides this block covers (shown as pills at the top)
- **Per-slide sections** — labeled with slide number and title, each with speaking notes
- **Transition** — the bridge phrase to the next block, as a speakable quote

### Step 3: Update CLAUDE.md

If a `CLAUDE.md` exists, add/update the cheatsheet entry in the file map.

### Step 4: Deliver

1. Write `cheatsheet.html` to the same directory as `workshop.md`
2. Open in browser: `open cheatsheet.html`
3. Tell the user about keyboard shortcuts

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `←` / `→` | Navigate between blocks |
| `t` | Toggle timer (start/pause elapsed time) |
| `n` | Preview next block (overlay) |
| `Escape` | Close next-block preview |
| `Home` | Jump to first block |
| `End` | Jump to last block |

## Design Principles

- **Teleprompter, not documentation.** Write notes the presenter can read aloud. Full sentences, natural tone, their voice.
- **One block = one screen.** Never scroll within a block.
- **Slide references are anchors.** Each section within a block is labeled with its slide number so the presenter knows where they are.
- **Light theme only.** High contrast, readable text. Bright room friendly.
- **No animations.** Instant transitions. This is a utility tool.
- **Large type for quotes.** The presenter is looking at participants, glancing at the cheatsheet.
