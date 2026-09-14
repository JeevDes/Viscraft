# CMS & pricing spec

Update this file as the CMS is actually built in Framer — it currently reflects the original brief plus one structural correction, not the final built schema.

## Structure decision — country, not corridor (2026-09-14)

The site organizes pages by **country**, not by corridor. A corridor (e.g. Schengen) is a shared visa type used by multiple countries (e.g. France, Germany, Italy...); each member country still likely needs its own page (own VAC location, appointment quirks, possibly fee nuances) even though the visa process/fee is common across the corridor.

**Why**: the original brief's Visa Guides schema had "Corridor" as a field on a corridor-level guide. This was corrected — country is the primary page unit, corridor becomes a grouping/shared-content attribute.

**How to apply**: when building the Visa Guides CMS (build order step 3), design country as the slug/primary unit with corridor as a reference/grouping field, and work out what content is shared at the corridor level vs. overridden per country. Not yet fully designed.

## Original CMS schema (per brief, to be adapted per the decision above)

**Visa Guides** (highest-value pages on the site): Title, Slug, Corridor, Visa type, Applicant profile (Simple/Moderate/Complex), Overview, Eligibility, Required documents (rich text), Processing time, Official fee (local currency), Official fee (INR), Fee as-at date, Official source URL, Appointment reality, Common refusal reasons, How Viscraft helps, Last reviewed (date), SEO title, SEO description. Every guide must display Last reviewed, link to the official source, and carry a standing line telling readers to confirm current requirements with the official authority.

**Resources**: Title, Slug, Category, Body, Related visa guide (relational), Download asset, Last reviewed.

**Trips** (case studies, NOT products — no price field, no booking CTA): Title, Slug, Destination, Duration, Traveller type, Season, Hero image, Gallery, The brief, What we planned, Why these choices, Client quote, Featured.

**Testimonials**: Name, City, Service line, Quote, Outcome, Photo, Date.

Note: Framer's relational CMS fields (Pro feature) are one-directional per collection with some item-count/display limits in components — not identical to a true relational DB. Design around this when building relations (e.g. Resources → Related visa guide).

## Pricing model

GST-inclusive, driven by corridor tier × applicant profile × delivery speed:

| Tier | Corridors | Range |
|---|---|---|
| Heavy | USA, UK, Schengen, Canada | ₹4,499 – ₹7,999 |
| Standard | Ireland, Australia, NZ, China | ₹3,999 – ₹6,999 |
| Light | Japan | ₹3,499 – ₹6,499 |

Confirmed 2026-09-14: **one price range per tier** (not per individual corridor within a tier), shown with a clear statement of what moves the price (applicant profile, proximity to travel). Consular/VAC fees are pass-throughs, shown separately, never blended into Viscraft's fee — bespoke pricing must not mean silent/opaque pricing, since opacity reads as concealment to a fraud-screening visitor.

**Promo layer** (decision 2026-09-14, not yet built): promos can override the tier price at corridor level or individual-country level (e.g. a Schengen-wide promo, or a France-only promo). Needs a data structure — promo price/discount, badge/label, start date, end date, scope (corridor or country) — to be designed when the pricing component is actually built.

**Live govt/VAC fee scraper** (raised 2026-09-14, deferred/parked): idea to run a daily scraper tracking official govt/visa/VAC/consular fees and auto-update the site as regulations change. Explicitly deferred by the business owner — not blocking current build.

**Why parked**: this is a separate infrastructure project outside Framer entirely (external scraper + hosting + a sync pipeline into Framer CMS via API) — Framer itself cannot run a scheduled scraper. Government sites change markup without notice and may block scrapers, so any implementation needs a staleness/fallback check regardless.

**How to apply**: until the scraper (or a manual update process) is resolved, treat Official fee / Fee as-at date fields as manually curated per the original CMS schema (Last reviewed + Official source URL + standing "confirm with official authority" line). Revisit the scraper as its own scoped project later.
