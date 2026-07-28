# Evidence and cleanup

## Completion report

Report:

- repository, branch, clean/dirty state, tested SHA, and pushed SHA;
- focused and full local commands with test counts and failures/warnings;
- whether local database reset/tests ran;
- migration version and advisor result when relevant;
- Vercel project, deployment ID, terminal status, deployed SHA, and production alias;
- production flows actually exercised;
- runtime/console/network observations;
- layers not verified and the concrete blocker.

Use non-secret identifiers only. Redact environment values, owner identity, tokens, cookies, magic links, database connection strings, and provider error bodies.

## Insufficient evidence

Do not claim completion from:

- `npm test` alone;
- unit tests alone;
- a local or legacy vinext build;
- a Vercel URL without READY status and SHA match;
- a pushed/merged commit without deployment provenance;
- a working UI without anonymous/non-owner/Origin denial checks;
- a small upload without direct-network evidence;
- stale generated output, old logs, or a prior conversation's result;
- local migration files without remote/local database evidence.

## Cleanup

After acceptance:

- restore any public slot changed only for testing, preferably to its committed default;
- verify no temporary callback wildcard or preview URL remains;
- remove temporary branch-scoped environment entries only when their exact purpose and ownership are known;
- allow staged-object cleanup through the supported terminal lifecycle;
- confirm the worktree contains no accidental screenshots, keys, links, dumps, or generated secrets;
- leave audit tombstones and legitimate version history intact.

Report what was restored or removed and whether recovery remains possible. If cleanup would delete material data or configuration outside the task's authority, stop and request direction.
