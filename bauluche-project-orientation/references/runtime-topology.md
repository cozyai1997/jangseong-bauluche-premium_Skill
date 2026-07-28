# Runtime topology

## Canonical production path

- Public and admin application: Next.js 16 on Vercel, Seoul region `icn1`.
- Production build: `npm run build:vercel`.
- Authentication: Supabase magic-link session, restricted server-side to the one address configured in `ADMIN_EMAIL`.
- Data: Supabase Postgres for immutable media slots, versions, and upload stages.
- Assets: public Supabase Storage bucket `bauluche-media`.
- Upload transport: the browser sends bytes directly to the signed Supabase TUS endpoint; Vercel handles only prepare and complete control requests.
- Public manifest: resolve every one of the 19 slots or fall back to the complete set of 19 committed defaults. Never render a mixed manifest.

## Production identifiers

- Site origin: `https://jangseong-bauluche-premium.vercel.app`
- Supabase project reference: `deawvlkozxxyfymijdlw`
- Auth callback path: `/auth/callback`

Treat these as non-secret identifiers, but verify them against live configuration before a production operation. Never infer a team or project ID from a URL.

## Environment contract

Use names only:

- `NEXT_PUBLIC_SUPABASE_URL`
- `NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY`
- `SUPABASE_SECRET_KEY`
- `ADMIN_EMAIL`
- `NEXT_PUBLIC_SITE_URL`

Only the publishable key is client-safe. Do not print or commit any value or the literal owner email.

## Retained legacy path

`.openai/hosting.json`, `vite.config.ts`, `worker/`, `db/`, `drizzle/`, Cloudflare D1/R2 bindings, `ADMIN_EMAILS`, and vinext commands belong to the earlier Sites/Cloudflare path. Preserve them unless removal is explicitly requested. They do not define the active administrator runtime.

`supabase/config.toml` may contain a local CLI label rather than the production project reference. Historical `docs/superpowers` plans explain past decisions but are not live deployment runbooks.
