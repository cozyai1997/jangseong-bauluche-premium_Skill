# Editor state

## Local preview

- Reset the file input after selection so the same file can be chosen again.
- Revoke the previous object URL before replacing it.
- Read decoded dimensions and show filename, MIME, byte size, and dimensions.
- Warn below the recommendation without preventing an otherwise valid save.
- Keep both the main preview and focal preview synchronized.

Focal keyboard behavior:

- X: Left/Right by 1, or 10 with Shift.
- Y: Up/Down by 1, or 10 with Shift.
- Home: 0; End: 100.
- Clamp pointer/touch and keyboard values to 0–100.

## Save state

Block duplicate submission. Disable close and destructive controls while a request is active. Announce progress and phase changes accessibly.

Replacement:

1. prepare with the displayed revision and file metadata;
2. direct upload through the provided transport;
3. complete with the exact prepared path plus display settings;
4. apply only the returned confirmed slot.

Settings-only save skips file transport but still uses expected revision.

## Failure and retry

- Ordinary failure: keep preview/settings, stop busy state, show actionable generic copy.
- Direct-upload failure: do not call complete.
- Lost response or retryable completion failure after a successful upload: retain prepared grant/body and retry complete only.
- New file, cancel, close, or terminal failure: discard completion-only retry state.
- `409`: retain preview and edits, store the latest server slot, explain the conflict, and let the owner adopt the latest revision before retrying. Do not silently overwrite.

The page card, source badge, revision, and history current marker change only after a successful server response.
