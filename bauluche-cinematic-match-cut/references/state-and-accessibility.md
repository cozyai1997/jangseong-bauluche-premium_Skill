# State and accessibility contract

## Root state

The pre-hydration gate owns:

- `data-bauluche-intro`: `play` while active, `skip` after completion or bypass.
- `data-bauluche-intro-phase`: `playing`, `handoff`, or `done`.
- `data-bauluche-intro-exit`: `natural`, `skipped`, or `bypass`.
- start and deadline timestamps for hydration handoff.
- a disposable controller on `window.__baulucheIntroGate`.

Use `INTRO_DURATION_MS = 4000` and `INTRO_HANDOFF_MS = 1400`. The handoff therefore begins at 2600 ms. Schedule from `deadline - Date.now()` so slow hydration does not extend the experience.

Every full-document normal-motion load creates a fresh deadline. Old visit markers are irrelevant and browser storage must remain untouched.

## Input and focus

- The intro is a named modal dialog.
- Give the visible SKIP control initial focus without scrolling.
- Trap both Tab and Shift+Tab on SKIP while the modal is active.
- SKIP click and Escape finish immediately and record `skipped`.
- Natural completion records `natural`.
- After a played intro, focus `#hero-title` exactly once with `preventScroll`; keep the heading programmatically focusable with `tabIndex={-1}`.
- If the gate settles before hydration, allow hydration to claim pending focus restoration once.
- Remove event listeners, timers, body classes, and scroll lock on every exit and unmount.

## Reduced motion

When `prefers-reduced-motion: reduce` is true:

- set `skip/done/bypass` in the head gate;
- create no intro deadline or timers;
- do not focus SKIP or the hero;
- hide the intro and disable its transitions/animations;
- expose the header, hero copy, facts, and image immediately in a static state.

Do not convert reduced motion into a fast animation.
