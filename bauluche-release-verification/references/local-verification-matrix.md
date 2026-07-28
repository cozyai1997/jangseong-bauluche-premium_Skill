# Local verification matrix

Read the current `package.json` before running commands.

## Baseline release checks

Run fresh:

1. `npm run typecheck`
2. `npm run lint`
3. `npm run test:unit`
4. `npm run test:dom`
5. retained `npm run build` when shared/legacy behavior is affected or repository policy requires it
6. `npm run test:render`
7. `npm run build:vercel`
8. `node --test tests/client-bundle-secrets.test.mjs`
9. `git diff --check`

Record exit status, test counts, lint warnings versus errors, and meaningful build warnings. Do not hide a skipped or unavailable check.

## Focus routing

- Intro/hero: cinematic intro, public media, rendered HTML.
- Development: data/assets, interaction, rendered HTML.
- Unit plans: unit assets/interactions, catalog, public render.
- Owner auth: admin policy/auth, auth flow, proxy/session, admin login render.
- Editor: catalog/state/render/interactions and media validation/API.
- Signed upload: direct upload, editor completion retry, media API/service/storage.
- Lifecycle/security: repository/service/API, manifest/fallback, database schema/RPC/stage tests, secret scan.

Focused green tests do not replace the release matrix.

## Database changes

For migrations, RPC signatures, triggers, constraints, grants, RLS, Storage settings, or generated database types:

1. start the supported local Supabase/Docker stack;
2. reset the local database from zero so every migration applies in order;
3. run `npm run test:db`;
4. run source-level migration/grant tests;
5. regenerate or verify database types;
6. inspect the migration diff and advisor output.

Never edit an applied migration to make a local reset pass. Add a forward migration.

## Secret hygiene

Search built client output and source boundaries for server-secret markers. Check environment variable names and scopes only:

- `NEXT_PUBLIC_SUPABASE_URL`
- `NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY`
- `SUPABASE_SECRET_KEY`
- `ADMIN_EMAIL`
- `NEXT_PUBLIC_SITE_URL`

Never print values, the owner address, magic links, cookies, upload tokens, or provider error payloads.
