# Boundary contract

## Trust order

1. Create a request-scoped publishable-key Supabase server client.
2. Call `auth.getUser()` to obtain a server-verified user.
3. Normalize the verified email and configured `ADMIN_EMAIL` with trim and lowercase.
4. Require exact equality.
5. Only then parse or act on protected input and create any privileged runtime.

Do not trust browser form fields, query parameters, user-supplied redirect URLs, unverified JWT payloads, user metadata, client state, or `oai-authenticated-user-*` headers.

## Page behavior

- Anonymous `/admin`: redirect to `/admin/login`.
- Verified owner: render the private administrator.
- Verified non-owner or unusable owner configuration: forbidden.

## API behavior

- Anonymous: `401` with stable code `UNAUTHENTICATED`.
- Verified non-owner: `403` with stable code `FORBIDDEN` and a generic message.
- Keep validation, missing resource, revision conflict, and service failure mappings separate from auth decisions.
- Do not reveal whether a particular email is allowed.

Every response, including success, redirect, and error, must remain private and non-cacheable.

## Mutation Origin

Require exact Origin on login, logout, upload prepare/complete, metadata edits, restore, and every other admin mutation. Missing Origin, `null`, subdomain variations, alternate ports, and lookalike suffixes fail.

Origin is CSRF defense, not authentication. Apply both Origin and verified-owner checks.

## Error hygiene

Return fixed public codes/messages. Never include:

- the configured owner identity;
- magic-link code, token hash, access/refresh token, or cookie;
- provider error text;
- secret or publishable key values;
- database SQL or internal stack;
- bucket, object, staging, or project internals not required by the public contract.
