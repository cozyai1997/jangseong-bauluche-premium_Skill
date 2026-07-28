# Tabs and verification

## Tab contract

- Give the container `role="tablist"` and an accessible label.
- Give every tab a stable `id`, `role="tab"`, `aria-controls`, and `aria-selected`.
- Keep exactly one tab at `tabIndex=0`; all others use `-1`.
- Give the active panel `role="tabpanel"` and `aria-labelledby` pointing to its active tab.
- Left/Up selects and focuses the previous tab with wrapping.
- Right/Down selects and focuses the next tab with wrapping.
- Home selects and focuses the first; End selects and focuses the last.
- Click selection and previous/next buttons update the same active index.
- Preserve visible focus and do not communicate selection by color alone.

One dynamic panel is valid when its label relationship updates atomically. Do not leave inactive duplicate panels exposed.

The current desktop grid and narrow-screen `nth-child` borders assume exactly four tabs. Replace those assumptions with count-independent layout before adding a type; verify that every tab remains reachable and that focus is never clipped.

## Focused verification

Add or update tests for:

1. stable unit order and exact verified facts;
2. unit `mediaKey` presence in the managed catalog;
3. `contain` as the only fit for every unit slot;
4. real default image dimensions and paths;
5. one selected and one focusable tab;
6. click, wrapping Arrow keys, Home, End, and previous/next controls;
7. correct panel label, plan, and facts after every selection;
8. full plan containment at desktop and narrow mobile;
9. reduced-motion behavior;
10. new-slot administrator, manifest, database seed, history, and all-or-nothing fallback behavior.

Run the current media-catalog, public-media render, unit interaction/render, administrator, schema, type, lint, and `build:vercel` checks affected by the change. Visually inspect both the committed default and a differently proportioned managed replacement.
