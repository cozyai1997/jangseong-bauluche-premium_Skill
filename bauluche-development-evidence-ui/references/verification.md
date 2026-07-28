# Verification

## Focused files

- `app/components/development-projects.mjs`
- `app/components/DevelopmentSection.tsx`
- `app/components/development-section.css`
- `app/media/catalog.mjs` only when managed slots change
- media manifest and admin mapping when adding a slot

## Automated evidence

Run the current equivalents of:

- `tests/development-section.test.mjs`
- `tests/development-interactions.test.tsx`
- `tests/development-assets.test.mjs`
- relevant rendered HTML and public-media render tests
- type checking and lint
- `npm run build:vercel`

Assert:

1. fixed project order, stable IDs, expected count, HTTPS sources, and evidence date;
2. tab/tabpanel relationships and one roving tab stop;
3. wrapping Arrow keys plus Home and End move both focus and selection;
4. all projects remain complete mobile articles;
5. no autoplay, carousel library, excessive scale, or horizontal overflow;
6. reduced motion removes transitions;
7. any added managed slot exists in all 19-slot manifest/admin/default contracts, with the expected new total if expansion is deliberate.

## Manual evidence review

Open each official source and map every title, status, metric, and summary sentence to supported wording. Check the evidence cutoff and disclaimer. Inspect keyboard operation, focus visibility, source-link text, image crop, no-content-with-JavaScript edge cases, reduced motion, 1440 px desktop, 900 px boundary, and approximately 390 px mobile.
