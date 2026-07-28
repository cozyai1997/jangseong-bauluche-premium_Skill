---
name: bauluche-media-control-editor
description: Use when changing, debugging, or reviewing the Jangseong Bauluche private image administrator, its six media groups or 19 fixed cards, replace/settings/history dialogs, local preview, alt text, cover/contain controls, focal-point picker, upload progress, completion retry, revision conflict, object-URL cleanup, history list, prior/default restore, modal focus, or administrator error/status feedback.
---

# Bauluche Media Control Editor

Keep every public image addressable through one immutable slot and show server-confirmed state only after the complete operation succeeds.

## Preserve the catalog

Read [catalog-contract.md](references/catalog-contract.md). The current administrator renders six ordered groups and 19 immutable slot keys from `app/media/catalog.mjs`. A slot defines its label, description, committed default, alt, allowed fits, focal defaults, recommended ratio, and minimum dimensions.

Do not create page-specific upload controls or rename/reuse a slot. A new public image location is a catalog/database/default/manifest expansion, not a card-only edit.

## Preserve local work until confirmation

1. Validate the selected file and create a local object-URL preview.
2. Allow alt, fit, and focal editing only within the slot contract.
3. Show progress from the injected direct-upload transport.
4. Keep the card unchanged while preparing, uploading, or completing.
5. Replace card state only with the confirmed server slot returned after completion.
6. On validation, network, upload, completion, or `409` conflict, keep the selected file, preview, and unsaved controls so the owner can recover.
7. On completion-only retry, reuse the prepared staged object; do not upload bytes again.
8. Clear prepared retry state and revoke preview URLs when selecting another file, cancelling the selection, closing, confirming, or unmounting.

Use [editor-state.md](references/editor-state.md) for validation, conflicts, progress, and retry behavior. Treat signed TUS transport and database fencing as separate dependencies.

Keep the established alt-text boundary exactly 1-300 trimmed characters across the dialog, API, service, and tests.

## Keep dialogs operable

Use [dialogs-history-and-verification.md](references/dialogs-history-and-verification.md). Editor and history surfaces are named modal dialogs with initial focus, Tab containment, Escape/background close only while idle, scroll lock, and focus restoration to the trigger.

Keep errors and status perceivable while a modal is open. History shows protected thumbnails, at most ten recent versions, current state, confirmation, prior-photo restore, and committed-default restore. Do not imply that historical alt/fit/focal settings are restored unless the version model is expanded to store them.
