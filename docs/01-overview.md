# Overview

Viscraft is an India-based visa and travel services business serving Indian customers, with two enquiry-led service lines:

**A) Visa application support** — document assembly/review, cover letter preparation, employment NOC drafting, pre-submission financial review, plus the flight/hotel/itinerary components an application requires.

**B) Bespoke travel planning** — tailored itineraries, flights, accommodation, ground arrangements.

Nine visa corridors: Schengen, UK, Ireland, USA, Canada, Australia, New Zealand, China, Japan. See [`03-cms-pricing-spec.md`](03-cms-pricing-spec.md) for the country-vs-corridor structure decision that refines this.

## The site is a trust-and-qualification funnel, not a store

No catalogue, no fixed departures, nothing directly bookable. Conversion = form submission, WhatsApp message, or phone call. Anything that looks purchasable creates a promise the business doesn't make.

## Two audiences, opposite emotional states, one brand

- **Visa customers**: anxious, often post-refusal, deadline-driven, deciding fast. Tone: clean, structured, calm, precise.
- **Travel customers**: excited, browsing months ahead, deciding slowly. Tone: warm, atmospheric, confident.
- Shared typography/logo/core palette; differentiated photography and accent treatment per audience.
- The homepage's only job is routing correctly in ~5 seconds — build it LAST.

## Two positioning differentiators

These produce the binding rules in [`02-copy-constraints.md`](02-copy-constraints.md):

- **Verifiability**: the Indian visa consultancy market has a real fraud problem; customers actively screen for it (GSTIN, CIN on MCA21, domain age, stock-photo red flags). The footer on every page carries entity name, CIN, GSTIN, office address, phone, and grievance officer — the footer is a conversion asset, not boilerplate.
- **Stated honesty**: cover letters, NOC drafting, and financial review are legitimate services and also the exact words fraudulent operators use for fabricated documents. A plainly stated "What we won't do" block is likely the highest-converting copy on the site — prominent on `/visa-support`, referenced from the homepage.

## Cross-sell

Someone who just got a visa still needs an itinerary, hotels, and transport — the highest-quality travel lead available. Built into the structure: the end of the visa journey presents travel planning as a genuine continuation, not a banner.

## WhatsApp

Primary channel, not secondary. Floating button on every page, dominant on the visa branch, prefilled with context from the originating page.

## Build order

(Wireframe review now precedes step 1 in practice — see [`04-decisions-log.md`](04-decisions-log.md).)

1. `/visa-support` (highest-urgency traffic)
2. `/enquiry/visa`
3. Visa Guides CMS + 2 sample guides (Schengen, UK)
4. `/about`, `/fees`, `/grievance`, `/contact`, `/faq`
5. `/travel-planning` + `/enquiry/travel`
6. Trips CMS, Resources CMS, Testimonials CMS
7. `/journal`
8. Legal pages + 404
9. Homepage

## Technical constraints

Framer Pro, one project, no code export (deliberate lock-in), mobile-first (mid-range Android on variable 4G is the baseline device — compress every image), English only for now (Hindi later consideration), JSON-LD (TravelAgency site-wide, FAQPage/HowTo/BreadcrumbList as applicable), unique meta title/description per page, clean slugs (no parameterised URLs), work on a branch and never publish to live. Full access details in [`07-tech-access.md`](07-tech-access.md).

## Never invent

Entity name, CIN, GSTIN, office address, phone, grievance officer name, testimonials, trip case studies, success figures, or any credential. Placeholder these and track them — see [`06-placeholders.md`](06-placeholders.md).
