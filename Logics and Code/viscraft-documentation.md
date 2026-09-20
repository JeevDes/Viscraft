# Viscraft — Prototype Documentation

**File:** `viscraft-website.html` · ~95 KB · single self-contained page
**Companion:** `viscraft-mobile-preview.html` — the same site inside a 390px phone frame for reviewing mobile

Everything (markup, styles, script) lives in one file with no build step and no external
dependencies except the Poppins webfont. Open it directly in a browser, or drop it on any
static host.

---

## 1. How it is put together

It is a **single-page app**: all five pages exist in the markup at once and only one is
shown at a time. Navigation swaps which one is visible and updates the URL hash — no page
reloads, so it feels instant.

```
#home                      Home
#about                     About Us
#services                  Services
#blog                      Blog listing
#country/<slug>            Country page      e.g. #country/switzerland
#post/<slug>               Blog post         e.g. #post/schengen-visa-101
```

```
<head>
  <style>            all CSS, grouped by component then by breakpoint
<body>
  <template id="tpl-header">    header, cloned into every page
  <template id="tpl-footer">    footer, cloned into every page
  <main data-page="home">       one <main> per page; .active shows it
  <main data-page="about">
  <main data-page="services">
  <main data-page="country">
  <main data-page="blog">
  <main data-page="post">
  <script>           data, router, components, validation
```

The header and footer are defined **once** as `<template>` elements and cloned into each
page on load. Edit them in one place and every page updates.

---

## 2. Editing content

All copy that repeats or varies sits in plain arrays at the top of the `<script>`. Change
these rather than hunting through markup.

| Array | Holds | Currently |
|---|---|---|
| `COUNTRIES` | Search results + country page data (`slug`, `name`, `price`) | 8 |
| `HOME_CARDS` | Cards in the home carousel | 12 |
| `TESTIMONIALS` | Quotes (`quote`, `name`) | 5 |
| `TAGS` | Blog filter tags | 4 |
| `BLOG_POSTS` | Posts (`slug`, `title`, `subtitle`, `excerpt`, `tags`, `author`, `date`, `body`) | 8 |

Adding a country to `COUNTRIES` makes it searchable and gives it a working country page
immediately. Adding to `BLOG_POSTS` puts it in the listing, the home teaser and its own
post page, and it will be picked up by any tag filter it declares.

**One rule when adding carousel items:** keep `HOME_CARDS` and `BLOG_POSTS` at a multiple
of 4. The carousels page four cards at a time and loop endlessly; a count that isn't a
multiple of four drifts out of phase after a wrap.

Static copy — headings, the About Us body text, service descriptions, FAQs — is written
directly in the relevant `<main>` block.

---

## 3. Coverage against the logic sheet

All **69 rows** of `Website_Logics.xlsx` are implemented.

| Behaviour | How it works |
|---|---|
| Logo → refresh / redirect | Reloads on the current page, navigates home from elsewhere. Header and footer logos both. |
| Country search | Live filter over `COUNTRIES`; picking a result opens that country page |
| Services / Blog buttons | Reload when already on that page, otherwise navigate |
| Contact Us | Smooth-scrolls to the footer of the current page |
| Country / testimonial / blog carousels | Drag or swipe, plus arrow buttons; loop endlessly in both directions |
| Blog card → post | Opens `#post/<slug>` |
| Footer social / contact links | `wa.me`, `tel:`, `mailto:` and the social URLs |
| Country nav pane | Sticky to the top; jumps land at the **start** of each section, clear of the bar |
| FAQ accordion | Expands one question at a time, chevron rotates |
| Blog tag filter | Multi-select; empty selection shows everything |
| Consultation forms | Validated — see below |
| Services centrefold | Plane flies a runway as you scroll |

### Form validation

Runs on all three forms (Country, About Us, Services). Fields are checked when you leave
them and again on submit; errors clear as you correct them.

| Field | Accepts | Rejects |
|---|---|---|
| Name | Letters, spaces, apostrophes, hyphens (`Anne-Marie O'Brien`) | Empty, digits, symbols |
| Contact | 7–15 digits, with `+`, spaces, hyphens, brackets (`+91 98765 43210`) | Empty, letters, too short/long |
| Email | `name@domain.tld`, TLD of 2+ characters | Empty, malformed, `a@b`, `a@b.c` |

A blocked submit shows a red banner at the top of the form plus a message under each bad
field, and outlines those fields in red.

**Submissions currently go nowhere.** `form.reset()` runs and a success message shows. To
make it live, replace that branch with a POST to your endpoint — CRM, email service, or a
Google Sheet. This is the one piece that must be wired before launch.

---

## 4. Responsive behaviour

Breakpoints, largest first:

| Width | What changes |
|---|---|
| ≤1000px | Country page booking card narrows beside the documents |
| ≤900px | Services journey tightens its gutter and type |
| ≤820px | Booking card drops below the documents |
| ≤720px | **Mobile layer** — see below |
| ≤620px | Consultation form stacks to one column |
| ≤560px | Carousels become swipe-first; services journey stacks |

The mobile layer (≤720px) covers: a hamburger menu in place of the header links, a
collapsible footer, larger tap targets, carousel cards centred with the neighbours
peeking, two-up service pills and blog filters, and 16px form inputs (anything smaller
makes iOS zoom on focus).

On the Services page below 560px the cards stack and the runway becomes a rail down their
left, with the plane still descending it. The cards reorder so they read in journey
sequence — VISA → Itinerary → Travel Bookings → D-Day — rather than column by column.

Verified on iPhone SE (375px), iPhone 14 (390px) and Pixel 7 (412px), portrait and
landscape: no horizontal scrolling, no console errors.

---

## 5. Things worth knowing before extending it

**Carousel positions are measured, never assumed.** Card widths are fractional, so the
code reads each card's real position from the DOM instead of multiplying an estimated
width. Rounding or hardcoding those numbers reintroduces a drift that leaves cards
half-cut. The same applies to the Services flight path and the equal-height journey cards
— all measured on load and on resize.

**Careful with `padding` shorthand on `.wrap` elements.** `.wrap` supplies the page's side
gutters. Writing `padding: 0 0 40px` on an element that also has `.wrap` silently resets
those gutters to zero and the content runs to the screen edge. Set `padding-top` /
`padding-bottom` only. This bit three elements during the build.

**Anything hidden has no dimensions.** Inactive pages are `display:none`, so measuring
them returns zeros. Carousels and the flight path are re-measured when their page becomes
visible; keep that in mind if you add another measured component.

---

## 6. Still placeholder

Content that needs replacing before this is a real site:

- Phone numbers (`+91 1234567899`), `info@viscraft.co.in`, and the Instagram/Facebook URLs
- Card images — the home carousel and hero use grey blocks and outline watermarks
- Country page detail: the document lists, embassy addresses and FAQs are the same for
  every country. These need to become per-country data on `COUNTRIES`.
- Blog post bodies — one paragraph each
- Testimonials — the same quote repeated

---

## 7. Turning this into a production build

The prototype is deliberately one file so it can be reviewed without tooling. For a real
site:

1. **Split it up** — header/footer as components, one file per page, CSS into its own
   sheet. The `<template>` blocks map cleanly onto components in any framework.
2. **Move content to a CMS** — the five arrays in §2 are already shaped like API
   responses, so this is mostly a swap of source.
3. **Wire the forms** to a real endpoint (§3).
4. **Add per-route pages** for SEO. Hash routing keeps everything on one URL, which search
   engines won't index as separate pages — real paths (`/country/switzerland`) need server
   or framework routing.
5. **Optimise images** once real photography replaces the placeholders.

Points 3 and 4 are the two that genuinely block launch; the rest can be staged.
