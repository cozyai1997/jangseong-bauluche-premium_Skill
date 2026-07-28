# Versions, retention, and fallback

## Slot and version identity

- `media_slots.slot_key` is immutable and catalog-owned.
- `media_versions` has unique object paths and a same-slot identity.
- The deferred current-version foreign key links `(slot_key, current_version_id)` to the version in that same slot.
- Every settings update, activation, or restore uses expected revision and increments the slot revision atomically.

History is newest first with the active version first/marked. The administrator displays at most ten recent versions.

## Restore

- Reject a version from another slot.
- Reject a missing or non-canonical version/object.
- Restore a prior image by protected version ID.
- Restore the committed default with `versionId: null`.
- Keep the current alt/fit/focal settings unless the data model is deliberately expanded.
- Increment revision and preserve the former current image in history.

## Retention

Keep the current version plus ten inactive versions. Pruning must never delete the current pointer target. Return only prunable object paths from the committed database operation; Storage deletion afterward is best effort. A Storage failure does not roll back the already-safe database state or expose provider detail.

## Public manifest

The runtime must return exactly one canonical row per one of the 19 ordered catalog keys. Validate:

- exact count, no missing or duplicate slot;
- current pointer/version/slot consistency;
- canonical UUID object path bound to the slot;
- existence of every active Storage object.

If runtime configuration is absent, acquisition throws, a query fails, count/identity/path is invalid, or any active object is missing/uncertain, return the complete immutable default manifest. Never return a partially managed set. The administrator similarly receives all defaults, a warning, and disabled persistence when storage is unavailable.
