# Worked example — the original brief this design system was extracted from

This is the original, industry-specific prompt (for a roofing company) that `references/
design-system.md` was generalized from. It's kept here as a calibration reference for the level of
detail and polish expected — **read it to understand the bar, never copy its roofing-specific
content (photo subjects, service names, stats like "900 roofs") into an unrelated business.**

---

Build a single-page marketing website for a professional roofing company. Modern, high-contrast,
editorial-industrial: near-black surfaces, a vivid spring-green accent, sharp 0px corners
everywhere, large photography, and small monospace labels. Desktop-first but fully responsive.

**Tech:** Single `index.html` with Tailwind (CDN) or plain CSS — no build step required. Fonts from
Google Fonts: Plus Jakarta Sans (500, 600) for everything, DM Mono (400) for small labels.
Scroll-triggered reveals (fade + 20px rise, ~0.6s ease-out, staggered) via `IntersectionObserver`.
Unsplash photo URLs for imagery (roofers on roofs, shingle/tile/metal roofs, storm damage,
warehouses, suburban houses).

**Design tokens:** Ink/card black `#0D0D0D`, elevated black `#262626`, accent green `#2BD47D`
(light `#34F491`, deep gradient stops `#115532`/`#082B19`), page light `#FAFAFA` / section light
`#EDEDED`, body text on dark `#D9D9D9`, muted text on light `#4D4D4D`.

**Type scale:** H1 72px/500/−0.04em/1.05. Section H2 40px/600. Card title 20-28px/600. Body
16px/500. Micro-labels: DM Mono 12px, uppercase, ~0.08em, green on dark.

Border radius is 0 everywhere except small chips/pills (≈10px) and avatar circles — this squareness
is the signature of the design, don't round the cards. Buttons: solid rectangle (green with black
text, or black with white text) + an attached square icon tile on the right holding a ↗ arrow, in
the inverse colour; hover swaps the two colours. Eyebrow label: a small light-grey pill with a tiny
black square bullet + the section word. Layout: max content width ~1240px, ~140px vertical section
padding.

**Sections, top to bottom:**

1. **Sticky navbar** — light bar, full width. Left: lowercase wordmark with a stylised © as the
   final character. Centre: About · Services · Blog · Contact. Right: green "Get in touch" button
   with the arrow tile. Collapses to a hamburger + slide-down panel under 900px.
2. **Hero** — full-bleed photo (roofers on a steep roof against blue sky), ~90vh, dark gradient
   scrim from the left. Left column: dark pill badge with a green dot ("Free roof inspections"), a
   3-line 72px headline about protecting what matters most, a 3-line supporting paragraph, and the
   green CTA. Right column: three stacked frosted-glass cards (rgba(13,13,13,0.45) + backdrop-blur,
   1px white-10% border), each a small green icon + bold title + two lines of body — Storm Damage
   Response / Licensed & Insured / 5-Star Rated Service. Bottom edge: infinite marquee of white
   30%-opacity placeholder client logos.
3. **About** — two columns. Left: a photo with two overlaid dark translucent stat blocks — a big
   number + "+" in green, two-line caption beneath ("15 Years of experience", "900 Roofs repaired &
   replaced"); numbers count up on scroll. Right: eyebrow pill, 40px two-line heading, a short
   paragraph, and a black "About us" button.
4. **Services** — split header: eyebrow + large two-line heading left, short paragraph + "All
   services" button right. Below, a 2×2 grid of black cards, each a horizontal split: photo on the
   left half with a small translucent icon tile pinned to its bottom-left corner, and on the right
   a 20px white title, 3-line grey description, and a hairline divider with a green DM Mono
   category tag. Services: Storm Damage & Insurance, Roof Repair, Roof Replacement, Flat &
   Commercial Roofing. Hover: image zooms ~1.05 over 600ms.
5. **Why us** (bento grid) — centred eyebrow + heading first, then four tiles in two rows: (a) a
   tall green-gradient tile with a huge "10y" in white, a floating warranty-certificate graphic, and
   a title + caption; (b) a black tile with a photo on the left and three green check-circle
   bullets (licensed/bonded/insured, 15+ years, 900+ roofs) plus a "Get in touch" button; (c) a
   black tile with a huge "98" + "%" and a subtle striped green gradient; (d) a black tile with a
   circular certification badge emblem and a title + caption.
6. **Reviews** — centred eyebrow + heading, two infinite marquee rows of testimonial cards
   scrolling in opposite directions, the whole block rotated about −3°. Each card: black, avatar +
   name + DM Mono role/location, a row of green stars, a 3-line quote. Pause on hover.
7. **Blog** — eyebrow, 40px heading, paragraph, "View all posts" button. Below: one large featured
   card (tall image) left and two smaller stacked cards right. Each: image, grey date chip (DM
   Mono), 20px title, "Read more →" link that slides its arrow right on hover.
8. **FAQ** — centred eyebrow + 40px heading, full-width black accordion rows. Closed: white
   question + thin green "+". Open: icon becomes "×", grey answer expands with a smooth height
   transition. First item open by default.
9. **Footer** — full-bleed `#0D0D0D`. Left: oversized wordmark (~100px) with the © as a large green
   outlined circle, a two-line tagline, small dark social chips (Instagram, LinkedIn, Facebook),
   and the green "Get in touch" button. Middle: "Our Contact" — three dark chips (location, phone,
   email) each with a small green icon. Right: "Pages" as two sub-columns of links. Hairline
   divider, then a bottom bar: copyright left, credit line right.

**Notes:** Write your own plausible copy — headline about protecting homes, service descriptions,
six testimonials from homeowners/property managers in different neighbourhoods, three blog titles,
four FAQs. Keep the alternating rhythm: light page background, with services/why/reviews cards and
the footer as black blocks. Accessibility: visible focus rings, prefers-reduced-motion disables
marquees and reveals, semantic landmarks, alt text on every image.
