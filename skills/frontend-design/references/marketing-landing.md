# Track 3: Marketing, Landing & Showcase Playbook

Use this playbook when designing marketing websites, product landing pages, campaign showcases, creator portfolios, pricing calculators, or brand-forward storytelling surfaces.

---

## 1. Hero Section & First Impressions

- **Typographic Voice**:
  - Anchor the hero with an unforgettable typographic personality. Pair an expressive display typeface (editorial serif, geometric brutalist, or neo-grotesque) with a clean, high-legibility body font.
  - Avoid generic kickers/pills unless specifically requested. Let the headline deliver immediate punch.
- **Atmospheric Visual Anchor**:
  - Center the hero around a high-fidelity visual: interactive product mockup, 3D tilt card (`perspective: 1000px; transform: rotateX(...) rotateY(...)`), layered glassmorphism composition, or animated canvas particle backdrop.
  - Provide a clear, high-contrast primary CTA with instant tactile response (`active:scale-[0.98]`).

---

## 2. Visual Rhythm & Narrative Pacing

- **Alternating Density**:
  - Avoid repetitive sequences of identical 3-column card grids. Alternate section pacing:
    1. Hero: High-impact, spacious, atmospheric.
    2. Logo Wall / Social Proof: Subtle, monochrome, infinite marquee or clean grid.
    3. Bento Grid: Asymmetric feature highlights (large featured bento item + compact companion cells).
    4. Deep Dive / Interactive Demo: Split 50/50 section with interactive tabbed preview.
    5. Pricing Matrix: Clear visual hierarchy with highlighted "Recommended" tier.
    6. FAQ Accordion: Scannable, clean border dividers, smooth expand/collapse animations.
- **Scroll-Driven Polish**:
  - Use scroll-triggered fade-ups or staggered reveals (`animation-delay: 100ms * index`) to make the page feel orchestrated rather than static.
  - Sticky Navigation Bar: Morph the navbar as the user scrolls (add `backdrop-blur-md bg-background/80`, shrink padding, or float as a pill dock).

---

## 3. High-Converting Pricing & Social Proof

- **Pricing Architecture**:
  - Clear billing interval toggle (Monthly vs. Annual with a "Save 20%" badge).
  - Elevate the most popular/recommended plan: distinctive border accent, subtle glow, or elevated z-index scale.
  - Feature lists with explicit green checks vs muted dashes to make differences instantly scannable.
- **Social Proof & Testimonials**:
  - Use varied avatar sizes, real-sounding quotes, company logos, and metric callouts ("4.9/5 from 1,200+ teams") rather than generic placeholder boxes.

---

## 4. Anti-Patterns to Avoid in Marketing & Landing

- **No Cliche AI Aesthetics**:
  - Avoid the overused "purple/cyan gradient blob on dark background" template.
  - Avoid identical 3-card columns with generic Lucide icons inside circles.
  - Avoid centered wall-of-text blocks that no user will read.
- **No Static Non-Responsive Imagery**:
  - Mockups and illustrations must scale responsively or reorganize on mobile without clipping or microscopic text.
