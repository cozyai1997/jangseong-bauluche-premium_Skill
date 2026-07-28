# Unit catalog expansion

The current presentation has four units and four managed slots: `unit.84a`, `unit.84b`, `unit.116c`, and `unit.116d`.

For a genuinely new unit:

1. Obtain an approved plan asset and verified unit facts.
2. Add one stable record to `unitTypes` in `app/content/home-content.ts`.
3. Add the immutable `unit.*` slot to `app/media/catalog.mjs` with:
   - unit group and human label;
   - factual description and alt;
   - committed default path;
   - `contain` as the only allowed fit;
   - centered focal values;
   - actual default pixel dimensions.
4. Add the committed default asset and inspect its decoded dimensions.
5. Add the slot with a new forward Supabase seed migration so production has a matching immutable row. Never rewrite an already-applied migration.
6. Update generated/static media key types if they are not derived automatically.
7. Confirm the administrator group renders the new card, replace/settings/history/default restore work, and public manifest resolution includes it.
8. Update every fixed-count and expected-key test. The all-or-nothing public fallback total changes from 19 only when the catalog expansion is intentional and fully migrated.

Do not rename or reuse an existing slot to represent a different unit. Slot keys are durable identities referenced by database versions, storage paths, history, and administrator state.

The existing unit household counts total the published 70 homes. Do not append a fifth type until approved data explains the distribution and all affected project-summary copy is updated consistently.
