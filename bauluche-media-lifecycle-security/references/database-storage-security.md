# Database and Storage security

## Tables

Enable RLS on:

- `public.media_slots`
- `public.media_versions`
- `public.media_upload_stages`

Define no policies for `anon` or `authenticated`. Revoke all table privileges from `public`, `anon`, and `authenticated`.

Grant only required operations to `service_role`:

- slots and versions: the operations used by the repository;
- upload stages: select, insert, and update, deliberately not delete.

Do not rely on RLS to constrain service-role code; the guarded server service and RPC invariants are the boundary.

## Functions

For every media RPC and trigger function:

- set `search_path = ''`;
- qualify `public`, `storage`, and `pg_catalog` objects explicitly;
- revoke execute from `public`, `anon`, and `authenticated`;
- grant execute only to `service_role` when the repository calls it;
- preserve trigger-only functions from direct browser execution.

Avoid dynamic SQL and ambiguous names. Keep optimistic revision, stage tuple, terminal state, and lock-order checks inside the transaction.

## Storage

Bucket: `bauluche-media`.

- Public read is intentional for public site images.
- File-size limit is 15 MiB.
- Allowed MIME types are JPEG, PNG, and WebP.
- Do not create unsigned browser INSERT/UPDATE/DELETE policies.
- Browser writes use a narrow signed upload token created after owner authorization; ordinary anonymous/authenticated clients cannot write.

The Supabase secret/service credential stays server-only. Do not name it with `NEXT_PUBLIC_`, serialize it, log it, or create the privileged media runtime before the request is authenticated and Origin-checked.
