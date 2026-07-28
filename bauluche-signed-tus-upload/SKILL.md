---
name: bauluche-signed-tus-upload
description: Use when changing, debugging, or reviewing Jangseong Bauluche large image uploads, the admin prepare or complete endpoints, Supabase signed upload grants, the direct Storage origin, resumable TUS endpoint or headers, 6 MiB chunking, upload progress, resume fingerprints or metadata, response-loss recovery, completion-only retry, stored-object validation, or Vercel upload bandwidth.
---

# Bauluche Signed TUS Upload

Keep binary image bytes out of Vercel. The application authorizes and signs, the browser uploads directly to Supabase Storage, and the application validates and activates afterward.

## Prepare a narrow grant

Authorize the owner and verify exact configured Origin before parsing protected input or opening a privileged runtime. Validate slot, expected revision, filename, MIME, extension, and byte size. Reserve the staged canonical path before signing.

Return exactly four fields: `objectPath`, `token`, `expiresIn: 7200`, and `directStorageUrl`. The client rejects extra fields, empty values, a different expiry, or a different Storage origin.

Read [prepare-and-grant.md](references/prepare-and-grant.md). Never accept `actorEmail` or an object path from the browser during prepare.

## Upload directly

Use the exact signed endpoint:

`{directStorageUrl}/storage/v1/upload/resumable/sign`

Configure `x-signature` with the grant token. Do not configure `Authorization`, `apikey`, or `x-upsert`. Use the exact metadata, 6 MiB chunks, bounded retry delays, and resume matching in [direct-tus.md](references/direct-tus.md).

Progress is rounded from uploaded/total bytes, clamped to 0-100, and omitted when total is unknown. No API route or Vercel Function receives the image body.

## Complete authoritatively

After TUS success, send the exact staged path and original prepare metadata plus alt/fit/focal settings to complete. Reauthorize and recheck Origin. Validate path-to-slot binding, stage tuple, Storage metadata, downloaded byte size, detected image signature/MIME/extension, dimensions, and revision before activation.

Use [completion-retry-and-verification.md](references/completion-retry-and-verification.md). A retryable lost/503 completion keeps the prepared body and calls complete only; it never prepares or uploads again. Clear completion-only state on success, terminal 400/404/409, new file, cancel, close, or unmount.

Treat SQL stage fencing, terminal cleanup claims, and atomic activation as the media-lifecycle dependency. Do not weaken them in transport code.
