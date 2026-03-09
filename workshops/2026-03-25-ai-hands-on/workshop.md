# AI-First Development Workshop

**Date:** March 25, 2026
**Duration:** ~2 hours
**Format:** Remote (digital breakout rooms available)
**Facilitators:** Allan, Matvii, breiby, Vilde (+ dAI support)
**Audience:** Mixed — beginners to power users across all verticals and markets

---

## Goals

1. **Use it** — Everyone can run existing AI skills in their daily work
2. **Understand it** — Everyone knows how AGENTS.md, skills, and context work together
3. **Extend it** — At least some participants feel confident contributing new skills
4. **Sustain it** — Post-workshop mechanisms are launched to keep momentum

## Blockers We're Addressing

| Blocker | How the workshop tackles it |
|---------|---------------------------|
| Awareness | Pre-prepared demos on real codebase files |
| Setup friction | Pre-workshop setup guide + verification deadline |
| Trust/skepticism | Demos use real files from real verticals — not toy examples |
| Contribution barrier | Show-and-tell of skill anatomy + contributing guide |

---

## Pre-Workshop Preparation (1 week before)

### For Organizers

#### Setup & Logistics
- [ ] Send the **Setup Guide** (see below) to all participants — deadline: 3 days before workshop
- [ ] Create `#ios-ai-workflows` Slack channel (keep it private until workshop day)
- [ ] Prepare a shared board (Miro/FigJam) with the pain point survey results clustered by theme
- [ ] Print/prepare the **Cheat Sheet** (see below) for sharing during hands-on

#### Rehearsing the Demos (Critical)
- [ ] Each facilitator rehearses their assigned demo(s) at least twice
- [ ] Time each demo — must fit in 8 min or cut scope
- [ ] Verify every file path still exists on latest `master`
- [ ] Record the expected output for each demo so you can show screenshots if Claude is slow or misbehaves
- [ ] Prepare a "plan B" for each demo: if the skill hangs or produces bad output, have a pre-recorded terminal recording (asciinema or screen recording) ready

#### Pain Point Survey (Context, Not Content)
- [ ] Send async form: *"Name one repetitive task in your iOS workflow you'd love to automate or speed up"*
- [ ] Cluster results by theme (testing, PR creation, code review, Warp compliance, localization, etc.)
- [ ] Map each cluster to existing skills or note "no skill yet"
- [ ] Use this to **frame** the demos: "Many of you said X — here's how we solve that"
- [ ] The survey results do NOT change the demos — the demos are pre-prepared and rehearsed

### For Participants

```
AI Workshop Setup — Complete by March 22

1. Install Claude Code
   Follow internal setup guide at [link to your internal docs]

2. Verify your API key
   Run: claude --version
   Expected: version number, no auth errors

3. Pull latest master
   cd ~/path/to/ios-app
   git checkout master && git pull

4. Verify the AI context loads
   Run: claude "List the available /ios- skills"
   Expected: You should see skills like ios-pre-push, ios-pr,
   ios-write-unit-test, etc.

5. Fill out the survey
   [link to pain point form]
   Question: "Name one repetitive task you'd love to automate
   or speed up"

Trouble? Post in #ios-ai-workshop Slack channel.
```

### Setup Verification Checkpoint (2 days before)
- [ ] Check who has NOT confirmed setup
- [ ] Ping them directly — unresolved setup on workshop day is the #1 time killer
- [ ] Have a 15-min "setup clinic" slot available the day before for stragglers

---

## Workshop Agenda (120 minutes)

### Block 1: Welcome & Context (10 min)

**Who:** Allan
**Format:** Presentation (shared screen)

Content:
- Why AI-first development matters for NMP
- Quick stats: "We have 17 skills, AGENTS.md with 50+ policies, and growing"
- Show the pain point survey results: "Here's what you told us annoys you most"
- Frame the session: "We've prepared demos that solve exactly these problems"
- Acknowledge mixed audience: "Whether this is your first time or you use it daily, you'll get value"

Key message: AI in this repo isn't a chatbot — it's infrastructure. Skills, AGENTS.md, rules, and docs form a system that makes the agent understand our codebase, conventions, and architecture.

---

### Block 2: Demos (35 min)

**Who:** Matvii (primary), Allan/breiby as backup
**Format:** Shared screen, live coding with narration

**Rules for the demo person:**
- Talk through what you're doing and WHY at every step
- Narrate what the agent "knows" and where that knowledge comes from
- Keep to time — 8 min max per demo, use a visible timer
- If something breaks: switch to the backup recording, explain what should have happened, move on

#### Demo 1: "Generate unit tests for a ViewModel" (~8 min)

**File:** `Jobs/Sources/JobProfile/Internal/ViewModel/UserDetailsFormViewModel.swift`
**What it is:** 89-line ViewModel that validates user form fields (name, email, phone) using Combine. No tests exist yet.

**Script:**
1. Open the file, briefly show the code: "This is a real ViewModel from Jobs. It validates form fields. It has zero tests."
2. Run: `claude "/ios-write-unit-test UserDetailsFormViewModel.swift"`
3. While it runs, narrate: "Notice it's using Swift Testing, not XCTest — because AGENTS.md tells it to. It generates Given/When/Then structure and creates protocol-based mocks."
4. Show the generated test file
5. Run the tests: `swift test --package-path Jobs --filter UserDetailsForm`
6. Show tests passing

**What to highlight:**
- The agent knew to use Swift Testing (project policy)
- It created proper mocks using protocols (project pattern)
- It covered success AND failure cases
- The exact test command was suggested

**If it fails:** Show pre-recorded output. Say: "The agent sometimes needs a second try — the important thing is it knows our conventions."

---

#### Demo 2: "Review a view for Warp design system compliance" (~8 min)

**File:** `RealEstate/Sources/RealEstateItemPage/Internal/ObjectPageSegments/Segments/FraudInfoBox/FraudInfoBoxView.swift`
**What it is:** 59-line SwiftUI view with hardcoded `.padding(16)`, `RoundedRectangle(cornerRadius: 8)`, and non-Warp colors.

**Script:**
1. Open the file, point out the hardcoded values: "See `.padding(16)` on line 27? And `cornerRadius: 8` on line 34?"
2. Run: `claude "Review FraudInfoBoxView.swift for Warp design system compliance"`
3. Show how the agent maps each hardcoded value:
   - `.padding(16)` -> `Warp.Spacing.spacing200`
   - `cornerRadius: 8` -> `Warp.Border.borderRadius100`
   - `strokeBorder(Color.border, lineWidth: 2)` -> proper Warp tokens
4. Optionally run: `claude "/ios-warp-design-system"` to show the full token reference

**What to highlight:**
- The agent knows the Warp design system because it's documented in a skill
- It gives exact token names, not vague suggestions
- This catches issues that code review often misses

**If it fails:** Open the warp-design-system skill directly and show the token table. "Even if you don't use the review command, the `/ios-warp-design-system` skill is a reference you can query anytime."

---

#### Demo 3: "Create a PR with proper template" (~8 min)

**Preparation:** Before the workshop, create a branch with a small change (e.g., add a comment or fix a typo in one of the vertical modules). Push it.

**Script:**
1. Show the branch: `git log master..HEAD --oneline`
2. Run: `claude "/ios-pr"`
3. Show how it:
   - Analyzes the git diff automatically
   - Picks the right gitmoji based on change type
   - Fills the PR template (Why/What/Changelog/Accessibility/Tests)
   - Identifies the affected module from file paths
   - Creates a draft PR
4. Show the created PR in GitHub

**What to highlight:**
- Zero manual template filling
- It follows the exact PR template from `PULL_REQUEST_TEMPLATE.md`
- It picks the right gitmoji and module name
- It creates as draft so you can review before marking ready

**If it fails:** Show a pre-created PR from a previous run. Walk through each section explaining what the agent filled in.

---

#### Demo 4: "Understand the system — how does the agent know all this?" (~8 min)

**Script:** (No Claude execution — this is a walkthrough)
1. Open `AGENTS.md` — show its structure: "This is the policy document. It tells the agent about our architecture, module structure, engineering policies."
2. Open `.claude/skills/write-unit-test/SKILL.md` — show: "This is a skill. It's a Markdown file with a name, description, and workflow steps."
3. Open `.claude/rules/unleash-cli.md` — show: "Rules are always loaded. Skills are loaded on demand."
4. Show the connection: "When you say `/ios-write-unit-test`, Claude reads this skill file, follows the workflow, and uses AGENTS.md for project context."
5. Quick diagram on the shared board:
   ```
   You type a command
       -> Claude loads the skill (Markdown)
       -> Skill references project policies (AGENTS.md)
       -> Agent reads your code
       -> Agent produces output following conventions
   ```

**What to highlight:**
- Everything is Markdown — readable, editable, version-controlled
- Skills are not magic — they're checklists that the agent follows
- Anyone can read, modify, or add skills

---

### Block 3: Guided Exercises (40 min)

**Who:** All facilitators float between breakout rooms
**Format:** Individual work, breakout rooms by vertical

**Share this exercise sheet with all participants:**

```
=== GUIDED EXERCISES ===

Everyone should complete Exercise A.
Then pick ONE from Exercise B or C based on your comfort level.

--- EXERCISE A: Your First Skill Run (everyone, ~10 min) ---

1. Open your terminal in the ios-app repo
2. Run:
   claude "Review the file at [pick any .swift file you've worked on recently]"
3. Read the output. Does it mention Warp tokens? SwiftLint rules?
   That's AGENTS.md at work.
4. Now try a skill:
   claude "/ios-warp-design-system"
   Ask: "What Warp spacing token should I use for 16 points?"
5. You should see: Warp.Spacing.spacing200

If this works: congratulations, you're using AI-assisted development.
If it doesn't: raise your hand in the breakout room.


--- EXERCISE B: Generate Tests (intermediate, ~20 min) ---

Pick a ViewModel or UseCase from your vertical that has no tests.

Suggestions if you can't find one:
- Jobs:       Jobs/Sources/JobProfile/Internal/ViewModel/UserDetailsFormViewModel.swift
- Recommerce: Recommerce/Sources/RecommerceTransaction/Internal/Core/ShippingOptIn/View models/PackageSizeOptionsViewModel.swift
- RealEstate: RealEstate/Sources/RealEstateItemPage/Internal/Data/Modell/Object/LoanCalculator/LoanViewModel.swift

1. Run: claude "/ios-write-unit-test [your file path]"
2. Review the generated tests:
   - Does it use Swift Testing (@Test, @Suite)?
   - Does it use Given/When/Then?
   - Does it create protocol-based mocks?
3. Try running the tests:
   swift test --package-path [Jobs|Mobility|RealEstate|Recommerce]
4. Bonus: ask Claude to add edge case tests


--- EXERCISE C: Explore a Skill (advanced, ~20 min) ---

1. Open: .claude/skills/review-code/SKILL.md
2. Read through it — notice the structure:
   - YAML header (name, description)
   - Checklist sections
   - Code examples
   - Workflow steps
3. Think: "What repetitive workflow does my team do that
   could be a skill?"
4. Draft a 10-line skill:
   - Create: .claude/skills/my-experiment/SKILL.md
   - Write the YAML header with name and description
   - Write 3 workflow steps
5. Test it: claude "/ios-my-experiment"
6. Share what you made in the breakout room

Skill template:
---
name: ios-my-experiment
description: Use when [trigger condition]
---
# My Experiment
## Workflow
1. Step 1
2. Step 2
3. Step 3
```

**Facilitator instructions:**
- Prioritize unblocking beginners on Exercise A — their first successful run is the biggest win
- For Exercise B: help people find untested files in their own vertical if the suggestions don't fit
- For Exercise C: point people to `Documentation/AGENTS-CONTRIBUTING.md` for the full contributing guide
- Check in every 5 min: "How's it going? Anyone stuck?"
- Collect interesting results for the wrap-up

---

### Block 4: Show & Tell + Sustain (15 min)

**Who:** Allan (facilitation), all (participation)
**Format:** Main room, shared screen

#### Show & Tell (7 min)
- Ask 2-3 people to share what they did:
  - "What exercise did you try?"
  - "What surprised you?"
  - "Would you use this again?"
- If someone wrote a skill draft (Exercise C), show it on screen

#### Sustain Announcements (8 min)
1. **Slack channel goes live:** `#ios-ai-workflows`
   - Post wins, questions, new skill ideas
   - Weekly "AI win of the week" highlight
2. **Biweekly AI office hours** (30 min, starts next week)
   - Rotating host from different verticals
   - Format: someone demos a workflow or new skill, then open Q&A
3. **Skill request board** (GitHub Issues label or Notion board)
   - Anyone can request: "I wish there was a skill for X"
   - Anyone can pick it up and implement it
4. **AI champions** — each vertical nominates one person to:
   - Be the go-to for AI questions in their team
   - Bring new skill ideas to the biweekly sessions
   - Help onboard teammates who missed the workshop

**Closing ask:** "Try using at least one AI skill in your real work this week. Post what happened in `#ios-ai-workflows` — good or bad."

---

## Cheat Sheet (share before hands-on block)

```
NMP iOS AI Quick Reference
===========================

GETTING STARTED
  claude "your question"            Ask anything about the codebase

DAILY WORKFLOW SKILLS
  /ios-pre-push                     Validate before pushing (lint + tests + snapshots)
  /ios-pr                           Create/update a PR with proper template
  /ios-review-code                  Review code against project standards
  /ios-write-unit-test              Generate unit tests (Swift Testing)
  /ios-write-snapshot-test          Generate snapshot tests

BUILDING
  /ios-create-new-module            Scaffold a new SPM module
  /ios-plan-feature                 Plan feature architecture
  /ios-warp-design-system           Look up Warp tokens and components
  /ios-localization-flow            Localization workflow (strings -> SwiftGen -> L10n)

CI & RELEASE
  /ios-ci-workflow-triage           Debug CI failures
  /ios-run-snapshot-tests <scheme>  Run snapshot test schemes
  /ios-distribute                   Distribute to Firebase App Distribution

CHECKS
  /ios-concurrency-settings-check   Verify Swift concurrency settings
  /ios-ios26-compatibility-check    Validate iOS 26 / Liquid Glass patterns
  /ios-drive-shared-ui-routing      Where should this UI component live?

UNDERSTANDING THE SYSTEM
  AGENTS.md                         Project policies the agent follows
  .claude/skills/                   All skill definitions (Markdown files)
  .claude/rules/                    Always-loaded context rules
  .claude/docs/                     Supporting docs for skills
  Documentation/AGENTS-CONTRIBUTING.md  How to add/modify skills

TIPS
  - Be specific: "Write tests for JobListViewModel" > "Write tests"
  - Use file paths: "Review Mobility/Sources/MobilityAdIn/ViewModel.swift"
  - Chain: review -> fix -> test -> pre-push -> pr
  - The agent knows Warp, module structure, and project conventions
```

---

## Post-Workshop Follow-Up

### Week 1
- [ ] Share recording + cheat sheet in `#ios-ai-workflows`
- [ ] Post "Week 1 challenge": try one skill you haven't used before, post the result
- [ ] Facilitators actively answer questions in the channel

### Week 2
- [ ] First biweekly AI office hours session
- [ ] Highlight early wins in Slack
- [ ] Review any skill requests that came in

### Month 1
- [ ] Survey: "Have you used AI skills in your workflow? What's working / not working?"
- [ ] Review and merge any contributed skills
- [ ] Iterate on existing skills based on feedback
- [ ] Publish a "Top 5 AI Wins" post to the broader team

### Ongoing
- [ ] Biweekly office hours continue (rotate hosts across verticals)
- [ ] Slack channel stays active with wins + requests
- [ ] Quarterly "skill sprint" — dedicated time for teams to build skills for their vertical

---

## Measuring Success

| Metric | How to measure | Target |
|--------|---------------|--------|
| Setup completion | Pre-workshop verification | 100% of attendees |
| First use | "I ran a skill" in Slack | 80% within first week |
| Repeat use | Survey at 1 month | 60% using skills weekly |
| Contributions | PRs adding/modifying skills | 3+ new skills within 2 months |
| Organic spread | People outside workshop using it | Measurable by month 2 |

---

## Risk Mitigation

| Risk | Mitigation |
|------|-----------|
| Demo breaks live | Every demo has a pre-recorded backup. Facilitator switches to recording and narrates. |
| File paths changed since rehearsal | Verify all paths on latest `master` the day before. |
| Beginners stuck on setup | Setup deadline is 3 days before. "Setup clinic" available day before. |
| Beginners stuck during exercises | Facilitators prioritize beginners. Exercise A is trivially simple. |
| Power users bored | Exercise C (write a skill) is genuinely challenging and creative. |
| Momentum dies after workshop | Slack channel + biweekly cadence + AI champions launched AT the workshop. |
| Claude is slow/unresponsive | Have pre-recorded outputs for all demos. Exercises still work even if slow. |

---

## Facilitator Roles

| Person | Primary responsibility | Demos | Breakout rooms |
|--------|----------------------|-------|----------------|
| Allan | Welcome, Sustain/close, Show & Tell MC | Demo backup | Floater |
| Matvii | Demo 1 (tests), Demo 2 (Warp), Demo 4 (system walkthrough) | Primary | Advanced room |
| breiby | Exercise facilitation | Demo 3 (PR creation) | Beginner room |
| Vilde | Logistics, timing, board, Slack channel setup | - | Intermediate room |
| dAI | Workshop structure, content review | - | - |

---

## Facilitator Rehearsal Checklist

Complete at least 3 days before the workshop:

- [ ] **Demo 1 (Tests):** Run `/ios-write-unit-test` on `UserDetailsFormViewModel.swift`. Verify it produces Swift Testing output. Run the tests. Record output as backup.
- [ ] **Demo 2 (Warp):** Run code review on `FraudInfoBoxView.swift`. Verify it catches hardcoded `.padding(16)` and `cornerRadius: 8`. Record output.
- [ ] **Demo 3 (PR):** Create a test branch with a small change. Run `/ios-pr`. Verify it creates a draft PR. Record output. Delete the test PR after.
- [ ] **Demo 4 (System):** Walk through AGENTS.md -> skill -> rule flow. No Claude execution needed — just practice the narration.
- [ ] **Exercise A:** Run through it yourself. Verify the Warp spacing question returns `Warp.Spacing.spacing200`.
- [ ] **Exercise B:** Try generating tests for each suggested file. Verify at least 2 of 3 produce valid tests.
- [ ] **Timing:** Each demo fits in 8 min. Full agenda fits in 2 hours.
