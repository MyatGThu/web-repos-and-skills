# Editorial Swiss (variant of premium-store-design)

Parent law: `premium-store-design/SKILL.md`. This file only covers what the variant
adds or changes; the base's core law, PDP acceptance checklist, budget order, and
theme selection table all still apply. Where the two disagree, use the override table
in `SKILL.md`'s "Variant: Editorial Swiss" section, not this file.

Core law: luxury is subtraction plus precision. One serif voice used huge and rarely,
one grotesque doing 90 percent of the pixels, one accent used once per viewport,
photography and film carrying all the color, and a grid you can see. Motion is an
enhancement layer over a page that is complete without it.

## Reference patterns (verified 2026-08-26; steal the pattern, never the asset)

- big.dk / snohetta.com: projects as a captioned index; photography dominant; chrome
  nearly invisible; hairline dividers; arrow-driven horizontal galleries.
- toteme.com: monochrome restraint, sentence case display, alternating image and text
  blocks, negative space as the brand.
- hunzag.com / jadeswim.com / eresparis.com: luxury swim ships quiet type, white
  grounds, unadorned tabular prices, zero promo overlays, and earns its press marquee.
- 2026 roundups: oversized high-contrast serif headlines as design elements,
  asymmetric offsets, subtle scroll reveals only. Pure Swiss is softening; pair the
  strict grid with editorial warmth.

## Type method (extends the base's serif/grotesque pairing and 13px test)

- TWO families, FIVE weight instances total, both from one performant source (Google
  Fonts with preconnect, display swap, pinned instances). A display serif that ships
  few weights (Instrument Serif's single 400 roman plus italic is ideal) makes the cap
  structural. The grotesque (Instrument Sans class) carries body, UI, labels at
  400/500/600.
- The display face never appears in tables, size charts, forms, buttons, prices, nav,
  or below its stated floor (28px); run the base's 13px pressure test on the grotesque
  before committing.
- Sentence case for display; tracked uppercase only at the 13px label tier. Flush
  left, ragged right, always. Hierarchy comes from size and placement.
- `font-variant-numeric: tabular-nums` on every price, table, and counter. Verify the
  served instance actually has tnum (render 111.00 against 888.00) or pin numerals to
  a fallback that does.

## Grid and showcase method

- 12 columns, 8px base, generous fluid gutters, section padding around 10vh. Expose
  the grid: full-bleed 1px hairline rules between sections, hairline frames on forms
  and toolbars. Hairlines are a dedicated decorative token, never a text color.
- Number the page: every section gets an oversized ghost numeral (grotesque, tabular,
  aria-hidden, hairline-tone) plus a 13px tracked label ("02 / THE RANGE"). Numbered
  structure is the Swiss signature and costs zero performance.
- Present products like an architecture office presents projects: the index list is
  the primary catalog view. Row = counter, name in the serif, metadata in 13px muted,
  tabular price right-aligned, hairline below. Hover may float an image swatch;
  mobile shows an inline thumbnail. Offer a grid as the secondary view, asymmetric
  (alternating cell widths), never marketplace-uniform.
- Captions everywhere: every editorial image gets a 13px figure caption ("Fig. 02
  Back, size 10 shown on 175cm"). Captions are the cheapest editorial signal there is.
- Asymmetry by vertical offset: pair blocks start at different heights on the grid.
  Full-bleed video earns at most one moment per page.
- The footer is a sign-off: the wordmark set enormous in the serif across the full
  grid, link columns and legal at 13px beneath. One optional inverse (dark) beat per
  site, maximum.

## Color method (extends the base's neutral-base-plus-one-accent rule)

- Light gallery ground (warm paper, not #FFF), near-black ink (never #000), one warm
  neutral for bands and mats. The base's single accent gets a hard quantity budget
  here: one accent element per viewport, normally the primary CTA. Add an annealed
  dark variant of the accent hue for text links so the accent can speak without a
  filled chip.
- Compute (do not eyeball) WCAG contrast for every text-on-surface pair, including the
  13px tier at AA 4.5:1, including accent surfaces (dark ink on the accent, never
  white unless proven). Ghost numerals are decorative and exempt only while
  aria-hidden and meaning-free.

## Motion restraint (all of it fail-open)

See the override table in `SKILL.md` for how this changes the base's parallax ban and
its Lenis/Swiper defaults.

- Base page is fully styled and visible with zero JavaScript; no `opacity: 0` in CSS.
  One init guard covers missing CDN, JS off, and `prefers-reduced-motion`.
- Allowed: micro-parallax inside `overflow-hidden` frames (transform-only, about 6
  percent travel, scrubbed, never the hero, max two per viewport); ONE reveal pattern
  (small y plus fade, once, below the fold only); horizontal rails built on native
  `overflow-x` with scroll-snap, enhanced (never replaced) by arrow buttons.
- Hidden scrollbars: `scrollbar-width: none` plus a `::-webkit-scrollbar { display:
  none }` rule on rails, optionally on the document; if the document scrollbar goes,
  ship a 1px scroll-progress hairline (CSS scroll-driven animation, degrades to
  absent) and keep keyboard scrolling and focus outlines untouched.
- LCP is untouchable: preloaded poster image as the LCP element, video fades in after
  `loadeddata`, no transform-scale on playing video ever, all scripts deferred, only
  transform and opacity animate (zero CLS by construction).

## What to avoid (beyond the base's banned list)

- Pinned horizontal sections (native scroll-snap rails only), Ken Burns on video,
  animated nav or prices, more than one reveal pattern.
- Tracked uppercase display type, centered body copy, the display face in UI.
- Fake luxury signals: invented press logos, "as seen on" without a real placement,
  false scarcity on made-to-order goods. Made-to-order is the story; numbered drops
  with real dates are truthful scarcity.
- Accent sprawl: the moment the accent appears twice in a viewport, one is wrong.
- More than five weight instances, any text below 13px, hairlines used as text color.

## Acceptance gate (on top of the base's PDP checklist)

- 13px chart test passes; tabular numerals verified; every text pair AA-computed.
- JS disabled: every page sells (working forms, visible content, scrollable rails).
- `prefers-reduced-motion`: no motion beyond native scrolling (see the override table
  in `SKILL.md`).
- Mobile LCP under 2.5s, CLS under 0.1, with motion enabled.
- The PDP must still pass the base's full Baymard checklist: editorial never overrides
  button size selectors, visible returns policy, or on-body imagery.

## Related

- `premium-store-design/SKILL.md`: this variant's parent law (photography,
  whitespace, PDP mechanics, budget order). Editorial Swiss is a styling of it, not a
  replacement.
- Build repo spec: `lastone/docs/16-editorial-redesign.md` (the concrete redesign this
  variant was distilled from: tokens, block plans, motion choreography).
- Companion catalogs: `ECOMMERCE-STACK.md` frontend table, `LIBRARIES.md`.
