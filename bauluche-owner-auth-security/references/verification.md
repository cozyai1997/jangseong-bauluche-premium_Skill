# Verification

## Primary code

- `app/auth/admin-policy.ts`
- `app/auth/admin.server.ts`
- `app/auth/service.server.ts`
- `app/supabase/server.ts`
- `app/supabase/proxy.ts`
- root `proxy.ts`
- auth route modules and admin pages
- every `app/api/admin/**/route.ts`
- shared media API handlers

## Automated evidence

Run the current equivalents of:

- `tests/admin-policy.test.mjs`
- `tests/admin-auth.test.ts`
- `tests/auth-flow.test.ts`
- proxy/session tests
- every affected admin API test
- client-bundle secret scan
- type checking, lint, render tests, and `npm run build:vercel`

Assert:

1. login ignores a submitted email and sends only to configured ownership;
2. wrong method and cross-Origin login fail before Auth calls;
3. provider messages never appear in responses;
4. valid code and valid email token hash complete cleanly;
5. missing, malformed, expired, or rejected callback input yields retry;
6. verified non-owner callback signs out and never reaches admin;
7. anonymous/non-owner/owner results are correct for pages and APIs;
8. forged Sites headers cannot change authorization;
9. normalized equality works and empty configuration fails closed;
10. logout is POST-only and exact-Origin checked;
11. cookie flags and refresh propagation remain safe;
12. all responses are `private, no-store`;
13. route inventory finds no unguarded admin API;
14. response/client scans contain no owner identity, token, cookie, provider message, or server secret.

In a safe production acceptance pass, verify anonymous redirect, owner magic-link login, callback, logout, forged-header rejection, and direct anonymous API denial without printing the address or link.
