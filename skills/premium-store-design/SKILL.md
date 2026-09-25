---
name: premium-store-design
description: "Apply a premium design system to a Shopify storefront: typography, color, whitespace, PDP mechanics, and disciplined motion, plus a luxury editorial Swiss variant (architecture-portfolio product presentation, an exposed 12-column grid, numbered section indexes) for stores courting a premium, influencer and press audience. Use when designing or restyling store pages, choosing a theme, building custom sections, or reviewing a storefront for a premium or editorial Swiss feel. No existing skill covers these aesthetic rules, theme choice, and Baymard PDP checks; Liquid token plumbing itself is partly covered by benjaminsehl/liquid-skills' liquid-theme-standards (unlicensed, not adopted here) and by Shopify AI Toolkit's shopify-liquid."
---

# Premium Store Design

Core law (from the 2026 premium-site research): **premium feel = editorial photography +
restrained typography + generous whitespace + boring PDP mechanics done right. Not
motion.** Excessive scroll/entrance animation measurably hurts Core Web Vitals and
conversion, and punishes the mobile majority first.

## Reference patterns (steal these, not their assets)

- Jacquemus/Skims: photography IS the product; UI chrome nearly invisible.
- Aesop: literary editorial copy + type discipline out-premiums any animation.
- Cuup: premium expressed as fit-UX depth (size systems, calculators).
- Triangl: small disciplined SKU count → simple IA; restraint reads expensive.
- Reformation/ALD: an editorial/lookbook channel ("Stories") beside commerce.

## Design tokens (define once, in the theme's settings/CSS custom properties)

- **Type:** ONE display face for hero/campaign (high-contrast serif: Canela, GT Alpina,
  Instrument Serif; free fallback Playfair Display) + ONE workhorse grotesque sans for
  all UI/body (Söhne, Neue Montreal; free: Satoshi or Inter). **Pressure-test at 13px**
  in size charts and mobile filters before committing. The classic failure is a hero
  font illegible in a spec table.
- **Color:** neutral/skin-tone or near-monochrome base; ONE accent reserved for CTAs;
  photography carries the color story, never UI chrome.
- **Space:** generous negative space, restrained grid: the cheapest "looks expensive"
  lever that exists.
- Full light-theme token set on `:root`; test both themes if the storefront offers dark.

## Theme selection

| Pick | When |
|---|---|
| Symmetry ($340) | fashion-editorial, campaign imagery, moderate catalog (default) |
| Prestige (~$400) | luxury-minimal, small catalog; 78.7% CWV pass rate across live stores; most common premium theme → REQUIRE custom section/CSS differentiation |
| Focal ($320–350) | campaign-photography-led / activewear energy |
| Impact / Broadcast ($380–400) | large catalog CRO / storytelling-first |

Never headless/Hydrogen for this build (2–3× cost multiplier, Plus-tier economics).
Custom needs → custom sections + metaobjects, inside the theme.

## PDP acceptance checklist (Baymard 2026: ship blocked until all pass)

- [ ] Button-style size selectors (never dropdowns), cited +15–20% add-to-cart
- [ ] Color swatches with image switch on hover/tap
- [ ] Inline size chart (metaobject-driven) + simple fit quiz; fit causes ~70% of fashion returns
- [ ] On-body/model shot + scale reference in every image set
- [ ] Return/final-sale policy visible ON the PDP (60% of shoppers look there)
- [ ] Guest wishlist (no forced account)
- [ ] Estimated total cost incl. shipping before checkout
- [ ] Customer review photos browsable
- [ ] Quick-add on collection grids (hover modal desktop / corner tap-icon mobile)

## Motion rules

**Allowed:** Lenis smooth scroll · GSAP/ScrollTrigger subtle section fade/slide reveals ·
Swiper PDP galleries · CSS View Transitions API (Baseline Oct 2025, zero-dependency
list→PDP and quick-shop transitions inside Liquid's no-framework constraint; verify
graceful degradation).
**Banned:** scroll-jacking, parallax, entrance animation on every element, infinite
scroll on collections, anything delaying LCP. Budget: LCP < 2.5s mobile, always.

The Editorial Swiss variant below changes the parallax ban and the Lenis/Swiper
defaults; see its override table before applying these rules to that variant.

## Budget order (spend in this order, stop when out)

1. Photography/creative direction (one styled sample day-shoot)
2. Copywriting system (editorial voice, consistent)
3. Theme + custom sections to de-genericize
4. Fit/size app + review app
5. Motion polish (last, minimal)

## Liquid implementation notes

- Tokens as CSS custom properties in `settings_data`/theme CSS; sections read them.
  Never hardcode colors/fonts in sections.
- Custom sections: schema-exposed settings so future edits don't need code.
- Size charts as metaobjects rendered by snippet: one source of truth per garment class.
- Validate all Liquid with Shopify-AI-Toolkit's validators before deploy.

## Variant: Editorial Swiss

Use this variant when the store is courting a premium, influencer and press facing
audience and wants products presented the way architecture portfolios present projects
(numbered indexes, an exposed 12-column grid, oversized serif section numerals) rather
than the softer photography-led base look. See `lastone/docs/16-editorial-redesign.md`
for the concrete redesign this variant was distilled from.

Full rules: [`references/editorial-swiss.md`](references/editorial-swiss.md).

Editorial Swiss is a styling of this base law, not a replacement: the PDP acceptance
checklist, budget order, and theme selection rules above still apply unchanged. It adds
grid, type, and color rules, and contradicts the base only on motion mechanics. Choose
the variant deliberately; where
it disagrees with the base, the variant wins only for stores that adopted it.

| Rule area | Base (default, this file) | Editorial Swiss variant (wins only when chosen) |
|---|---|---|
| Parallax | Banned outright | Allowed as micro-parallax only: transform-only, about 6% travel, scrubbed, never on the hero, max two per viewport |
| Scroll & gallery mechanism | Lenis smooth scroll and Swiper PDP galleries are the defaults | Native `overflow-x` scroll-snap rails preferred over Swiper; Lenis is not used, arrow buttons enhance but never replace native scroll |
| `prefers-reduced-motion` | No explicit rule beyond the general motion caution above | Nothing beyond native scrolling; the base page is fully styled and visible with zero JavaScript |

## Related

`shopify-store-builder` (sequencing) · baslefeber/shopify-skills (CRO/perf/a11y audits
post-build) · build repo `lastone/docs/04-design-playbook.md` (full sourced playbook,
base variant) · `lastone/docs/16-editorial-redesign.md` (Editorial Swiss variant) ·
companion catalog `ECOMMERCE-STACK.md` frontend table.
