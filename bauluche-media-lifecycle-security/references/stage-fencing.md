# Upload stage fencing

## State machine

`media_upload_stages.state` permits:

```text
staged -> activated
staged -> cleanup_claimed
```

`activated` and `cleanup_claimed` are terminal. Their audit timestamps and immutable identity fields must remain consistent and cannot be rewritten back to staged or into each other.

Stage identity binds:

- canonical object path;
- UUID version ID;
- immutable slot key;
- expected revision;
- sanitized original filename;
- MIME and byte size;
- verified actor;
- creation and upload expiry.

Reserve the stage before creating a signed upload. Reject path/version collisions and cross-slot identity.

## Activation

Use the established lock order: stage first, slot second. Require:

- stage is still `staged`;
- complete input equals the reserved tuple;
- slot revision equals the expected revision;
- version path/ID/slot/file metadata equal the stage;
- current pointer transition and version insert occur in one transaction.

The insert guard requires the matching stage and slot transition, then terminalizes the stage as `activated`. An already-recorded object may return idempotently only when it is still current. A recorded inactive history object is not a successful replay.

## Cleanup

Cleanup must win a database claim before Storage deletion. If activation already won or the object became a recorded version, preserve it. If a claim races with activation, re-query recorded/current state before deleting.

Claim expired and retryable work in bounded batches with `FOR UPDATE SKIP LOCKED`. Retry object deletions independently. Retain `cleanup_claimed` rows as tombstones; record attempts and final confirmed cleanup rather than deleting the audit row.

Never use service-role DELETE on `media_upload_stages`.
