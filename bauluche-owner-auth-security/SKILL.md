---
name: bauluche-owner-auth-security
description: Use when changing, debugging, or auditing the Jangseong Bauluche owner-only administrator, Supabase magic-link request or callback, login/logout, admin page guard, admin API authorization, session refresh, CSRF Origin checks, auth cookies, rate-limit state, cache headers, forged identity headers, or authentication error responses.
---

# Bauluche Owner Auth Security

Preserve a single-owner, server-decided identity. A Supabase session proves authentication; the configured owner email decides authorization.

## Keep the identity server-owned

1. Read the owner only from server configuration `ADMIN_EMAIL`.
2. Never accept a login email, owner email, redirect destination, allowlist, or identity header from the browser.
3. Request a magic link only for the configured owner and the fixed `/auth/callback` URL. The current bootstrap contract uses `shouldCreateUser: true`; do not change account-provisioning semantics without an explicit migration decision.
4. At every authorization boundary, call Supabase `auth.getUser()` and compare the verified email with `ADMIN_EMAIL` after trim and lowercase normalization.
5. Fail closed when the user, verified email, or configured owner is missing.

Read [owner-flow.md](references/owner-flow.md) before changing login, callback, logout, cookies, or proxy behavior.

## Authorize each boundary

The proxy refreshes sessions; it does not grant administrator access. Protect the admin page and every `app/api/admin/**` route with the centralized guard before reading a mutation body, opening privileged database/storage clients, or signing an upload.

Apply [boundary-contract.md](references/boundary-contract.md):

- anonymous API: `401`;
- verified non-owner API: generic `403`;
- anonymous page: redirect to `/admin/login`;
- verified non-owner page: forbidden;
- every state-changing request: exact configured Origin;
- every admin/auth response: `private, no-store`.

Ignore legacy Sites identity headers. Never expose the owner address, tokens, callback credentials, Supabase/provider errors, SQL, storage paths, project identifiers, or secret/config values.

## Verify three identities

Use [verification.md](references/verification.md). Test anonymous, verified owner, and verified non-owner on every new or changed route. Add a failing regression test before altering policy. Confirm callback mismatch signs out, login ignores submitted email, forged headers fail, Origin comparison is exact, cookies remain secure, and all public errors are fixed and generic.
