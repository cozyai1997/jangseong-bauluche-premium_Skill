# Visual geometry contract

## Shared media

`HomeExperience.tsx` must pass the exact `media["hero.main"]` resolved object to both:

- `CinematicIntro`
- `HeroSection`

Both sides must use its `src`, `fit`, `focalX`, and `focalY`. Preserve the managed-media slot identity. An administrator crop change must affect intro and hero together on the next render.

## Shared stage

The portal frame and hero image use `height: var(--hero-stage-height)`:

- desktop: `max(760px, 100svh)`;
- at 900 px: `max(850px, 100svh)`;
- at 640 px: `max(820px, 100svh)`.

Keep the intro portrait portal centered against the visible viewport when the shared stage is taller by deriving its tail from the same stage variable.

## Match endpoints

- Keep the same intrinsic width and height values on both images.
- Keep inline resolved fit and focal positioning authoritative over decorative CSS defaults.
- Keep the image base scale synchronized at the handoff boundary.
- Animate the portal bounds and surface away while the underlying hero image enters.
- Coordinate header, hero copy, and facts after the image match begins; do not let their layout centering depend on the transform animation channel.

Check desktop, tablet, narrow mobile, and short viewport. A match cut is wrong if the same feature in the image jumps even when each frame looks acceptable in isolation.
