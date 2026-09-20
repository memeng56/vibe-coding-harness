---
name: frontend-design
description: Create distinctive, production-grade frontend interfaces with high design quality across 4 specialized tracks: (1) Mobile & Touch-first UI, (2) Desktop & Web UI, (3) Marketing, Landing & Showcase, and (4) Games & Creative Canvas. Use this skill when the user asks to build components, pages, dashboards, mobile apps, marketing sites, or games.
---

This skill guides the creation of distinctive, production-grade frontend interfaces that avoid generic "AI slop" aesthetics. It dynamically routes to specialized architectural playbooks across 4 core tracks:

1. **Mobile & Touch-First UI**
2. **Desktop & Web UI**
3. **Marketing, Landing & Showcase**
4. **Games & Creative Canvas**

---

## 1. Platform & Surface Routing Matrix

Before writing any code, determine the primary interaction model or surface from the user's request. Load and follow the specialized reference playbook:

| Track | Primary Surfaces & Identifiers | Specialized Action |
| :--- | :--- | :--- |
| **Track 1: Mobile & Touch-First UI** | Mobile apps, PWAs, Capacitor/Cordova, React Native, mobile webviews, touch-first responsive surfaces. | **Load [references/mobile.md](references/mobile.md)** for minimum 44px tap targets, thumb-zone placement, sliding bottom sheets, safe areas (`env(safe-area-inset-*)`), and touch gestures. |
| **Track 2: Desktop & Web UI** | SaaS platforms, dashboards, admin tools, data tables, multi-panel tools, desktop apps (Tauri, Electron). | **Load [references/desktop-web-ui.md](references/desktop-web-ui.md)** for high data density, multi-pane splitters, collapsible navigation rails, `Cmd+K` palettes, and window chrome (`-webkit-app-region: drag`, traffic lights, context menus). |
| **Track 3: Marketing, Landing & Showcase** | Marketing websites, product launch pages, brand showcases, creator portfolios, pricing calculators. | **Load [references/marketing-landing.md](references/marketing-landing.md)** for bold hero typography, visual rhythm, interactive bento grids, pricing comparison tiers, and scroll-driven storytelling. |
| **Track 4: Games & Creative Canvas** | 2D/3D browser games, interactive canvas simulations, WebGL/Three.js/PixiJS, particle engines, physics sandboxes. | **Load [references/games.md](references/games.md)** for delta-time game loops (`requestAnimationFrame`), canvas DPR scaling, multi-key input tracking, and DOM/SVG HUD overlays. |

*Ambiguity rule: If a product app is viewed on a mobile device, combine Track 2 (data model/logic) with Track 1 (mobile touch/sheet ergonomics).*

---

## 2. Universal Aesthetic Floor & Design Thinking

Regardless of track, commit to a BOLD, intentional aesthetic direction before coding:

1. **Purpose**: What problem does this interface solve? Who uses it?
2. **Tone**: Pick an extreme: brutally minimal, maximalist chaos, retro-futuristic, organic/natural, luxury/refined, playful/toy-like, editorial/magazine, industrial/utilitarian, brutalist/raw, art deco/geometric, or soft/pastel.
3. **Differentiation**: What makes this unforgettable? What single detail will users remember?

Execute working code that is:
- Production-grade and fully functional.
- Visually striking and memorable.
- Cohesive with a clear aesthetic point-of-view.
- Meticulously refined in every detail.

---

## 3. Core Aesthetic Guidelines

- **Typography**: Choose fonts that are beautiful, unique, and characterful. Avoid generic system fonts (Arial, Inter, Roboto). Pair a distinctive display font with a refined body font.
- **Color & Theme**: Commit to a cohesive palette using CSS variables. Dominant colors with sharp accents outperform timid, evenly-distributed palettes.
- **Motion**: Use animations for purposeful feedback and high-impact reveals. Focus on orchestrated page loads with staggered reveals (`animation-delay`) and tactile active states.
- **Spatial Composition**: Unexpected layouts. Asymmetry, diagonal flow, overlap, grid-breaking elements, generous negative space, or controlled high density.
- **Backgrounds & Depth**: Create atmosphere rather than defaulting to solid colors. Apply gradient meshes, noise textures, layered transparencies, dramatic shadows, or custom borders.

---

## 4. Hard Anti-Patterns (Zero AI-Slop)

- **NEVER** use generic AI aesthetics: overused font families (Inter, Roboto, Arial), predictable purple-gradient headers on white/dark cards, or repetitive 3-column card grids.
- **NEVER** converge on the same aesthetic choices across different projects; vary themes, typography, and layout models based on the domain.
- **NEVER** leave interactive components without feedback states (hover, focus-visible, active).
