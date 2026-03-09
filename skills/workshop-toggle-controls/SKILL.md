---
name: workshop-toggle-controls
description: Toggle ALL keyboard controls on or off in workshop HTML files. Disables every key the page intercepts (arrows, Home/End, Space, F) so the browser/OS handles them normally. Use when preparing to present or restoring controls after.
---

# Toggle Slide Deck Controls

## When to use

- Before presenting: disable all keyboard intercepts so keys behave normally in the browser
- After presenting: re-enable controls for development/testing

## Procedure

1. Find all HTML files in the current working directory (non-recursive — just `*.html` in the cwd)
2. For each HTML file, locate the `addEventListener('keydown'` block
3. Toggle the entire event listener body:

### Enabled state

The keydown listener has active switch cases:
```js
document.addEventListener('keydown', (e) => {
  switch(e.key) {
    case 'ArrowRight': case ' ': case 'ArrowDown':
      e.preventDefault(); this.next(); break;
    case 'ArrowLeft': case 'ArrowUp':
      e.preventDefault(); this.prev(); break;
    case 'Home': e.preventDefault(); this.goTo(0); break;
    case 'End': e.preventDefault(); this.goTo(this.total - 1); break;
    case 'f': case 'F':
      if (!document.fullscreenElement) document.documentElement.requestFullscreen();
      else document.exitFullscreen();
      break;
  }
});
```

### Disabled state

Every line inside the listener callback is commented out:
```js
document.addEventListener('keydown', (e) => {
  // switch(e.key) {
  //   case 'ArrowRight': case ' ': case 'ArrowDown':
  //     e.preventDefault(); this.next(); break;
  //   case 'ArrowLeft': case 'ArrowUp':
  //     e.preventDefault(); this.prev(); break;
  //   case 'Home': e.preventDefault(); this.goTo(0); break;
  //   case 'End': e.preventDefault(); this.goTo(this.total - 1); break;
  //   case 'f': case 'F':
  //     if (!document.fullscreenElement) document.documentElement.requestFullscreen();
  //     else document.exitFullscreen();
  //     break;
  // }
});
```

### Toggle logic

- If the switch block is uncommented (or partially uncommented), comment out ALL lines inside the listener callback
- If the switch block is fully commented out, uncomment ALL lines
- Preserve the `addEventListener` wrapper itself — only toggle the body

### Handling partial states

The file may have some controls already commented out (e.g., F-for-fullscreen disabled, arrows still active). When toggling OFF, comment out everything. When toggling ON, uncomment everything — restore the full enabled state above.

## Output

After toggling, report:
- Which files were modified
- New state: "ALL controls OFF" or "ALL controls ON"
- Example: "slides.html: ALL keyboard controls OFF (arrows, Home/End, Space, F)"
