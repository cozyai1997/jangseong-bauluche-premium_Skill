---
name: bauluche-development-evidence-ui
description: Use when adding, updating, restyling, or reviewing the Jangseong Bauluche development-benefits section, its project facts, official source links, evidence date or disclaimer, desktop project tabs, mobile project articles, premium visual hierarchy, or reduced-motion behavior.
---

# Bauluche Development Evidence UI

Make the section feel premium through editorial clarity while keeping every mutable claim traceable and qualified.

## Establish evidence before copy

1. Inspect `app/components/development-projects.mjs`, `DevelopmentSection.tsx`, and `development-section.css`.
2. Open every cited primary public source. Record what it supports, its publication date, and the evidence cutoff date. If current verification is unavailable, preserve the existing qualified claim or omit the update.
3. Apply [evidence-contract.md](references/evidence-contract.md). Never promote a plan, target, estimate, or expected effect into a completed fact, guarantee, direct job count, or property-value promise.
4. Keep project data centralized and immutable. Preserve stable IDs, numbers, media keys, and typed unions unless the change deliberately expands the catalog.
5. Update the visible disclaimer date whenever the evidence set changes.

## Keep one accessible story in two layouts

Desktop uses one manually activated tablist and one tabpanel. Keep roving `tabIndex`, visible focus, click, wrapping Arrow keys, Home, and End. Do not autoplay.

At the mobile breakpoint, render every project as a full semantic article in source order. Do not replace the complete list with a hidden desktop panel, horizontal carousel, or collapsed content.

Use [interaction-and-presentation.md](references/interaction-and-presentation.md) for markup, motion, and visual constraints. Premium styling must not obscure status qualifiers, metrics, summaries, or source links.

## Verify the claim and the interface

Use [verification.md](references/verification.md). Add a failing data or interaction test before changing a contract. Check official link destinations manually, then run focused data, interaction, render, accessibility, type, lint, and Vercel-build checks.

If a new project needs a new administrator-managed image, coordinate the media catalog, manifest typing, admin slot list, defaults, and public fallback. Do not silently reuse an unrelated evidence image.
