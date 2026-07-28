# Dialogs, history, and verification

## Modal behavior

- Use `role="dialog"`, `aria-modal="true"`, and a unique labelled title.
- Move focus to an intentional control after mount.
- Trap Tab and Shift+Tab inside.
- Escape and backdrop click close only when not busy.
- Lock body scroll while open and restore the prior value.
- On every close/unmount, remove listeners, cancel pending focus frames, revoke preview URLs, and return focus to the invoking control.
- Put active errors in an in-dialog alert or otherwise ensure they are not hidden behind the modal. Associate field errors with their fields.
- Express upload progress with perceivable status/progress semantics, not visual text alone.

## History

- Load protected history for the selected slot and cap display at ten.
- Show the current version first/marked, plus original filename, time, and protected thumbnail.
- Keep the committed default as a separate restore target with `versionId: null`.
- Require confirmation and send the displayed `expectedRevision`.
- On `409`, preserve the intended restore, offer latest-state adoption, then reload history.
- Provide an in-dialog load error and retry path.
- A version record stores the photo and file metadata, not a historical display-settings snapshot. Describe restore as changing the photo while current alt/fit/focal remain unless the model is deliberately expanded.

## Verification

Run the current equivalents of media-catalog, admin-state, admin-render, admin-interactions, media validation/API, typecheck, lint, render, secret scan, and `build:vercel`.

Assert:

1. six ordered groups and 19 cards;
2. local preview replacement and object-URL revocation;
3. extension/MIME/size/zero-byte/alt/fit/focal validation;
4. pointer and keyboard focal controls;
5. contain-only behavior;
6. progress semantics and duplicate-submit protection;
7. no card update before complete;
8. upload failure skips complete;
9. completion retry does not re-upload;
10. conflict preserves local work and adopts latest revision explicitly;
11. history cap, protected thumbnails, prior/default restore, and conflict retry;
12. modal focus trap, busy close prevention, Escape, scroll cleanup, and trigger focus restoration.
