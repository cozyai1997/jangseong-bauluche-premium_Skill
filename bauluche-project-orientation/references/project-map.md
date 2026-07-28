# Project map

Use current source and tests as authority. Confirm paths still exist before editing.

| Concern | Primary code | Primary evidence |
|---|---|---|
| Intro and hero match cut | `app/components/CinematicIntro.tsx`, `HeroSection.tsx`, `IntroGateScript.tsx`, `app/intro-state.mjs`, `app/cinematic-intro.css`, `app/globals.css` | cinematic intro, render, and public-media tests |
| Development evidence | `app/components/DevelopmentSection.tsx`, `app/development-projects.mjs`, development styles | development project, accessibility, and render tests |
| Unit plans | unit-plan section components, catalog entries, plan assets | unit-plan and asset-dimension tests |
| Managed-media catalog | `app/media/catalog.mjs`, `types.ts`, `manifest.server.ts`, `ManagedImage.tsx` | media catalog, manifest, and render tests |
| Admin editor | `app/admin/AdminMediaManager.tsx`, `MediaEditorDialog.tsx`, `admin-state.mjs` | admin render and interaction tests |
| Owner authentication | `app/auth/admin.server.ts`, `admin-policy.ts`, `service.server.ts`, `app/supabase/server.ts`, `app/supabase/proxy.ts` | admin policy, auth flow, and admin auth tests |
| Upload APIs | `app/api/admin/media/**`, `app/media/api-handlers.server.ts` | media API tests |
| Direct TUS upload | `app/media/direct-upload.client.ts`, `storage.supabase.server.ts`, `service.supabase.server.ts` | direct-upload and Supabase service tests |
| Media persistence | `repository.supabase.server.ts`, `manifest.server.ts`, `supabase/migrations/**` | repository tests and Supabase database tests |
| Deployment | `next.config.ts`, `vercel.json`, `package.json`, environment names | Vercel build, render tests, runtime logs |

Search by symbol when a listed filename moved. Preserve unrelated dirty changes.
