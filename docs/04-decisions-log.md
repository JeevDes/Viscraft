# Decisions log

Append-only, dated record of everything decided (or explicitly deferred) in conversation with the business owner, so nobody has to re-derive it. Append a new dated entry whenever a real decision gets made — not to restate the brief in `01-overview.md`.

If an entry here conflicts with something decided later, the newer decision wins — update this file, don't just note the conflict.

## 2026-09-14

- **Entity/compliance details** (legal entity name, CIN, GSTIN, office address, grievance officer name/contact): use placeholders throughout (e.g. `[[CIN — TO SUPPLY]]`). See [`06-placeholders.md`](06-placeholders.md).
- **WhatsApp number**: placeholder for now.
- **Pricing structure**: one range per tier, not per corridor — see [`03-cms-pricing-spec.md`](03-cms-pricing-spec.md) for the full model including the promo layer and the parked fee-scraper idea.
- **Site structure**: organized by country, not corridor (Schengen is a corridor shared by many countries, e.g. France) — see [`03-cms-pricing-spec.md`](03-cms-pricing-spec.md).
- **Enquiry form placement**: short "quick start" capture (3–4 fields: destination/country, visa type, urgency) embedded on `/visa-support`, deep-linking pre-filled into the full `/enquiry/visa` form for the remaining qualifying fields (refusal history, employment status, etc.), rather than duplicating the full ~9-field form in both places. Rationale: an anxious, fast-deciding visa visitor shouldn't face a full qualifying form on a trust-building landing page; avoids maintaining two copies of a long form. Confirmed by the business owner.
- **Work sequencing amendment**: start with wireframe review (business owner has existing wireframes to be critiqued/improved/revised) before building `/visa-support`, ahead of the original brief's build order. Wireframes to be added to this repo (not yet pushed as of this date).
- **Version control / collaboration**: a second developer is working on this project independently via Claude CLI, sharing this GitHub repo. Pushes/merges from either side land on the shared remote and are visible to both; pulls are not automatic — fetch/pull explicitly each session. Suggested (not yet confirmed) that each person work on their own branch rather than committing straight to `main`. Unclear/unconfirmed whether this repo is meant to hold only wireframes/docs or more — the Framer site itself is version-controlled separately via Framer's own project-level branching, not via this repo.

## Still open / not yet answered

- "What we won't do" block copy — to be drafted from the fraud-marker language in `02-copy-constraints.md` for business-owner review; not yet drafted.
- Country-level page treatment (which countries get built/featured first, beyond the Schengen + UK sample guides) — not yet discussed under the new country-first framing.
- Whether this docs folder should be the single source of truth for both collaborators, or whether each side is also keeping separate private notes — worth confirming explicitly.
