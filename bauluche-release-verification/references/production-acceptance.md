# Production acceptance

## Configuration

Confirm without exposing values:

- the correct Vercel team/project and production branch;
- all five required environment names in the correct production scope;
- exact site origin and exact `/auth/callback` allowlist, with no wildcard;
- the Bauluche Supabase project, public Storage bucket, MIME/size limits, and advisor state;
- the Vercel build command is `npm run build:vercel` and region is `icn1`.

Do not confuse the local `supabase/config.toml` label with the linked production project. Do not use the legacy Sites project, Cloudflare D1/R2, or vinext build as production evidence.

## Deployment provenance

1. Fetch remote state.
2. Commit the exact tested source and push the intended branch.
3. Deploy that source through the linked Vercel project.
4. Wait for terminal `READY`; a queued/building URL is not success.
5. Match deployment commit SHA to the tested/pushed SHA.
6. Confirm the production alias resolves to that deployment.
7. Inspect build and runtime logs for the acceptance window.

## Public/admin/media journey

Exercise applicable steps:

1. public page renders all 19 canonical media slots or the complete default set;
2. normal-motion refresh replays the four-second intro; reduced motion bypasses it;
3. anonymous `/admin` redirects to login;
4. the configured owner requests and completes a magic link;
5. administrator shows six groups and 19 cards;
6. choose a valid near-limit image, edit alt/fit/focal, and observe direct progress;
7. network trace shows only JSON through the app and TUS POST/PATCH bytes to Supabase Storage;
8. card/public page change only after completion;
9. reload preserves the committed result;
10. history is private; restore prior/default and confirm public reflection;
11. stale revision returns a recoverable conflict;
12. logout works;
13. anonymous API, cross-Origin mutation, verified non-owner, and forged legacy Sites headers fail.

Check client console, failed network requests, Vercel runtime errors, Supabase logs, and security/performance advisors. Do not include secrets or identity-bearing data in evidence.
