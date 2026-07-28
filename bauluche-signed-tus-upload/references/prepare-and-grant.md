# Prepare and grant

## Request

The browser sends JSON to the encoded slot prepare route:

- `expectedRevision`
- `originalFilename`
- `contentType`
- `byteSize`

The server supplies the verified actor. It validates:

- owner authentication and exact mutation/configured Origin;
- immutable catalog slot;
- non-negative expected revision;
- sanitized filename;
- JPEG, PNG, or WebP MIME and matching canonical extension;
- byte size from 1 through 15 MiB.

Create a UUID and canonical path:

`media/<slotKey>/<uuid>.<jpg|png|webp>`

Reserve the immutable upload stage before requesting a signed upload with upsert disabled. If signing fails, claim the stage for cleanup before returning the generic failure.

## Response

The JSON object contains only:

```text
objectPath
token
expiresIn = 7200
directStorageUrl
```

The direct origin is the configured/pinned Supabase Storage hostname. Do not return an API key, service key, bucket write credential, actor, alternate path, or provider error.

Keep the response private and no-store. Map unauthenticated, forbidden, invalid, unknown-slot, revision, and unavailable failures through the fixed admin error contract.
