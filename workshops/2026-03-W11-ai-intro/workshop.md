# Workshop 1: AI in Our Repo — Introduction

**Date:** Week of March 9-13, 2026
**Duration:** ~30-35 minutes (flexible)
**Format:** Remote, shared screen presentation + one live demo
**Audience:** iOS community, mixed experience levels
**Presenters:** Matvii (presentation) + Benjamin (Superpowers demo)

---

## Purpose

A low-key introduction to the AI infrastructure in our iOS repo. Most people already use Claude in some form — they don't know what's been built into the repo to make it dramatically better, how it's structured, or how it evolves.

| This workshop | The March 25 workshop |
|---------------|----------------------|
| Watch and learn | Hands-on exercises |
| "Here's what we've built" | "Now you use it" |
| No setup required | Everyone needs Claude Code installed |
| Tour the system | Contribute to it |

### Workshop ambition alignment

| Pillar | How this workshop delivers |
|--------|---------------------------|
| **Low key** | No polls, no structured Q&A, conversational tone, ~30 min |
| **Concrete** | Real files shown (AGENTS.md, rules/, skills/), real demo (Android→iOS port) |
| **Actionable** | Setup link, Slack channel, "try one thing this week" |
| **Inspiring** | Benjamin's Superpowers demo is the wow moment |

---

## Agenda (~30-35 min)

```
 0:00  Block 1 — Opening                          2 min
 0:02  Block 2 — The Three Levels                 12 min
 0:14  Block 3 — Superpowers Demo (Benjamin)      15 min
 0:29  Block 4 — Close + Next Steps                5 min
 0:34  End
```

---

## Block 1: Opening (2 min)

**Who:** Matvii
**Format:** Presentation — one slide

### Script

No preamble. No agenda slide. Straight in:

> "Our repo has a growing AI layer. Most of you have used Claude in some form — but you might not know what's been built into the repo to make it dramatically better. This is a quick tour of what exists, how it's structured, and how you can start using it."

> **Transition:** "Let me show you how this works — starting with what most of us do today."

---

## Block 2: The Three Levels (12 min)

**Who:** Matvii
**Format:** Presentation with file walkthroughs on screen

### Script

#### Level 1: Use Claude for Coding (~2 min)

One slide. Quick and relatable:

- "Most of us are somewhere here — you paste code into ChatGPT, use Copilot suggestions, or run Claude in the terminal"
- "It works. You get answers. But Claude doesn't know we use Warp tokens instead of hardcoded colors, or that we prefer Swift Testing over XCTest, or how our modules are structured"
- "It's like hiring a great Swift developer who's never seen our codebase"

> Don't dwell on this. Everyone gets it. Move on.

#### Level 2: Give Claude Context (~6 min)

This is the key section. Don't sell the idea of context — they know Claude gets smarter in the repo. Instead, **demystify the architecture**.

**Slide: "Where does the context come from?"**

Show the layered architecture:
```
~/.claude/            ← your personal preferences (global, not shared)
CLAUDE.md             ← repo entry point (in git)
AGENTS.md             ← policies & architecture (in git)
.claude/rules/        ← always-on context (in git)
.claude/skills/       ← on-demand workflows (in git)
```

- "When you run Claude inside the repo, it reads all of this before answering a single question"

**Slide: "What's in AGENTS.md?"**

Open the actual file on screen. Don't read it — scroll through and narrate the sections:
- "Project overview — tells Claude this is a modular SPM codebase for FINN, Tori, DBA, Blocket"
- "Architecture — module structure, Drive as canonical shared UI, workspace layout"
- "Engineering policies — SwiftLint rules, localization workflow, Warp design system, concurrency settings"
- "Available skills — 17 skills listed with descriptions"
- "CI and testing — snapshot test config, build verification"

The point: show the **density** of knowledge Claude has access to.

**Slide: "Rules are always loaded"**

Show `.claude/rules/` folder:
- "These are always in context. Like our Unleash CLI reference — Claude can look up toggle commands without you explaining them"
- "Module-specific AGENTS.md files add domain context for verticals like Recommerce"

**Slide: "The key insight"**

> "Same question to Claude. Completely different answer. The only difference is where you run it. And you get this for free — it's all in git, it loads automatically."

**Slide: "How this evolves"**

Light touch — tease, don't teach:
- "We have a contribution policy. Not everything goes in AGENTS.md"
- "Stable rules → AGENTS.md. Repeatable workflows → skills. Long references → Documentation/"
- "If you notice Claude getting something wrong, or your team has a pattern worth sharing — there's a process for that"
- "We'll dig into contributing in the March 25 workshop"

#### Level 3: Skills, Agents & MCP (~3 min)

**Slide: "Repeatable workflows"**

- "Once Claude knows our project, you can teach it workflows. That's what skills are."
- "Skills are Markdown files with step-by-step instructions. We have 17."

Flash the skill list (don't explain each one — just the names and the volume):
- Daily: `/ios-pre-push`, `/ios-pr`, `/ios-review-code`, `/ios-write-unit-test`
- Building: `/ios-create-new-module`, `/ios-plan-feature`, `/ios-warp-design-system`
- CI: `/ios-ci-workflow-triage`, `/ios-run-snapshot-tests`

**Slide: "And it connects to tools"**

- "MCP servers connect Claude to external systems — Jira, Confluence, Amplitude, Xcode"
- "You can ask Claude to check a Jira ticket, look up analytics, or build your project"

**Bridge to Benjamin:**

> "But instead of me talking about what Level 3 looks like — Benjamin is going to show you. And he picked a use case that I think will blow your mind."

---

## Block 3: Superpowers Demo (15 min)

**Who:** Benjamin
**Format:** Live demo, shared screen

### Purpose

Show Level 3 in action with a concrete, impressive use case: **porting a feature from the Android repo to iOS** using Superpowers.

### What Benjamin shows

1. **Brainstorming** — using the brainstorming skill to analyze the Android feature and plan the iOS implementation
2. **Planning** — assembling an implementation plan from the brainstorm output
3. **Subagents** — launching parallel agents that work across both repos (Android for reference, iOS for implementation)
4. **The result** — the agent produces working code in the iOS repo, informed by the Android implementation

### Why this demo

- **Concrete:** A real problem developers face (cross-platform feature parity)
- **Inspiring:** The agent works across two repos simultaneously — something that's hard for humans to do efficiently
- **Actionable:** People can try Superpowers themselves after seeing this

### After the demo

Matvii briefly reacts if natural: "So that's what Level 3 looks like in practice — repeatable workflows, agents that understand both codebases, and you can run this yourself."

---

## Block 4: Close + Next Steps (5 min)

**Who:** Matvii
**Format:** Presentation — one or two slides

### Script

Three things. Quick, specific, actionable:

1. **"Here's how to start"**
   - Share setup guide link in the meeting chat
   - "Install Claude Code, run `claude --version`, you're done"

2. **"Here's where to talk about it"**
   - "#ios-ai-workflows in Slack — post wins, questions, skill ideas"
   - Make channel public at this moment if not already

3. **"Try one thing this week"**
   - "Run Claude inside the repo. Ask it to review a file, explain some code, or just explore"
   - "Check out the skills list in AGENTS.md — see if any match your workflow"
   - "Post what happened in Slack"

**Tease March 25:**

> "Next workshop is hands-on. You'll run skills yourself, write tests, create PRs. Get Claude Code installed before then — the setup guide is in the chat."

---

## Pre-Workshop (optional, light touch)

No formal pre-workshop Slack message needed. If desired, a casual heads-up:

```
Quick heads-up — at this week's iOS community session we'll do a short tour
of the AI tooling built into our repo. No setup needed, just show up.

If you want to be ready to try things after: install Claude Code and
run `claude --version` to verify.
```

---

## Success Criteria

| Outcome | How to tell |
|---------|------------|
| People understand the context architecture | They can name CLAUDE.md, AGENTS.md, rules, skills |
| People know skills exist | They reference specific skill names or check the list |
| Setup starts happening | Messages in #ios-ai-workflows |
| March 25 is anticipated | People ask about it or set up Claude Code |
| Nobody felt lectured at | Felt like a tour, not a class |

---

## Related

- [March 25 hands-on workshop](../2026-03-25-ai-hands-on/workshop.md)
