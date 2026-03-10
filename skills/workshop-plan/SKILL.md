---
name: workshop-plan
description: Design a workshop or presentation from scratch through guided conversation. Produces a structured workshop.md with narrative arc, timing, speaker notes, and facilitation design.
---

# Workshop Plan

Design a complete workshop or presentation through guided conversation. One question at a time, building from audience to finished facilitation document.

## When to use

- Planning a new workshop, presentation, or team session
- Restructuring an existing workshop
- Creating a facilitation-ready document from rough notes or ideas

## Output

A `workshop.md` file following the standard structure convention (see template below). This file is the single source of truth consumed by `/workshop-slides` and `/workshop-cheatsheet`.

## Process

### Phase 0: Format & Interaction Level

Ask this first — it determines the shape of everything else.

1. **Format:** "Is this a presentation (mostly one-way, you talk), an interactive workshop (exercises, polls, Q&A), or a mix?"
2. **Interaction level:** Based on the answer, set expectations:
   - **Presentation:** No polls, no structured Q&A. Focus on narrative arc and story. Cheatsheet will be speaking notes.
   - **Interactive:** Polls, exercises, Q&A. Focus on interaction design and facilitation cues.
   - **Mix:** Presentation core with targeted interaction points.

This determines whether Phases 3-4 (Interaction Design, Facilitation Cues) are needed or skipped.

### Phase 1: Audience & Goals

Ask one at a time. Do not batch.

1. **Topic:** "What's this about? One sentence."
2. **Audience:** "Who's attending? How many? What's their experience level?"
3. **Audience segments:** "Is everyone at the same level, or are there distinct groups? For example, beginners and power users, or people from different teams?" — if segments exist, note them. The narrative should speak to all groups.
4. **Duration:** "How long? Fixed slot or flexible?"
5. **Success:** "After this, what should people know, feel, or do differently?"
6. **Series context:** "Is this part of a series? What comes before/after?"

### Phase 2: Narrative Architecture

**Do NOT think in topics. Think in story beats.**

The default structure is a narrative arc:

```
Setup → Problem/Gap → Proof → Reveal/Fix → Depth → Wow moment → Action
```

Not every beat is needed. Adapt to the content. But the principle is: **tell a story, not a topic list**.

Ask the user:
1. "What are the 3-5 key things you want to cover?" — then propose a **narrative arc** with story beats and timing, not just a block list
2. "What's the 'wow moment' — the thing people will remember?" — design the arc to build toward it
3. "Are there any demos or live examples?" — design them as payoff moments in the story

**Constraints:**
- **Max block length:** 15 minutes. Anything longer must be split.
- **Narrative coherence:** Each slide/section should connect to the next with a clear "why now?" If you can't explain why section B follows section A, reorder.
- **Audience segments:** If multiple groups exist, design moments where each group sees themselves (e.g., a "two ways" comparison slide)
- **Buffer:** Leave 5-10% of total time as flex

For **interactive** workshops, also apply:
- At least one interactive element every 15 minutes (poll, Q&A, exercise)
- Alternate between passive and active blocks

### Phase 3: Interaction Design (interactive/mix only)

Skip this phase for presentations.

For each interactive element:

**Polls:** Exact question text, answer options, how to read results, when it runs
**Q&A:** Format, how many questions, prepared fallback questions (always 2)
**Demos:** What to show, step-by-step script, narration cues, fallback plan

### Phase 4: Facilitation Cues (interactive/mix only)

Skip for presentations. For presentations, the cheatsheet handles speaking notes.

For each block:
- **Opening line:** The exact first sentence
- **Transition:** The bridge phrase to the next block
- **"If X happens":** What to do if things go wrong

### Phase 5: Pre/Post Comms

- **Pre-workshop message:** Copy-paste ready (or note "not needed" for low-key sessions)
- **Post-workshop follow-up:** What to share after
- **Feedback mechanism:** How to measure success

### Phase 6: Output

Write the complete `workshop.md`. Before writing, confirm: "Here's the narrative arc — [show beat list with timing and slide mapping]. Ready to write?"

**Adapt the template to the format:**
- Presentations: include Narrative Arc section, skip Risk Mitigation / Workshop Branch / Backup Recordings unless there are demos
- Interactive workshops: include all sections
- Keep it lean — don't add sections that aren't needed

### Phase 7: Initialize CLAUDE.md & AGENTS.md

**CLAUDE.md** (repo root):
- If not present, create with: project description, available skills, active workshop info, file map
- If it exists, update the "Active Workshop" section

**AGENTS.md** (workshop directory):
```markdown
# AGENTS.md

## Available Skills

| Skill | Command | Purpose |
|-------|---------|---------|
| workshop-slides | `/workshop-slides` | Generate slide deck from workshop.md |
| workshop-cheatsheet | `/workshop-cheatsheet` | Generate facilitator cheatsheet from workshop.md |
| workshop-toggle-controls | `/workshop-toggle-controls` | Toggle keyboard controls on/off for presenting |

## Presenting

Before presenting, run `/workshop-toggle-controls` to disable keyboard intercepts so the browser handles them normally. Re-run after to restore.
```

## Workshop.md Structure Template

Adapt based on format. Sections marked (conditional) are only included when relevant.

```markdown
# Workshop Title

**Date:** [date or TBD]
**Duration:** [total time]
**Format:** [Remote/In-person], [presentation/interactive/mix]
**Audience:** [count] [role], [experience level]
**Presenters:** [names]

---

## Purpose

[1-2 sentences]

[Optional: comparison table if part of a series]

---

## Narrative Arc

[Story structure mapping beats to slides and timing]

```
Beat           →  Slides    →  Duration  →  Presenter
Setup             S1-S2        ~2 min       [name]
Problem           S3-S4        ~3 min       [name]
...
```

---

## Agenda ([total time])

```
[Start]  Block N — [Name]    [Duration]  ([Presenter])
```

---

## Block N: [Name] ([duration])

**Who:** [presenter]
**Format:** [presentation/demo/interactive]
**Slides:** [slide numbers]

### Script

[Content organized by slide, with speaking notes as natural sentences]

> **Transition:** "[bridge phrase]"

---

## Pre-Workshop (conditional)

[Copy-paste message or "not needed"]

---

## Workshop Branch (conditional — only if live demos)

[Branch setup and verification checklist]

---

## Success Criteria

| Outcome | How to tell |
|---------|------------|
| [Outcome] | [Measurement] |
```

## Design Principles

- **One question at a time.** Never batch questions.
- **Be opinionated.** Propose narrative arcs, don't ask "what structure do you want?"
- **Story over topics.** "Why does this section follow that one?" must have an answer.
- **Audience segments matter.** If there are different groups, design for all of them.
- **Adapt the template.** Don't include Risk Mitigation tables for a casual 20-minute presentation. Don't skip interaction design for a 2-hour hands-on workshop.
- **Time is sacred.** Every block has a duration. The total must add up.
