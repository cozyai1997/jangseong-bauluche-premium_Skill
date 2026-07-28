# Owner flow

## Magic-link request

- Accept POST only.
- Require `Origin` to equal `NEXT_PUBLIC_SITE_URL`'s origin exactly, including scheme, host, and port.
- Ignore any body email or redirect.
- Call Supabase OTP for `ADMIN_EMAIL` only.
- Use the fixed absolute `/auth/callback` URL.
- Keep the current `shouldCreateUser: true` behavior unless owner provisioning is deliberately redesigned.
- Redirect with 303 and `private, no-store`.
- Map provider rate limiting to the bounded public rate-limit state; map all other failures to a generic retry state. Never forward a provider message.

## Callback

Accept either:

- a PKCE `code`; or
- `token_hash` with `type=email`.

Reject missing or mismatched inputs with a clean retry redirect. After exchange or verification, call `auth.getUser()` and run the same normalized owner policy used everywhere else. Sign out on verification failure, missing user, or non-owner. Redirect the verified owner to `/admin`; never accept arbitrary `next` or retain tokens in the final URL.

## Session and logout

Use a fresh request-scoped Supabase server client. Cookies are HttpOnly, SameSite=Lax, path `/`, and Secure in production. Preserve the attributes Supabase needs during proxy refresh.

Logout is POST-only, exact-Origin checked, and redirects to a fixed signed-out login state. Ignore sign-out provider detail in the public response.

The root proxy matcher covers `/admin/**`, `/api/admin/**`, and `/auth/**` for session refresh and private caching. Every protected page/API still performs its own authorization.
