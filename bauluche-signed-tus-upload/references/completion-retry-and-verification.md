# Completion, retry, and verification

## Complete request

Send:

- prepare metadata: revision, original filename, content type, byte size;
- exact grant object path;
- alt text, fit, focal X, and focal Y.

The server injects the authenticated actor.

## Trust order

1. Verify owner and exact Origin.
2. Validate catalog slot and canonical path; require path slot to match.
3. Return an already-recorded current result only for safe response-loss idempotency.
4. Validate filename/MIME/size/settings and path extension.
5. Load the staged record and require the exact tuple: path, UUID/version, slot, expected revision, sanitized filename, MIME, byte size, and actor.
6. Reject a cleanup-claimed or incompatible terminal stage.
7. Read Storage object info and download the object.
8. Require declared size/MIME to match Storage metadata and downloaded bytes.
9. Detect actual image signature, MIME, canonical extension, size, and dimensions.
10. Activate through the fenced repository, then run best-effort retention cleanup.

## Retry

Store prepared completion state only after TUS success. On lost response, network failure, or retryable service-unavailable completion, retain the exact body/path and call complete only.

Clear it on:

- success;
- terminal invalid, missing, or revision-conflict response;
- new or removed file;
- close or unmount.

Prepare/TUS failure has no completion-only state, so a retry begins with a new prepare.

## Verification

Run direct-upload, admin-interaction, media-API, Supabase service/storage, type, lint, secret-scan, and Vercel-build checks. Assert:

- exact endpoint and grant shape/origin;
- only the signed custom header and no API/upsert credential;
- 6 MiB chunks, retry delays, integer progress;
- exact-match resume and nonmatch rejection;
- prepare then upload then complete order;
- no complete after upload failure;
- lost/503 complete retry without re-upload;
- terminal clearing behavior;
- missing object, stage mismatch, stored metadata/byte mismatch, idempotent completion, and revision conflict.

In a browser, upload a near-15 MiB image and confirm no image body crosses a Vercel Function.
