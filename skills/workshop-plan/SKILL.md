---
name: workshop-plan
description: Design a workshop from scratch through guided conversation. Produces a structured workshop.md with full facilitation design — timing, polls, demos, speaker notes, fallback plans, and pre/post comms.
---

# Workshop Plan

Design a complete workshop through guided conversation. One question at a time, building from audience to finished facilitation document.

## When to use

- Planning a new workshop, training session, or team presentation
- Restructuring an existing workshop
- Creating a facilitation-ready document from rough notes or ideas

## Output

A `workshop.md` file following the standard structure convention (see template below). This file is the single source of truth consumed by `/workshop-slides` and `/workshop-cheatsheet`.

## Process

### Phase 1: Audience & Goals

Ask these one at a time. Do not batch questions.

1. **Topic:** "What's this workshop about? One sentence."
2. **Audience:** "Who's attending? How many? What's their experience level with this topic?"
3. **Format:** "Remote or in-person? Duration? Is it standalone or part of a larger session?"
4. **Success:** "After this workshop, what should people know, feel, or do differently?"
5. **Series context:** "Is this part of a series? If so, what comes before/after?"

### Phase 2: Content Architecture

Design the block structure. Apply these constraints:

- **Energy arc:** Open with engagement (poll/question), deepen with content, interact in the middle, close with action
- **Max block length:** 15 minutes. Anything longer must be split.
- **Interaction frequency:** At least one interactive element every 15 minutes (poll, Q&A, demo, exercise)
- **Block types:** Opening, Content, Demo, Interaction (poll/Q&A/exercise), Close
- **Buffer:** Always leave 5-10% of total time as flex/buffer

Ask the user:
1. "What are the 3-5 key things you want to cover?" — then propose a block structure with timing
2. "Which blocks should be interactive vs presentation?" — adjust based on answer
3. "Any demos or live examples you want to include?" — design demo blocks with scripts

### Phase 3: Interaction Design

For each interactive element, design the full specification:

**Polls:**
- Exact question text
- Answer options (for multiple choice) or format (word cloud, scale)
- How to read and respond to results ("If mostly X, say Y")
- When in the timeline it runs

**Q&A:**
- Format (live questions, upvoted Q&A tool, chat)
- How many questions to take
- Prepared fallback questions (always have 2)

**Demos:**
- What file/tool/screen to show
- Step-by-step script
- What to narrate during each step
- Fallback plan if it fails

### Phase 4: Facilitation Cues

For each block, write:
- **Opening line:** The exact first sentence to say
- **Transition to next block:** The bridge phrase
- **"If X happens" notes:** What to do if things go wrong, audience is quiet, time runs over

### Phase 5: Pre/Post Comms

- **Pre-workshop message:** Copy-paste ready Slack/email message to send before the workshop
- **Setup checklist:** What facilitators need to prepare (tools, accounts, branches, recordings)
- **Post-workshop follow-up:** What to share after (recording, links, next steps)
- **Feedback mechanism:** How to measure success

### Phase 6: Output

Write the complete `workshop.md` following the structure template below. Save it to the workshop directory specified by the user.

Before writing, confirm the full structure with the user: "Here's the workshop at a glance — [show block list with timing]. Ready to write?"

## Workshop.md Structure Template

The output MUST follow this structure exactly. This enables `/workshop-slides` and `/workshop-cheatsheet` to parse it.

```markdown
# Workshop Title

**Date:** [date or TBD]
**Duration:** [total time]
**Format:** [Remote/In-person], [tools used]
**Audience:** [count] [role], [experience level]
**Facilitators:** [names or TBD]

---

## Purpose

[1-2 sentences on what this workshop achieves]

[Optional: comparison table if part of a series]

---

## Pre-Workshop Actions

### [Timing] ([description])

**[Channel] message to send** (copy-paste ready):

```
[Message text]
```

### Before the workshop

#### [Tool] Setup
- [ ] [Setup step]

#### Other Prep
- [ ] [Prep step]

---

## Agenda ([total time])

```
[Start] Block N - [Name]    [Duration]
```

---

## Block N: [Name] ([duration])

**Who:** [facilitator]
**Format:** [presentation/demo/interactive]

### Script

[Numbered steps with exact words to say in quotes]
[Poll specifications in code blocks]
[Demo steps with narration cues]

> **Transition:** "[Bridge phrase to next block]"

---

## Workshop Branch (Sandbox)

[If demos exist: branch setup instructions and verification checklist]

---

## Backup Recordings

[If demos exist: list of recordings to prepare]

---

## Facilitator Assignments

| Block | Facilitator | Backup |
|-------|-------------|--------|
| [Block name] | TBD | TBD |

---

## Risk Mitigation

| Risk | Mitigation |
|------|-----------|
| [Risk] | [What to do] |

---

## Success Criteria

| Outcome | How to tell |
|---------|------------|
| [Outcome] | [Measurement] |
```

## Design Principles

- **One question at a time.** Never batch questions. Wait for the answer before asking the next.
- **Be opinionated.** Propose block structures, don't ask "what blocks do you want?" Say "I'd suggest 5 blocks like this — what do you think?"
- **Energy arc matters.** Don't put all content blocks in a row. Alternate between passive and active.
- **Write for glanceability.** Speaker notes should be scannable during a live session, not dense paragraphs.
- **Always have fallbacks.** Every demo needs a backup. Every Q&A needs prepared questions. Every tool needs a plan B.
- **Time is sacred.** Every block has a duration. The total must add up. Include buffer.
