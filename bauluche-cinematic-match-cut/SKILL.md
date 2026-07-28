---
name: bauluche-cinematic-match-cut
description: Use when changing, debugging, or reviewing the Jangseong Bauluche cinematic intro, its four-second replay-on-refresh behavior, the portal-to-hero match cut, shared hero image crop, pre-hydration timing, SKIP or Escape behavior, focus handling, scroll lock, or reduced-motion bypass.
---

# Bauluche Cinematic Match Cut

Preserve one continuous visual and interaction contract from the first head script through the hydrated hero.

## Keep one authoritative timeline

1. Start the gate in `app/components/IntroGateScript.tsx`, rendered from `app/layout.tsx` before the body.
2. Keep timing constants and pure transitions in `app/components/intro-state.mjs`.
3. For every normal-motion full document load:
   - start in `playing`;
   - enter `handoff` at 2600 ms;
   - reach `done` at 4000 ms.
4. Treat the pre-hydration deadline as authoritative. Hydration must calculate remaining time, never restart four seconds.
5. Never read or write `localStorage`, `sessionStorage`, cookies, or a visit marker. A refresh must replay the intro.
6. Make natural completion, SKIP, Escape, late hydration, and reduced-motion bypass idempotent.

Read [state-and-accessibility.md](references/state-and-accessibility.md) before modifying timers, the gate controller, root data attributes, focus, or scroll behavior.

## Preserve the match cut

Pass the same resolved `media["hero.main"]` object to `CinematicIntro` and `HeroSection`. Match URL, fit, focal coordinates, dimensions, stage height, base scale, and breakpoint crop; do not approximate one side independently.

Use [visual-geometry.md](references/visual-geometry.md) for the CSS and media invariants. Keep the handoff portal-driven, with the hero entering beneath it. Avoid a blanket cross-fade that hides crop drift.

## Verify behavior, not only source text

Use [verification.md](references/verification.md). Add or update a failing test before changing a contract. Exercise timing at 2599/2600/3999/4000 ms, two independent full-document loads, late hydration, reduced motion, SKIP, Escape, focus restoration, and shared media geometry.

Do not claim accessibility from `role="dialog"` alone. Verify focus containment, hero focus after a played intro, no focus theft on bypass, scroll-lock cleanup, and static visible hero content under reduced motion.
