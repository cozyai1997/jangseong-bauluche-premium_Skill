---
name: bauluche-project-orientation
description: Use when beginning work on the Jangseong Bauluche Premium website, locating its active repository or worktree, deciding which runtime is canonical, routing a change to the correct code area, or separating the live Vercel/Supabase path from retained Sites/Cloudflare files.
---

# Bauluche Project Orientation

Orient before changing code. Establish the repository, runtime, affected subsystem, and required verification from current evidence rather than from an old plan or remembered path.

## Orient the task

1. Locate the Git repository whose origin or package identity is `cozyai1997/jangseong-bauluche-premium`. Do not hardcode a temporary worktree path.
2. Read `git status`, the current branch and SHA, `README.md`, `package.json`, `next.config.ts`, `vercel.json`, and `.openai/hosting.json`.
3. State the canonical runtime before proposing changes:
   - Next.js on Vercel for the public site and administrator.
   - Supabase Auth, Postgres, and Storage for owner access and managed media.
   - Sites/Cloudflare/vinext files are retained legacy or recovery paths unless the user explicitly scopes work to them.
4. Map the request with [project-map.md](references/project-map.md).
5. Read [runtime-topology.md](references/runtime-topology.md) whenever the task mentions deployment, authentication, environment variables, storage, uploads, callbacks, or production.
6. Select the smallest verification set with [test-routing.md](references/test-routing.md). Do not treat `npm test` as complete release evidence.

## Report orientation

Before implementation, report:

- repository, branch, SHA, and dirty-state risks;
- canonical runtime and any legacy trap encountered;
- code areas and contracts likely affected;
- verification and production evidence required.

Never reveal environment values, the configured owner email, tokens, service-role keys, magic links, or provider error payloads. Refer to environment variables by name only.
