# Workshop Toolkit

Three Claude Code skills for designing, presenting, and facilitating workshops. One markdown file is the source of truth — skills generate everything else.

## How it works

```
Your idea
    │
    ▼
/workshop-plan          ← guided conversation to design the workshop
    │
    ▼
workshop.md             ← single source of truth
    │
    ├──▶ /workshop-slides       → slides.html      (what participants see)
    │
    └──▶ /workshop-cheatsheet   → cheatsheet.html   (what the facilitator sees)
```

## Skills

### `/workshop-plan`

Conversational skill that helps you design a workshop from scratch. Asks questions one at a time, then produces a structured `workshop.md` with:

- Block structure with timing and energy arc
- Poll questions with exact text and response strategies
- Demo scripts with step-by-step narration and fallback plans
- Speaker notes and transition phrases
- Pre/post workshop communications
- Risk mitigation table

### `/workshop-slides`

Generates a participant-facing HTML slide deck from `workshop.md`.

- Single self-contained HTML file (zero dependencies)
- Style preview — pick from curated themes before generating
- Workshop-specific slide types: polls, demos, agenda timeline, key insights
- Keyboard navigation (arrows, space, Home/End)
- Viewport-locked slides with responsive typography
- `prefers-reduced-motion` support

### `/workshop-cheatsheet`

Generates a facilitator cheatsheet from `workshop.md`. Designed for glancing at during a live session.

- One block per screen — no scrolling
- Speaker notes in large, scannable text
- Poll cards with exact questions and how to read results
- Demo steps with fallback plans
- Progress bar and block timer
- Keyboard shortcuts: `←`/`→` navigate, `T` timer, `N` next preview

## Setup

Skills are installed via symlinks to `~/.claude/skills/`:

```bash
ln -s ~/Developer/workshop-toolkit/skills/workshop-plan ~/.claude/skills/workshop-plan
ln -s ~/Developer/workshop-toolkit/skills/workshop-slides ~/.claude/skills/workshop-slides
ln -s ~/Developer/workshop-toolkit/skills/workshop-cheatsheet ~/.claude/skills/workshop-cheatsheet
```

After linking, the skills are available globally in any Claude Code session.

## Repository structure

```
workshop-toolkit/
├── skills/
│   ├── workshop-plan/SKILL.md
│   ├── workshop-slides/
│   │   ├── SKILL.md
│   │   ├── viewport-base.css
│   │   └── style-presets.md
│   └── workshop-cheatsheet/
│       ├── SKILL.md
│       └── cheatsheet-template.md
├── workshops/                       # actual workshop content
│   ├── 2026-03-W11-ai-intro/
│   └── 2026-03-25-ai-hands-on/
└── frontend-slides-ref/             # upstream reference patterns
```

## Workflow

1. **Plan:** `cd workshops && claude` → `/workshop-plan`
2. **Generate slides:** `/workshop-slides workshops/my-workshop/workshop.md`
3. **Generate cheatsheet:** `/workshop-cheatsheet workshops/my-workshop/workshop.md`
4. **Present:** Open `slides.html` for participants, `cheatsheet.html` on your second screen

## Credits

Slide generation patterns adapted from [frontend-slides](https://github.com/zarazhangrui/frontend-slides) by zarazhangrui.
