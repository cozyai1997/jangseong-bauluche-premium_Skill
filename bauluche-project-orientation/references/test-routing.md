# Test routing

Read current `package.json` scripts before running commands.

## Focused checks

- Intro/hero: intro-state, cinematic intro, public media, and render tests.
- Development section: development data, interaction/accessibility, and render tests.
- Unit plans: unit-plan behavior, catalog, asset dimensions, and render tests.
- Admin editor: admin state, render, and interaction tests.
- Authentication: admin policy, auth flow, admin auth, proxy, and origin checks.
- Upload transport: direct upload, media API, storage, service, and completion-retry tests.
- Schema/lifecycle: repository and service tests plus Supabase database tests.

## Release matrix

Run the equivalent current scripts for:

1. type checking;
2. lint;
3. unit tests;
4. DOM interaction tests;
5. render tests;
6. Vercel production build;
7. client-bundle secret scan;
8. `git diff --check`.

Run the retained vinext/legacy build only when changed code still affects that path or the repository's release policy requires it.

For migrations, RPCs, grants, RLS, or generated database types, also reset the local Supabase database and run the database test suite. Docker/local Supabase availability is a prerequisite; report an unavailable prerequisite rather than claiming the database was verified.

## Completion evidence

Before claiming production success, match the deployed commit SHA, confirm a terminal `READY` deployment, inspect runtime logs, and exercise the affected path. For admin/media changes, cover anonymous redirect, owner login, 19 media cards, direct upload, restore, public reflection, logout, and forged-header rejection as applicable.
