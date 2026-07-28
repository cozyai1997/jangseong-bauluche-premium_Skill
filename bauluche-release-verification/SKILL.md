---
name: bauluche-release-verification
description: Use before claiming a Jangseong Bauluche change complete, committing or pushing it, promoting or deploying to Vercel production, applying a Supabase migration, changing Auth callbacks or environment configuration, or after modifying administrator login, managed media, signed uploads, database security, public rendering, or production infrastructure.
---

# Bauluche Release Verification

Prove the exact source, local checks, deployment, data plane, and user flow. Historical success, a green build, or a deployment URL alone is not completion evidence.

## Prove the target

1. Locate the canonical Git repository and record branch, clean/dirty state, HEAD SHA, upstream, and remote freshness.
2. Preserve unrelated user changes. Do not deploy an uncommitted or ambiguous source tree.
3. Resolve the actual Vercel team/project link; never infer IDs from a URL or reuse `.openai/hosting.json`.
4. Confirm the Supabase project reference is the Bauluche project before any database operation. Never operate on another project with a similar organization name.
5. Treat Next.js/Vercel plus Supabase as production. Vinext/Sites/Cloudflare/D1/R2 is retained legacy.

## Run fresh local evidence

Use [local-verification-matrix.md](references/local-verification-matrix.md). `npm test` is insufficient because it omits type checking, lint, database tests, the Vercel build, and the separate client-secret scan.

Route the focused tests first, then run the complete matrix. For database/RPC/RLS/grant changes, reset local Supabase from zero and run database tests. Report unavailable Docker or tooling instead of claiming that layer passed.

## Deploy only when authorized

Deployment changes external state. When the task authorizes it, commit and push the exact tested tree, deploy that SHA, wait for terminal Vercel `READY`, and confirm the production alias points to it. Verify environment variable names and scopes without printing values or owner identity.

Use [production-acceptance.md](references/production-acceptance.md). Exercise the affected public/admin/media flow, inspect Vercel logs and Supabase advisors, and prove upload bytes bypass Vercel.

## Close with evidence and cleanup

Use [evidence-and-cleanup.md](references/evidence-and-cleanup.md). Report command results, counts, database evidence, commit SHA, deployment ID/status/alias, runtime observations, and any unverified layer.

Restore test media and temporary callback/environment configuration. Do not delete rows, objects, deployments, or secrets merely to make the report clean; use the supported lifecycle and obtain authority for destructive cleanup.
