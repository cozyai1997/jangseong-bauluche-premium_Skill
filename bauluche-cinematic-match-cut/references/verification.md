# Verification

## Primary files

- `app/components/intro-state.mjs`
- `app/components/IntroGateScript.tsx`
- `app/components/CinematicIntro.tsx`
- `app/components/HeroSection.tsx`
- `app/components/HomeExperience.tsx`
- `app/components/cinematic-intro.css`
- `app/globals.css`
- `app/layout.tsx`

## Focused automated evidence

Run the current equivalents of:

- `tests/cinematic-intro.test.mjs`
- `tests/public-media-render.test.mjs`
- `tests/rendered-html.test.mjs`
- relevant DOM interaction tests
- type checking and lint
- `npm run build:vercel`

Keep tests for:

1. fresh `playing` state on two independent full-document loads with zero storage access;
2. handoff at 2600 ms and completion at 4000 ms;
3. hydration scheduling from the original deadline;
4. SKIP click and Escape before and after hydration;
5. one-time hero focus after a played intro;
6. no focus movement and no intro under reduced motion;
7. root scroll lock while active and cleanup after every exit;
8. the exact same `hero.main` media object, fit, focal position, dimensions, and stage height on both sides.

## Visual inspection

Inspect at least wide desktop, 900 px, 640 px, a narrow phone, and a short landscape viewport. Reload rather than only navigating. Watch the same image landmark through the portal expansion into the hero and confirm there is no crop jump, flash, scrollbar shift, blank frame, or late four-second restart.
