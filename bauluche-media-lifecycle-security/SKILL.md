---
name: bauluche-media-lifecycle-security
description: Use when changing, debugging, or auditing Jangseong Bauluche media_slots, media_versions, media_upload_stages, Supabase migrations or RPCs, staged-to-activated fencing, upload cleanup races, idempotent activation, version history, prior/default restore, retention pruning, all-19-slot public fallback, RLS, grants, function security, the bauluche-media Storage bucket, service-role access, or database security advisors.
---

# Bauluche Media Lifecycle Security

Preserve one irreversible database decision for every staged object, one revisioned current image per slot, and a fail-closed public manifest.

## Fence activation from cleanup

Read [stage-fencing.md](references/stage-fencing.md). Every reservation starts `staged` and terminates as either `activated` or `cleanup_claimed`; both terminal outcomes are immutable audit tombstones.

Reserve before signing. Lock the upload stage before the media slot. Require a matching staged tuple and the slot revision transition before inserting a version. Activation and cleanup must never both win.

Claim cleanup in the database and commit before deleting Storage bytes. Never delete a recorded version. Use bounded `FOR UPDATE SKIP LOCKED` cleanup and keep tombstones rather than erasing the race evidence.

## Preserve revisioned history

Read [versions-retention-fallback.md](references/versions-retention-fallback.md). Enforce same-slot current-version identity, optimistic revision checks, idempotent already-current completion, prior/default restore, and retention that always preserves the current version.

Public resolution is all-or-nothing. Resolve the complete ordered set of 19 canonical slots and confirm every active object, or return all 19 immutable committed defaults. Never mix managed and fallback media after any missing, duplicate, malformed, query, runtime, or Storage failure.

## Keep browser roles powerless

Read [database-storage-security.md](references/database-storage-security.md). Enable RLS, define no browser table policies, revoke table/RPC access from public browser roles, and grant only the required service-role operations. Keep stage deletion unavailable so audit tombstones survive.

Use fixed empty function `search_path` and explicit schema qualification. The public bucket is readable but accepts writes only through the signed server-created flow. Create a privileged client only after owner authorization. Never expose keys, provider errors, SQL, internal paths, or owner identity.

## Migrate and prove

Use [migration-verification.md](references/migration-verification.md). Add a new forward migration; never rewrite an applied one. Test state transitions and real concurrent races, reset the local Supabase database, run database plus application suites, inspect generated types, and review Supabase security/performance advisors before production.

Keep browser TUS transport and owner login in their separate skills.
