# Landing page — design system & section anatomy

This is the engine behind the `landing-page` skill: a proven one-page marketing site structure,
originally specified for a roofing company and generalized here so it works for any local
business (restaurant, dental clinic, law firm, gym, agency, contractor, SaaS, etc.). The
**structure and interaction mechanics are invariant** — keep them exactly as specified regardless
of industry. The **tokens (colors, copy, imagery, stats)** are what change per client, filled in
from the Step 1-3 interview in SKILL.md.

A full worked example (the original roofing brief this was extracted from) is in
`references/example-roofing-brief.md` — read it once to calibrate the level of detail and polish
expected; don't copy its roofing-specific content into an unrelated business.

---

## Tech (invariant)

- Single `index.html`. No build step, no framework, no bundler.
- Styling: Tailwind via the CDN script tag (`<script src="https://cdn.tailwindcss.com">`) *or*
  plain CSS in a `<style>` block — pick whichever is faster for the specific layout, but don't mix
  a partial Tailwind setup with a partial custom one.
- Fonts: Google Fonts via `<link>` tag. Default pairing — a confident sans-serif at 500/600 weight
  for everything, plus a monospace at 400 weight for small uppercase labels (e.g. Plus Jakarta Sans
  + DM Mono, or an equivalent pair if the brand already has font preferences). Load only the
  weights actually used.
- Interactions in vanilla JS, no dependencies:
  - Scroll-triggered reveals: fade + 20px rise, ~0.6s ease-out, staggered per child, via
    `IntersectionObserver`.
  - Count-up animation on the stat numbers when they scroll into view.
  - Infinite marquee (logos strip, testimonials) via CSS animation (`@keyframes` translating a
    duplicated track) — pause on hover for the testimonials marquee.
  - Accordion (FAQ) with a smooth `max-height`/grid-template-rows transition, not an abrupt
    show/hide.
- Imagery: Unsplash photo URLs (`https://images.unsplash.com/...`), chosen per section to match
  the client's actual business — never reuse the roofing example's photo subjects for an unrelated
  industry. Pick search terms from what the client described in the interview (e.g. a dental
  clinic → "dentist office interior", "dental checkup", "smiling patient"; a restaurant → "chef
  plating dish", "restaurant interior warm lighting", "table with food close-up").
- Desktop-first, fully responsive. Navbar collapses to a hamburger + slide-down panel under 900px.

## Design tokens (variable per client — pick or derive one direction, don't mix)

Four starting "moods". Offer these as buttons in Step 2 of SKILL.md if the client has no existing
brand colors; if they do have brand colors/a logo, derive an equivalent token set from their actual
colors instead of using one of these presets verbatim (keep the same *structure* — one dominant
surface, one accent, one light page background — just swap the hex values).

| Mood | Dominant surface | Accent | Light bg | Corners | Personality |
|---|---|---|---|---|---|
| **Bold oscuro editorial** | Near-black `#0D0D0D` / elevated `#262626` | Vivid spring-green `#2BD47D` (light `#34F491`, deep gradient stop `#082B19`) | `#FAFAFA` / section `#EDEDED` | `0px` everywhere except chips (~10px) and avatars (circle) | Premium, confident, high-contrast trades/B2B |
| **Cálido y cercano** | Warm off-white `#FBF4EC` / cards `#FFFFFF` | Terracotta `#E2692C` (light `#F08A53`, deep `#7A3112`) | `#F7EFE4` | `16px` cards, `999px` chips/buttons | Hospitality, wellness, family-oriented services |
| **Corporativo minimalista** | White `#FFFFFF` / cards `#F5F7FA` | Deep blue `#1C4ED8` (light `#4D7CFB`, deep `#0D2A7A`) | `#F5F7FA` | `8px` cards, `6px` buttons | Professional services, finance, B2B SaaS |
| **Vibrante y audaz** | Deep violet `#1A0B2E` / elevated `#2D1448` | Hot coral `#FF5A5F` + lime `#C6FF4D` as secondary accent | `#FFFBF2` | `24px` cards, pill buttons | Creative agencies, fitness/boutique studios, youth brands |

Body text on dark surfaces: a light grey, never pure white (`#D9D9D9` on the dark-editorial mood;
derive an equivalent ~85% lightness grey for other dark-surface moods). Muted text on light
surfaces: a mid grey (~30% lightness), never pure black.

## Type scale (invariant ratios, font swappable)

- H1 (hero headline): 72px / weight 500 / letter-spacing −0.04em / line-height 1.05. Scale down to
  ~40-48px on mobile.
- Section H2: 40px / 600.
- Card title: 20-28px / 600.
- Body: 16px / 500.
- Micro-labels (eyebrows, tags, dates): monospace, 12px, uppercase, letter-spacing ~0.08em, in the
  accent color when on a dark surface.

## Shape language

- Corner radius is whatever the chosen mood specifies — apply it **everywhere** (cards, images,
  buttons) except the small exceptions the mood allows (chips/pills, avatar circles). This
  consistency is the signature of the design; don't round some cards and not others.
- Buttons: solid rectangle/pill (per mood) in the accent color with dark text, or in the dominant
  dark/light surface color with contrasting text — plus an attached icon tile on the trailing edge
  holding a ↗ arrow, in the inverse colour pairing. Hover: swap the two colours.
- Eyebrow label: a small pill in a neutral light tone, containing a tiny bullet/dot + the section
  word ("About", "Services", "Why us", "Reviews", "Blog", "FAQ") — translate these section words to
  match the client's working language.

## Layout

Max content width ~1240px, generous vertical section padding (~140px desktop, ~72px mobile).

---

## Sections, top to bottom (invariant structure, variable content)

### 1. Sticky navbar
Light bar, full width. Left: lowercase wordmark (or the client's actual logo image if they have
one) — if text, a stylised distinguishing glyph as the final character is a nice signature touch
but optional. Centre: 3-4 nav links matching the sections actually built (e.g. About · Services ·
Blog · Contact — drop Blog if the client skipped that section). Right: accent-colored CTA button
with the arrow tile, using the CTA verb decided in the interview (e.g. "Get in touch", "Book a
table", "Get a quote", "Schedule a visit"). Collapses to hamburger + slide-down panel under 900px.

### 2. Hero
Full-bleed photo relevant to the business, ~90vh, dark gradient scrim fading from one side. Left
column: a small pill badge with an accent dot (a short hook relevant to the business — "Free
inspections", "Reservations open", "New patients welcome" — ask what fits), a 3-line headline (72px)
about the core value proposition, a 2-3 line supporting paragraph, and the CTA button. Right
column: 2-3 stacked frosted-glass trust cards (`rgba(surface, 0.45)` + backdrop-blur, hairline
border), each a small accent icon + bold title + one line of body — content from the
differentiators gathered in Step 3 (e.g. "Licensed & Insured", "24/7 Emergency Service", "5-Star
Rated"). Along the bottom edge, an optional infinite marquee of low-opacity placeholder client/
partner logos — omit if the client has no partner logos to show and doesn't want generic
placeholders.

### 3. About
Two columns. One side: a photo with 1-2 overlaid translucent stat blocks — a big number + unit in
the accent color, with a short caption beneath (e.g. "15 years of experience", "2,000+ clients
served" — use the client's real stats from Step 3, never invent a precise number in production
mode). Animate the numbers counting up on scroll. Other side: eyebrow pill, a two-line 40px
heading, a short paragraph about the business's story/mission, and a secondary button ("About us"
or similar, linking to a fuller about page if one exists, otherwise just an anchor/no-op).

### 4. Services
Split header: eyebrow + large two-line heading on one side, a short paragraph + "All services"
button on the other. Below, a grid of cards (2×2 for 4 services, or adjust the grid for however
many the client has — 3 or 5-6 also work, just keep the grid balanced). Each card: a horizontal
split with a photo on one half and a small translucent icon tile pinned to its corner, and on the
other half a title, a 2-3 line description, and a hairline-divided monospace category tag at the
bottom. Hover: image zooms ~1.05 over 600ms. Use the client's actual service list from Step 3.

### 5. Why us (bento grid)
Centred eyebrow + centred 40px heading first. Four tiles in a 2-row bento layout:
- A tall accent-gradient tile: a huge stat number in a contrasting color (years in business,
  rating, or another headline number not already used in About), with a small supporting graphic
  (a badge/certificate motif works well) and a title + caption at the bottom.
- A dark/light tile with a photo on one side and 2-3 accent check-circle bullets on the other
  (licensing/certifications/guarantees — whatever credentials the business actually has), plus a
  CTA button.
- A tile with a second huge stat (a percentage works well — satisfaction rate, retention, on-time
  rate — whatever is true and relevant) and a subtle accent gradient bleeding in from one edge.
- A tile with a circular certification/award badge emblem (if the client has a real
  certification/award to show) and a title + caption. If there's no real badge to show, replace
  this fourth tile with another genuine differentiator instead of fabricating a credential.

### 6. Reviews
Centred eyebrow + heading. Two infinite marquee rows of testimonial cards scrolling in opposite
directions, the whole block rotated about −3° so the rows bleed off both edges on a slight
diagonal. Each card: surface-colored, avatar circle + name + monospace role/location, a row of
accent-colored stars, and a 2-3 line quote. Pause on hover. Use real testimonials if the client
provided them; in demo mode, plausible placeholder ones are fine but say so clearly in chat (never
inside the HTML) so nobody mistakes them for real reviews before the site goes live.

### 7. Blog
Eyebrow, 40px heading, paragraph, and a "View all posts" button. Below: an asymmetric layout — one
larger featured card (tall image) and 2 smaller stacked cards alongside it. Each: image, a small
monospace date chip, a title, and a "Read more →" link whose arrow slides right on hover. Skip this
section entirely if the client has no blog/content plans — don't force it in.

### 8. FAQ
Centred eyebrow + 40px heading, then a stack of full-width accordion rows. Closed: question text +
a thin accent "+". Open: icon becomes "×", the answer expands with a smooth height transition.
First item open by default. Use the client's real FAQs if given; otherwise draft plausible ones for
the stated industry (standard questions a prospective customer would actually ask).

### 9. Footer
Full-bleed dominant-surface color. One side: an oversized wordmark/logo, a 1-2 line tagline, small
social chips with leading icons for whichever platforms the client actually uses (don't invent
social presence they don't have), and the CTA button. Middle: "Our contact" with chips for
location, phone, email — each with a small accent icon — using the client's real contact info.
Other side: a "Pages" link list in 1-2 sub-columns. Hairline divider, then a bottom bar: copyright
left, a small credit line right.

---

## Accessibility (invariant, non-negotiable)

- Visible focus rings on every interactive element (don't suppress the default outline without
  replacing it with an equally visible one).
- `prefers-reduced-motion: reduce` disables marquees (freeze the track) and scroll reveals (content
  renders in its final state immediately, no fade/rise).
- Semantic landmarks (`<nav>`, `<main>`, `<header>` inside hero if appropriate, `<footer>`) and
  heading hierarchy that actually nests (one `h1`, `h2`s per section, no skipped levels).
- `alt` text on every image, written from the actual photo content, not a generic filler.

## Copy discipline

- **Demo mode** (prospecting a not-yet-signed client): plausible placeholder copy for anything the
  client didn't supply — testimonials, stats, FAQs, blog titles — is acceptable, since the
  deliverable is a visual mockup to win the business, not a live production site. Tell the user in
  chat which pieces are placeholder so they remember to swap them before it ever goes live.
- **Production mode** (confirmed client): never fabricate testimonials, statistics, certifications,
  license numbers, or specific legal/medical/financial claims. Where the interview left a gap, write
  a visible `[COMPLETAR]` placeholder in that spot instead of inventing something plausible-sounding
  — same discipline as this plugin's other client-facing skills.
- In both modes: generic, non-specific phrasing ("Licensed & insured", "Family owned and operated")
  is fine to draft even without the client confirming the exact wording: it's not a fabricated fact.
  A specific number, date, license ID, or named certification is a fact and needs a real source.
