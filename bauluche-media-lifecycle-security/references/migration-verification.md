# Migration and verification

## Migration discipline

1. Inspect current migrations, repository calls, generated database types, and source/database tests.
2. Write a failing invariant or concurrency test.
3. Add a new timestamped forward migration. Never edit an applied production migration.
4. Keep the change transactional and compatible with existing rows; backfill before adding a constraint that assumes new data.
5. Preserve explicit table locks only when the data transition requires them and document the lock order.
6. Update repository mappings and generated types when the schema or RPC signature changes.
7. Reset a local Supabase database from zero and run all migrations plus database tests.

## Required evidence

Run:

- database schema, RPC, and upload-stage pgTAP/source tests;
- repository and Supabase service tests;
- media API, manifest/fallback, history/restore, client secret-scan, type, and lint tests;
- Vercel production build;
- `git diff --check`.

Prove:

1. only valid stage transitions and immutable terminal tombstones;
2. reserve-before-sign and stage-before-slot locking;
3. activation/cleanup races cannot both win;
4. insert without a matching stage/current transition fails;
5. activation and completion replays are idempotent only when safe;
6. bounded `SKIP LOCKED` cleanup and independent retry;
7. prior/default restore, revision conflicts, active-first history, and current-plus-ten retention;
8. every incomplete/malformed/missing/runtime-failure manifest becomes all 19 defaults;
9. browser roles cannot read/write tables or execute media RPCs;
10. service role has no stage DELETE and no unintended grants;
11. functions have fixed search path and qualified objects;
12. bucket public read, 15 MiB/MIME limits, and no unsigned writes.

Inspect Supabase security and performance advisors after migration. In production, verify schema/migration version, grants, bucket configuration, a real upload/restore/public reflection, cleanup behavior, and logs without printing secrets or owner data.
