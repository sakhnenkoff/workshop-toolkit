# Workshop 1: AI in Our Repo — Introduction

**Date:** Week of March 9-13, 2026 (exact day TBD)
**Duration:** ~60 minutes (second hour of the combined session)
**Format:** Remote, shared screen + Slido polls
**Audience:** 15-25 iOS developers, mixed experience levels
**Facilitators:** TBD (assign at planning meeting)

---

## Purpose

This is the **first** of two workshops. Its job is to create curiosity and get people on board — not to teach everything.

| This workshop | The March 25 workshop |
|---------------|----------------------|
| Watch and learn | Hands-on exercises |
| "Here's what's possible" | "Now you do it" |
| No setup required to participate | Everyone must have Claude Code installed |
| Create curiosity | Build competence |

---

## Pre-Workshop Actions

### Monday (start of workshop week)

**Slack message to send** (copy-paste ready):

```
Hey team! This week's workshop includes a section on AI-assisted development
in our iOS repo.

No setup is required to participate this week — you can just watch the demos.

But if you want to follow along (and be ready for the hands-on workshop on
March 25), please set up Claude Code before the session:

1. Install Claude Code: [link to internal setup guide]
2. Verify: run `claude --version` in your terminal
3. Pull latest master in the ios-app repo

Questions? Drop them in #ios-ai-workshop

See you at the workshop!
```

### Before the workshop

#### Slido Setup
- [ ] Go to [slido.com](https://www.slido.com) and create an event
- [ ] Add the 3 polls (see poll text below):
  - Poll 1: Multiple choice (multi-select) — "How do you currently use AI in your development?"
  - Poll 2: Word cloud — "What repetitive task would you most want to speed up?"
  - Poll 3: Rating (1-5 scale) — "How likely are you to try Claude Code this week?"
- [ ] Enable Q&A with upvoting (for the Q&A block — best questions float to top)
- [ ] Note the join code / link — share in meeting chat when the workshop starts
- [ ] Test it: participants go to slido.com and enter the code, no signup needed

#### Other Prep
- [ ] Each facilitator rehearses their demo section at least once
- [ ] Verify all demo file paths exist on current master
- [ ] Prepare backup screen recordings for each demo (in case Claude is slow or misbehaves)
- [ ] Create the `#ios-ai-workflows` Slack channel (keep private until workshop close)

---

## Agenda (60 minutes)

```
 0:00  Block 1 — Opening + Pulse Check         8 min
 0:08  Block 2 — The Three Levels              12 min
 0:20  Block 3 — Demo A: Context               12 min
 0:32  Block 3 — Demo B: Skills in Action      13 min
 0:45  Block 4 — Polls + Q&A                   10 min
 0:55  Block 5 — Close + Next Steps             5 min
 1:00  End
```

---

## Block 1: Opening + Pulse Check (8 min)

**Who:** TBD
**Format:** Shared screen, Slido

### Script

1. Brief framing (2 min):
   - "This hour is about showing you what's possible — not teaching everything"
   - "Whether you've never used AI tools or you use them daily, you'll see something new"
   - "Our repo has a growing AI infrastructure — AGENTS.md, 17 skills, rules, MCP servers — and we want everyone to benefit from it"

2. Slido Poll #1 (3 min):

   ```
   POLL #1 — "How do you currently use AI in your development?"
   Type: Multiple choice (multi-select)
   Options:
   - I don't really use AI tools
   - ChatGPT / web-based AI for general questions
   - Copilot / inline code suggestions
   - Claude Code in the terminal
   - Claude Code with skills (/ios-write-unit-test, /ios-pr, etc.)
   ```

3. Show results live (3 min):
   - Acknowledge the spread: "This is exactly why we're doing this — there's a big range and that's fine"
   - If mostly low usage: "Great, we'll show you what's been built and how easy it is to start"
   - If some power users: "For those already using it — stick around for how the system works under the hood, and we'll need your help later"

---

## Block 2: The Three Levels (12 min)

**Who:** TBD
**Format:** Presentation (slides or shared screen with notes)

### Script

Walk through the three levels of AI-assisted development. Use the repo as the example throughout.

**Level 1: Use Claude for coding**
- "This is where most people start — you ask Claude a question, it gives you an answer"
- "You can ask it to explain code, generate a function, debug an error"
- "This works, but it's generic. Claude doesn't know our project conventions, our module structure, or our design system"

**Level 2: Give Claude context** (this is the key level)
- "This is where the magic happens — and it takes almost zero effort to understand"
- "When you run Claude Code inside our repo, it automatically reads `CLAUDE.md` and `AGENTS.md`"
- "These files tell Claude about our architecture, our engineering policies, our module structure, our testing conventions"
- "Suddenly Claude knows to use Swift Testing instead of XCTest, knows what Warp tokens are, knows our PR template"
- "There are three layers of context:"
  - **Global** (`~/.claude/CLAUDE.md`) — your personal preferences across all projects
  - **Repo** (`CLAUDE.md`, `AGENTS.md`, `.claude/rules/`) — shared team knowledge, checked into git
  - **Local** (`.claude/settings.local.json`) — your machine-specific settings, not committed
- "The repo-level context is what makes this powerful. It's version-controlled, everyone gets it, and it evolves with the project."

**Level 3: Teach Claude workflows**
- "This is the next level — instead of just giving Claude knowledge, you give it repeatable workflows"
- "**Skills** are Markdown files that define step-by-step processes. We have 17 of them."
  - Quick list: write tests, review code, create PRs, check Warp compliance, run snapshots, scaffold modules...
- "**MCP servers** connect Claude to external tools — Jira, Confluence, Amplitude, Xcode builds"
- "You don't need to be at this level today — but knowing it exists matters"

**Key takeaway to land:**
- "The jump from Level 1 to Level 2 is the biggest. And you get it for free just by running Claude inside our repo."

---

## Block 3: Demos (25 min)

### Demo A: "Context Changes Everything" (~12 min)

**Who:** TBD
**Format:** Live terminal, shared screen

**Purpose:** Show the tangible difference between using Claude with and without project context.

**Demo file:** `Jobs/Sources/JobEasyApply/Internal/Views/AiApplicationLetter/AiApplicationLetterViewModel.swift`
(A 244-line ViewModel that handles AI-generated job application letters — topical and has interesting business logic)

#### Script

**Step 1 — Without context (3 min):**

1. Open a terminal in a **temp directory** (not in the repo):
   ```bash
   cd /tmp
   claude
   ```
2. Paste the file content and ask:
   ```
   Review this Swift ViewModel for code quality issues and suggest improvements
   ```
3. Show the response — it'll be generic:
   - Generic Swift style suggestions
   - No mention of project conventions
   - No awareness of Warp, module structure, or testing patterns
4. Narrate: "This is Level 1. It's helpful, but it doesn't know us."

**Step 2 — With context (4 min):**

1. Open Claude Code **inside the repo**:
   ```bash
   cd ~/path/to/ios-app
   claude
   ```
2. Ask the same question, pointing to the file:
   ```
   Review AiApplicationLetterViewModel.swift in JobEasyApply for code quality issues
   ```
3. Show the response — it should reference:
   - Project-specific patterns (AGENTS.md policies)
   - Warp design system awareness (if applicable)
   - SwiftLint policies (no `print()`, use `Logger`)
   - Module architecture awareness (vertical module, not app-modules)
4. Narrate: "Same question, completely different answer. The only difference is where we're running Claude."

**Step 3 — Open the hood (5 min):**

1. Show `CLAUDE.md` briefly: "This is the entry point. It points to AGENTS.md"
2. Show `AGENTS.md` — scroll through key sections:
   - Project overview
   - Architecture / module structure
   - Engineering policies (SwiftLint, localization, design system)
   - Available skills list
3. Show `.claude/rules/` folder: "These are always loaded — like the Unleash CLI reference"
4. Show `.claude/skills/` folder: "These are loaded on demand when you invoke them"
5. Quick mental model:
   ```
   CLAUDE.md          --> Entry point
   AGENTS.md          --> Policies & architecture
   .claude/rules/     --> Always-on context
   .claude/skills/    --> On-demand workflows
   ```

**If it fails:** Switch to backup recording. Key message still lands: "The difference is context."

---

### Demo B: "Skills in Action" (~13 min)

**Who:** TBD
**Format:** Live terminal, shared screen

**Purpose:** Show a skill running on a real file, then demystify what a skill is.

**Demo file:** `Jobs/Sources/JobProfile/Internal/ViewModel/UserDetailsFormViewModel.swift`
(89-line ViewModel that validates user form fields with Combine. Has zero tests.)

#### Script

**Step 1 — Show the file (2 min):**

1. Open the file, briefly walk through it:
   - "This is a real ViewModel from Jobs — it validates name, email, and phone number"
   - "It uses Combine publishers for reactive validation"
   - "It has zero tests. Let's fix that."

**Step 2 — Run the skill (5 min):**

1. Run:
   ```
   claude "/ios-write-unit-test Jobs/Sources/JobProfile/Internal/ViewModel/UserDetailsFormViewModel.swift"
   ```
2. While it runs, narrate what's happening:
   - "It's reading the skill definition — which tells it to use Swift Testing, not XCTest"
   - "It's reading AGENTS.md for project conventions"
   - "It's analyzing the file to understand the validation logic"
   - "It's generating tests with Given/When/Then structure"
3. Show the generated test file
4. Point out:
   - Uses `@Test` and `@Suite` (Swift Testing, not XCTest)
   - Creates proper test structure
   - Tests both valid and invalid inputs
   - Tests edge cases (empty strings, nil values)

**Step 3 — Demystify the skill (4 min):**

1. Open the skill file:
   ```
   .claude/skills/write-unit-test/SKILL.md
   ```
2. Show: "This is the entire skill. It's a Markdown file."
3. Walk through the structure:
   - YAML header: name and description (this creates the `/ios-write-unit-test` command)
   - Workflow steps: what the agent should do, in order
   - Conventions: use Swift Testing, Given/When/Then, protocol mocks
4. Key message: "Skills are not magic. They're checklists that Claude follows. Anyone can read them, modify them, or create new ones."

**Step 4 — Flash the full skill list (2 min):**

1. Show the cheat sheet briefly (can share link in chat):
   - Daily workflow: `/ios-pre-push`, `/ios-pr`, `/ios-review-code`, `/ios-write-unit-test`
   - Building: `/ios-create-new-module`, `/ios-plan-feature`, `/ios-warp-design-system`
   - CI: `/ios-ci-workflow-triage`, `/ios-run-snapshot-tests`
2. Mention MCP servers: "We also have connections to Jira, Confluence, Amplitude, and Xcode — but that's for another session"

**If it fails:** Show backup recording. Open the skill file anyway — the "it's just Markdown" message doesn't need Claude to be running.

---

## Block 4: Polls + Q&A (10 min)

**Who:** TBD
**Format:** Slido + chat questions

### Slido Poll #2 (4 min)

```
POLL #2 — "What repetitive task in your workflow would you most want to speed up?"
Type: Word cloud (open text input)
```

Show results live. Connect them to existing skills:
- If "testing" appears: "We have `/ios-write-unit-test` and `/ios-write-snapshot-test`"
- If "PR" / "code review" appears: "We have `/ios-pr` and `/ios-review-code`"
- If something has no skill: "This is exactly the kind of thing we can build a skill for — and you can help"

### Slido Poll #3 (2 min)

```
POLL #3 — "After seeing this, how likely are you to try Claude Code this week?"
Type: Scale 1-5
1 = Not likely
5 = Definitely trying it
```

Show results. Don't comment negatively on low scores — just acknowledge: "Whatever your number, the setup instructions are coming."

### Slido Q&A (4 min)

- Switch to Slido Q&A view — participants submit questions and upvote each other's
- Take the top 2-3 questions by upvotes
- If no questions come in: have 1-2 prepared prompts:
  - "A question we often get: does Claude send our code to external servers?" (address privacy/security concern)
  - "Another one: can I break anything by using Claude Code?" (no — it asks permission before running commands)

---

## Block 5: Close + Next Steps (5 min)

**Who:** TBD
**Format:** Shared screen

### Script

1. **Recap the three levels:**
   - Level 1: Use Claude for coding (good start)
   - Level 2: Give Claude context (where the real value is — and you get it automatically in our repo)
   - Level 3: Skills and workflows (the infrastructure is built, come use it)

2. **Share links in chat:**
   - Setup guide: [link to internal docs]
   - Cheat sheet: `Documentation/CLAUDE-CODE-CHEAT-SHEET.md` in the repo
   - Workshop recording: will be shared after

3. **Announce the Slack channel:**
   - Open `#ios-ai-workflows` (make it public now)
   - "Post your wins, questions, and ideas here"

4. **Tease March 25:**
   - "Next workshop is hands-on — you'll run skills yourself, generate tests, create PRs"
   - "To participate, you need Claude Code installed. Please set it up before then."
   - "Setup instructions are in the Slack channel"

5. **Closing ask:**
   - "If you're already set up: try one thing this week. Review a file, ask Claude a question inside the repo. Post what happened in `#ios-ai-workflows`."
   - "If you're not set up: get set up. That's your one thing."

---

## Workshop Branch (Sandbox)

To ensure demo reproducibility, facilitators should work from a frozen branch:

### Setup (do this before rehearsals)

```bash
git checkout master
git pull
git checkout -b workshop/ai-intro-march-2026
git push -u origin workshop/ai-intro-march-2026
```

### What the branch gives you

- File paths won't change if someone merges to master
- Facilitators can rehearse demos with predictable results
- Generated test files from demo runs won't pollute master
- Every facilitator gets the exact same starting point

### Verification checklist (on the branch)

- [ ] `Jobs/Sources/JobEasyApply/Internal/Views/AiApplicationLetter/AiApplicationLetterViewModel.swift` exists (Demo A)
- [ ] `Jobs/Sources/JobProfile/Internal/ViewModel/UserDetailsFormViewModel.swift` exists (Demo B)
- [ ] No tests exist for `UserDetailsFormViewModel` (Demo B)
- [ ] `.claude/skills/write-unit-test/SKILL.md` exists (Demo B demystification)
- [ ] `CLAUDE.md` and `AGENTS.md` exist at repo root
- [ ] `.claude/rules/` and `.claude/skills/` directories are populated
- [ ] `Documentation/CLAUDE-CODE-CHEAT-SHEET.md` exists

---

## Backup Recordings

Record these before the workshop (asciinema or screen recording):

- [ ] **Demo A backup:** Claude reviewing `AiApplicationLetterViewModel.swift` with and without repo context
- [ ] **Demo B backup:** `/ios-write-unit-test` generating tests for `UserDetailsFormViewModel.swift`
- [ ] **Demo B skill file:** Screen recording of scrolling through `write-unit-test/SKILL.md`

---

## Facilitator Assignments

Fill in at planning meeting:

| Block | Facilitator | Backup |
|-------|-------------|--------|
| Block 1: Opening + Pulse Check | TBD | TBD |
| Block 2: The Three Levels | TBD | TBD |
| Block 3: Demo A (Context) | TBD | TBD |
| Block 3: Demo B (Skills) | TBD | TBD |
| Block 4: Polls + Q&A | TBD | TBD |
| Block 5: Close + Next Steps | TBD | TBD |

---

## Risk Mitigation

| Risk | Mitigation |
|------|-----------|
| Claude is slow or unresponsive | Every demo has a pre-recorded backup. Switch immediately, narrate what should happen. |
| File paths changed since rehearsal | Use the workshop branch. Verify paths day before. |
| Demo produces bad output | Pre-recorded backup. The "it's just Markdown" message doesn't need Claude running. |
| Slido doesn't work | Fall back to "type in meeting chat" for all polls. |
| No questions during Q&A | Have 2 prepared questions (privacy, safety). |
| Too many questions, runs over time | Cap at 3 questions. Say "Great questions - let's continue in #ios-ai-workflows." |
| People zone out | Polls at minute 3 and minute 45 re-engage attention. Demos are visual and narrated. |

---

## Success Criteria

After this workshop, we want:

| Outcome | How to tell |
|---------|------------|
| People understand the 3 levels | Slido poll #3 shows interest (avg 3+) |
| People know skills exist | They reference specific skill names |
| Setup starts happening | Messages in #ios-ai-workflows asking for help |
| March 25 is anticipated | People ask about it or mark their calendars |
| No one felt lost or overwhelmed | No complaints about pace or complexity |

---

## Related

- [March 25 hands-on workshop plan](./2026-03-25-ai-first-development-workshop.md)
- [Claude Code Cheat Sheet](../ios-app/Documentation/CLAUDE-CODE-CHEAT-SHEET.md) (in the repo)
