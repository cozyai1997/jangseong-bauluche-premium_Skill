---
name: bauluche-unit-plan-gallery
description: Use when a Jangseong Bauluche unit plan is cropped, clipped, too small, mismatched with its facts, replaced in the administrator, added as a new unit type, or when the unit tablist, tabpanel, arrow controls, responsive layout, keyboard behavior, alt text, or plan-asset dimensions need implementation or review.
---

# Bauluche Unit Plan Gallery

Treat a plan as a technical drawing: show all of it, pair it only with verified facts, and keep image, tab, and details on one stable record.

## Diagnose the asset before CSS

1. Inspect the actual decoded pixel dimensions, transparency or background, internal whitespace, orientation, and legibility of every affected default and managed image.
2. Inspect the container at desktop, 900 px, 640 px, narrow mobile, and text zoom.
3. Apply [plan-asset-contract.md](references/plan-asset-contract.md). Unit slots allow `contain` only. Never solve empty space by switching to `cover`, clipping overflow, or enlarging past the safe canvas.
4. Keep intrinsic dimensions and an intentional canvas size to avoid layout shift.

## Keep facts and media atomic

Use the entry in `app/content/home-content.ts` as the unit presentation record. Verify code, household count, exclusive area, supply area, contract area, ratio, description, and `mediaKey` against approved project material. Do not infer a missing value from a drawing or copy another type.

For a new type, follow [catalog-expansion.md](references/catalog-expansion.md). Expanding beyond the current four unit types changes the managed-media completeness contract; update all catalog, database, default, administrator, manifest, and test surfaces deliberately.

## Implement complete tabs

The current unit tabs have basic tab roles and relationships but do not yet implement roving focus or Arrow/Home/End behavior. Do not describe them as complete until those behaviors exist and are tested.

Follow [tabs-and-verification.md](references/tabs-and-verification.md). Use the development-project tab implementation as the local keyboard reference. Keep previous/next controls synchronized with the same active index.

Do not introduce a lightbox, URL state, pricing, room counts, or availability unless the user explicitly requests it and verified project data supports it.
