---
name: landing-page
description: >
  Use this skill when the user wants to design or build a one-page marketing website / landing
  page for a business of any kind — trigger on phrases like "landing page", "necesito una página
  web para un cliente", "diseñame un sitio web", "armame la landing de [negocio]", "quiero vender
  páginas web a negocios locales", "build me a website for X", "hacé un mockup de sitio web para
  prospectar a un cliente", or any request to produce a single-page business website. Runs a
  structured interview to gather the business's basics, design direction, services, differentiators,
  testimonials and contact info, then builds a complete, self-contained `index.html` (Tailwind CDN
  or plain CSS, Google Fonts, vanilla-JS scroll reveals/marquees/accordion, Unsplash imagery)
  following a proven one-page structure (navbar, hero, about, services, why-us bento, reviews,
  blog, FAQ, footer), and verifies the result visually before delivering it. Works for any
  industry — restaurants, clinics, law firms, gyms, contractors, agencies, etc. — not just the
  roofing-company example this skill's design system was originally extracted from.
---

# Landing Page

Design and build a self-contained, one-page marketing website for a business. The deliverable is a
single `index.html` file the client can host anywhere — no backend, no build step, no framework.
This works for any industry: the interview adapts the copy, imagery, and design tokens to whatever
business the user describes; only the underlying section structure and interaction mechanics stay
fixed (that structure is what makes the result look professional and cohesive).

Read `references/design-system.md` in this skill directory once at the start — it has the full
technical spec (tech stack, design tokens per "mood", type scale, the 9-section anatomy with exact
interaction behaviors, accessibility requirements, and the copy-honesty rules for demo vs.
production mode). `references/example-roofing-brief.md` is the original worked example this system
was generalized from — read it once too, to calibrate the level of detail expected, but never
reuse its industry-specific content for an unrelated business.

## Step 1: Context and basics

Ask via buttons first: **"¿Para qué es este sitio?"**
- **"Estoy armando un demo para prospectar a un cliente nuevo"** → demo mode: plausible placeholder
  copy is fine where real content is missing, since the goal is a visual mockup to win the business.
- **"Es el sitio final de un cliente ya confirmado"** → production mode: no fabricated stats,
  testimonials, or credentials — missing pieces get a visible `[COMPLETAR]` instead (see the copy
  discipline rules in `references/design-system.md`).

Then gather, free text (can be answered together in one message if the user volunteers it all —
don't force one-by-one if they already gave you the details):
1. **Nombre del negocio** (used as the wordmark/title).
2. **Rubro / qué hace** (one line — e.g. "techado residencial", "restaurante de cocina peruana",
   "estudio jurídico de familia").
3. **Zona/ciudad que atiende**.
4. **¿Tiene logo o colores de marca definidos?** If yes, ask for the hex codes or to describe/paste
   the logo; this drives Step 2 instead of picking a preset mood.

## Step 2: Design direction

If the business has no existing brand colors, show the four mood presets from `references/
design-system.md` as buttons — **"Bold oscuro editorial"**, **"Cálido y cercano"**, **"Corporativo
minimalista"**, **"Vibrante y audaz"** — with a one-line description of each (dominant surface +
accent + personality fit) so the choice is informed, not a guess. If they have brand colors, derive
an equivalent token set from those colors instead (same structure: one dominant surface, one
accent, one light background) and confirm it back to the user in one line before moving on.

## Step 3: Content

Gather, in a few grouped turns (buttons for anything categorical, free text otherwise):

1. **Servicios/productos principales** — 3 to 6 offerings, each a name + one-sentence description.
   If the user is unsure and it's demo mode, offer to draft plausible ones for the stated industry
   and let them approve or edit before moving on.
2. **Diferenciadores y cifras clave** — 2-4 real standout numbers (years in business, clients
   served, satisfaction rate, certifications, completed jobs, rating) to feed the About and Why-us
   sections. In production mode these must be real; don't let the user skip this by proposing fake
   ones.
3. **Testimonios** — real ones to paste, or (demo mode only) draft plausible placeholder ones and
   say so clearly.
4. **Blog** — 3 real or plausible post titles, or skip the section entirely if the client has no
   blog plans.
5. **FAQ** — 4 real Q&As, or plausible ones for the stated industry if the client doesn't have a
   list ready.
6. **Contacto** — teléfono, email, dirección o zona de servicio, y qué redes sociales usa (no
   inventar presencia en redes que no tiene).
7. **CTA** — what should the main button say and do (e.g. "Get a quote", "Book a table", "Schedule
   a visit") — since this is a static file with no backend, the CTA should be a `mailto:`, `tel:`,
   or an anchor link to the contact section, not a form that submits anywhere; ask which fits.
8. **Fotografía** — ask what kind of photos fit each major section (hero, about, services); if the
   user doesn't have specific preferences, propose Unsplash search terms yourself based on the
   stated industry and confirm them in one line.

## Step 4: Build the site

Apply `references/design-system.md` precisely: the tech stack rules, the chosen mood's tokens (or
the derived brand tokens), the type scale, the shape language, and the full section-by-section
anatomy — substituting every piece of content gathered in Steps 1-3. Keep the structure invariant;
only the content, imagery, and color tokens vary.

Build one self-contained `index.html`:
- Tailwind via the CDN script tag, or plain CSS — no build step either way.
- Google Fonts via `<link>`, only the weights actually used.
- All interactions (scroll reveals, count-up stats, marquees, accordion) in vanilla JS, no
  dependencies.
- Images as hotlinked Unsplash URLs — don't download or embed them.
- Full accessibility per `references/design-system.md`: focus rings, `prefers-reduced-motion`
  handling, semantic landmarks, real `alt` text.

## Step 5: Verify visually before delivering

Don't deliver without looking at the rendered result. If a browser automation tool is available in
this environment (e.g. a pre-installed Playwright/Chromium), use it to:
1. Open the file and screenshot it at a desktop width (~1440px) and a mobile width (~390px).
2. Look at both screenshots: check the layout doesn't break, the hero and bento grid read
   correctly, the first FAQ item shows open, and nothing overlaps.
3. Emulate `prefers-reduced-motion: reduce` and confirm marquees/reveals don't block the content
   from being visible (static fallback state renders correctly).

If no browser automation is available in this environment, say so plainly to the user instead of
delivering unverified — at minimum confirm the HTML is well-formed and every referenced asset URL
is valid.

## Step 6: Deliver and iterate

Save as `index.html` in a folder named after the business in kebab-case (e.g.
`landing-acme-roofing/index.html`) and present it to the user. Give a one-line summary of what was
built (mood/tokens chosen, sections included, demo vs. production mode) — don't re-describe the
whole structure, that's what the file is for.

If demo mode, remind the user in chat (not in the file) which pieces are placeholder content that
must be replaced with real client data before the site ever goes live.

Offer to iterate: swap the mood/colors, rewrite a section's copy, add/remove a section, or regenerate
with different imagery — small, targeted edits to the existing file rather than rebuilding from
scratch each time.

## Notes

- One file only. Don't split into separate CSS/JS files or add a build step — that's the whole
  point of a quick, hostable-anywhere deliverable.
- Don't invent specific license numbers, named certifications, or legal/medical/financial claims in
  either mode — generic phrasing ("Licensed & insured") is fine to draft, a specific fabricated
  credential is not.
- If the client's industry doesn't fit a section (no blog, no social presence, no partner logos),
  drop that section/element rather than forcing in placeholder content for its own sake.
- This skill is self-contained: it doesn't read or write outputs from any other skill in this
  plugin.
