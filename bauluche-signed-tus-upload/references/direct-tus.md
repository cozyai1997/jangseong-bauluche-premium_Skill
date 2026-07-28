# Direct TUS contract

Use `tus-js-client` with:

- endpoint: `<directStorageUrl>/storage/v1/upload/resumable/sign`
- configured header: `x-signature: <token>`
- `chunkSize: 6 * 1024 * 1024`
- `retryDelays: [0, 3000, 5000, 10000, 20000]`
- `uploadDataDuringCreation: true`
- `removeFingerprintOnSuccess: true`

Do not configure `Authorization`, `apikey`, `x-upsert`, or an application bearer token. Protocol headers added by the TUS client are separate from application credentials.

Metadata is exact:

```text
bucketName: bauluche-media
objectName: <grant.objectPath>
contentType: <file.type>
cacheControl: 31536000
```

Before starting, inspect previous uploads. Resume only a candidate whose metadata matches all three:

- bucket name;
- exact staged object path;
- file content type.

A near match is not resumable. A previous-upload lookup failure rejects rather than silently starting a second object. Remove the successful fingerprint so a completed object is not resumed later.

Compute progress as `round(bytesUploaded / bytesTotal * 100)`, then clamp to 0 through 100. Emit nothing for a non-positive total.

The browser network trace should show prepare/complete JSON to the app and TUS POST/PATCH bytes to the Supabase Storage hostname.
