# Catalog contract

## Fixed structure

The current catalog contains 19 immutable slots in six ordered groups:

1. hero;
2. story;
3. location;
4. unit;
5. development;
6. social.

Render cards and group counts from `MEDIA_GROUPS` and `MEDIA_SLOTS`; do not maintain a parallel UI list. `MediaSlotKey` and the public/admin manifests derive from this catalog.

Each slot owns:

- durable key, group, label, and description;
- committed default path and factual default alt;
- default fit and `allowedFits`;
- default focal X/Y;
- recommended ratio and minimum width/height.

Cover-only and contain-only slots must not expose an unavailable mode. Contain-only plans disable focal controls because the complete drawing remains visible.

## Validation

- Formats: JPEG, PNG, WebP.
- Maximum size: 15 MiB; reject zero bytes.
- Validate filename extension and declared MIME in the client for early feedback.
- The server/storage completion path remains authoritative for actual bytes, MIME, size, and dimensions.
- Alt text: trimmed, required, 1–300 characters.
- Fit: one of the selected slot's `allowedFits`.
- Focal X/Y: finite integers from 0 through 100.
- Minimum dimensions are advisory; warn rather than silently upscaling or cropping.

Use concise informative alt for content images. Preserve empty/decorative treatment only where the consuming component deliberately hides the image from assistive technology.

## Expansion

Adding a slot requires a committed default asset, real dimensions, catalog entry, database seed migration, generated/derived types, public all-or-nothing manifest, administrator card, history/restore support, and fixed-key/count test updates. Never make the editor accept arbitrary runtime slot names.
