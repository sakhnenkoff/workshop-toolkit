# Cheatsheet HTML Template

This document defines the HTML/CSS/JS patterns for the facilitator cheatsheet. The `workshop-cheatsheet` skill reads this when generating output.

## HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>[Workshop Title] — Facilitator Cheatsheet</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
  <!-- All CSS inline -->
</head>
<body>
  <!-- Progress bar at top -->
  <div class="progress-bar">
    <div class="progress-fill" id="progress"></div>
    <div class="progress-segments">
      <!-- One segment per block, width proportional to duration -->
    </div>
  </div>

  <!-- Block slides -->
  <div class="blocks-container" id="blocks">
    <div class="block active" data-duration="[minutes]" data-start="[HH:MM]">
      <div class="block-header">
        <div class="block-meta">
          <span class="block-number">1 / N</span>
          <span class="block-time">[start_time]</span>
          <span class="block-duration">[N] min</span>
        </div>
        <h1 class="block-title">[Block Name]</h1>
        <div class="block-info">
          <span class="facilitator">[Who]</span>
          <span class="format-badge">[Format]</span>
        </div>
      </div>

      <div class="block-body">
        <!-- Speaker notes as large readable items -->
        <div class="notes">
          <div class="note-item">[Speaker note / script step]</div>
        </div>

        <!-- Poll specification (if this block has one) -->
        <div class="poll-card">
          <div class="poll-label">POLL</div>
          <div class="poll-question">[Exact question text]</div>
          <div class="poll-options">[Options or format]</div>
          <div class="poll-reading">[How to read results]</div>
        </div>

        <!-- Demo steps (if this block has a demo) -->
        <div class="demo-card">
          <div class="demo-label">DEMO</div>
          <div class="demo-steps">
            <div class="demo-step"><span class="step-num">1</span> [Step text]</div>
          </div>
          <div class="demo-fallback">[Fallback plan]</div>
        </div>
      </div>

      <div class="block-footer">
        <div class="transition">
          <span class="transition-label">NEXT →</span>
          <span class="transition-text">[Transition phrase]</span>
        </div>
      </div>
    </div>
  </div>

  <!-- Timer overlay -->
  <div class="timer" id="timer">
    <span class="timer-value" id="timer-value">00:00</span>
    <span class="timer-label">elapsed</span>
  </div>

  <!-- Next block preview overlay -->
  <div class="next-preview" id="next-preview">
    <div class="preview-content">
      <h2>Up Next</h2>
      <h3>[Next block name]</h3>
      <p>[Next block first note]</p>
    </div>
  </div>

  <!-- Keyboard hint -->
  <div class="keyboard-hint">
    ← → navigate &nbsp; T timer &nbsp; N next preview
  </div>

  <!-- All JS inline -->
</body>
</html>
```

## CSS Design System

```css
:root {
  --bg: #ffffff;
  --bg-subtle: #f8f9fa;
  --bg-card: #f1f3f5;
  --text: #1a1a2e;
  --text-secondary: #495057;
  --text-dim: #868e96;
  --accent: #228be6;
  --accent-light: #e7f5ff;
  --poll-color: #7048e8;
  --poll-bg: #f3f0ff;
  --demo-color: #e8590c;
  --demo-bg: #fff4e6;
  --transition-color: #2b8a3e;
  --transition-bg: #ebfbee;
  --danger: #e03131;
  --font-sans: 'Inter', system-ui, sans-serif;
  --font-mono: 'JetBrains Mono', monospace;
}

/* Body fills viewport, no scroll */
html, body { height: 100%; overflow: hidden; margin: 0; }
body { font-family: var(--font-sans); background: var(--bg); color: var(--text); }

/* Progress bar - fixed at top */
.progress-bar {
  position: fixed; top: 0; left: 0; right: 0; height: 4px;
  background: var(--bg-card); z-index: 100;
}
.progress-fill {
  height: 100%; background: var(--accent);
  transition: width 0.3s ease;
}
.progress-segments {
  position: absolute; top: 0; left: 0; right: 0; height: 100%;
  display: flex;
}
.progress-segment {
  height: 100%; border-right: 2px solid var(--bg);
  opacity: 0.3;
}
.progress-segment.done { opacity: 1; background: var(--accent); }
.progress-segment.current { opacity: 0.6; background: var(--accent); }

/* Block fills the screen */
.blocks-container { height: 100vh; position: relative; }
.block {
  position: absolute; inset: 0;
  display: none; flex-direction: column;
  padding: 32px 64px 24px;
}
.block.active { display: flex; }

/* Header */
.block-header { margin-bottom: 24px; flex-shrink: 0; }
.block-meta {
  display: flex; align-items: center; gap: 16px;
  font-family: var(--font-mono); font-size: 13px; color: var(--text-dim);
  margin-bottom: 8px;
}
.block-title {
  font-size: 36px; font-weight: 700; margin: 0 0 8px;
  letter-spacing: -0.5px;
}
.block-info { display: flex; gap: 12px; }
.facilitator {
  font-size: 14px; color: var(--text-secondary);
  font-weight: 500;
}
.format-badge {
  font-family: var(--font-mono); font-size: 11px;
  text-transform: uppercase; letter-spacing: 1px;
  padding: 3px 10px; border-radius: 4px;
  background: var(--bg-card); color: var(--text-dim);
}

/* Body - takes remaining space */
.block-body { flex: 1; overflow-y: auto; display: flex; flex-direction: column; gap: 20px; }

/* Speaker notes */
.notes { display: flex; flex-direction: column; gap: 12px; }
.note-item {
  font-size: 20px; line-height: 1.5; color: var(--text);
  padding-left: 20px; border-left: 3px solid var(--bg-card);
}
.note-item strong { font-weight: 600; }
.note-item code {
  font-family: var(--font-mono); font-size: 14px;
  background: var(--bg-subtle); padding: 2px 8px;
  border-radius: 3px;
}

/* Poll card */
.poll-card {
  padding: 20px 24px; border-radius: 10px;
  background: var(--poll-bg); border: 1px solid rgba(112, 72, 232, 0.15);
}
.poll-label {
  font-family: var(--font-mono); font-size: 11px; font-weight: 600;
  letter-spacing: 2px; color: var(--poll-color); margin-bottom: 8px;
}
.poll-question { font-size: 18px; font-weight: 600; margin-bottom: 8px; }
.poll-options { font-size: 15px; color: var(--text-secondary); margin-bottom: 8px; }
.poll-reading { font-size: 14px; color: var(--text-dim); font-style: italic; }

/* Demo card */
.demo-card {
  padding: 20px 24px; border-radius: 10px;
  background: var(--demo-bg); border: 1px solid rgba(232, 89, 12, 0.15);
}
.demo-label {
  font-family: var(--font-mono); font-size: 11px; font-weight: 600;
  letter-spacing: 2px; color: var(--demo-color); margin-bottom: 8px;
}
.demo-steps { display: flex; flex-direction: column; gap: 8px; }
.demo-step { font-size: 15px; display: flex; align-items: baseline; gap: 10px; }
.step-num {
  font-family: var(--font-mono); font-size: 12px; font-weight: 600;
  width: 24px; height: 24px; border-radius: 50%;
  display: inline-flex; align-items: center; justify-content: center;
  background: rgba(232, 89, 12, 0.12); color: var(--demo-color); flex-shrink: 0;
}
.demo-fallback {
  margin-top: 12px; padding-top: 12px; border-top: 1px solid rgba(232, 89, 12, 0.15);
  font-size: 13px; color: var(--danger); font-style: italic;
}

/* Footer with transition */
.block-footer {
  flex-shrink: 0; margin-top: 16px; padding-top: 16px;
  border-top: 1px solid var(--bg-card);
}
.transition {
  padding: 12px 16px; border-radius: 8px;
  background: var(--transition-bg); border: 1px solid rgba(43, 138, 62, 0.15);
  display: flex; align-items: center; gap: 12px;
}
.transition-label {
  font-family: var(--font-mono); font-size: 11px; font-weight: 600;
  letter-spacing: 1px; color: var(--transition-color);
}
.transition-text { font-size: 15px; color: var(--text-secondary); }

/* Timer */
.timer {
  position: fixed; bottom: 24px; right: 24px;
  display: flex; flex-direction: column; align-items: center;
  background: var(--bg); border: 1px solid var(--bg-card);
  border-radius: 12px; padding: 12px 20px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.08);
  opacity: 0; transition: opacity 0.2s;
}
.timer.visible { opacity: 1; }
.timer-value {
  font-family: var(--font-mono); font-size: 32px; font-weight: 600;
  color: var(--text);
}
.timer-label {
  font-family: var(--font-mono); font-size: 10px;
  color: var(--text-dim); text-transform: uppercase; letter-spacing: 1px;
}

/* Next preview overlay */
.next-preview {
  position: fixed; inset: 0; background: rgba(0,0,0,0.5);
  display: none; align-items: center; justify-content: center; z-index: 200;
}
.next-preview.visible { display: flex; }
.preview-content {
  background: var(--bg); border-radius: 16px; padding: 40px 48px;
  max-width: 600px; box-shadow: 0 8px 32px rgba(0,0,0,0.15);
}

/* Keyboard hint */
.keyboard-hint {
  position: fixed; bottom: 24px; left: 50%; transform: translateX(-50%);
  font-family: var(--font-mono); font-size: 11px; color: var(--text-dim);
  background: var(--bg-subtle); padding: 6px 16px; border-radius: 6px;
  border: 1px solid var(--bg-card);
}
```

## JavaScript

```javascript
class CheatsheetApp {
  constructor() {
    this.blocks = document.querySelectorAll('.block');
    this.current = 0;
    this.timerRunning = false;
    this.timerSeconds = 0;
    this.timerInterval = null;
    this.totalBlocks = this.blocks.length;

    this.initKeyboard();
    this.updateProgress();
  }

  initKeyboard() {
    document.addEventListener('keydown', (e) => {
      switch(e.key) {
        case 'ArrowRight': this.next(); break;
        case 'ArrowLeft': this.prev(); break;
        case 't': case 'T': this.toggleTimer(); break;
        case 'n': case 'N': this.toggleNextPreview(); break;
        case 'Escape': this.closeNextPreview(); break;
        case 'Home': this.goTo(0); break;
        case 'End': this.goTo(this.totalBlocks - 1); break;
      }
    });
  }

  next() {
    if (this.current < this.totalBlocks - 1) {
      this.goTo(this.current + 1);
    }
  }

  prev() {
    if (this.current > 0) {
      this.goTo(this.current - 1);
    }
  }

  goTo(index) {
    this.blocks[this.current].classList.remove('active');
    this.current = index;
    this.blocks[this.current].classList.add('active');
    this.resetTimer();
    this.updateProgress();
  }

  updateProgress() {
    // Calculate progress based on completed blocks
    const fill = ((this.current) / this.totalBlocks) * 100;
    document.getElementById('progress').style.width = fill + '%';

    // Update segment states
    document.querySelectorAll('.progress-segment').forEach((seg, i) => {
      seg.classList.toggle('done', i < this.current);
      seg.classList.toggle('current', i === this.current);
    });
  }

  toggleTimer() {
    const timer = document.getElementById('timer');
    if (this.timerRunning) {
      clearInterval(this.timerInterval);
      this.timerRunning = false;
    } else {
      timer.classList.add('visible');
      this.timerRunning = true;
      this.timerInterval = setInterval(() => {
        this.timerSeconds++;
        const m = Math.floor(this.timerSeconds / 60);
        const s = this.timerSeconds % 60;
        document.getElementById('timer-value').textContent =
          String(m).padStart(2, '0') + ':' + String(s).padStart(2, '0');
      }, 1000);
    }
  }

  resetTimer() {
    this.timerSeconds = 0;
    document.getElementById('timer-value').textContent = '00:00';
  }

  toggleNextPreview() {
    const preview = document.getElementById('next-preview');
    preview.classList.toggle('visible');
  }

  closeNextPreview() {
    document.getElementById('next-preview').classList.remove('visible');
  }
}

document.addEventListener('DOMContentLoaded', () => new CheatsheetApp());
```

## Content Mapping Rules

When parsing `workshop.md` blocks into cheatsheet blocks:

| workshop.md element | Cheatsheet element |
|---------------------|-------------------|
| `## Block N: Name (duration)` | Block title + duration in header |
| `**Who:** [name]` | Facilitator badge |
| `**Format:** [type]` | Format badge |
| Numbered script steps | Note items (large text) |
| Quoted text (`"..."`) in steps | Bold/highlighted in note items |
| Code blocks starting with `POLL` | Poll card |
| Steps under `#### Script` | Note items |
| Steps under demo headings | Demo card with numbered steps |
| Lines with "If it fails" / "backup" / "fallback" | Demo fallback section |
| `> **Transition:**` lines | Transition footer |
| Agenda section timestamps | Block start times |
