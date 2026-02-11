# Zaitex Design Vision — "The Aura"

> **Status:** Draft for User Approval
> **Goal:** Synthesize the visual direction based on specific "Aura Build" references.

---

## 🖤 The Vibe: "Dark Mode Luxury"

We are moving away from "standard agency" and towards **"Digital Art Gallery."**
The feeling should be **expensive, silent, and confident.**

**Keywords:**
- **Liquid:** Layouts that flow rather than stack.
- **Tactile:** High-res textures (glass, noise, grain) that you can almost feel.
- **Cinematic:** Typography / Motion that directs the eye like a movie.

---

## 🧬 Visual DNA (Derived from References)

### 1. The Canvas
- **Background:** Deepest Black (`#000000` or `#050505`).
- **Surface:** Glassmorphism isn't just a blur; it's a *material*. Use subtle noise overlays and extremely faint borders (`white/5` or `white/10`) to define space without harsh lines.

### 2. The Layout: "Liquid Bento"
Based on `studio-creative.aura.build`:
- **Asymmetric Grids:** Don't just act like a spreadsheet. Span columns, vary row heights.
- **Fluid Gaps:** Spacing should feel organic.
- **Content-First:** The grid adapts to the content (massive images next to tiny text).

### 3. Typography: "Extreme Contrast"
Based on `frontend-engineer-template.aura.build`:
- **The "Hero":** Massive, tight-letter-spacing sans-serifs (Inter Tight, Geist, or identical) for headlines.
- **The "Technical":** Tiny, uppercase, mono-spaced labels (e.g., `[ SELECTED WORK 2026 ]`) to add a "precision engineering" feel.
- **Hierarchy:** Skip the middle sizes. Go huge or go tiny.

### 4. Motion & Interactivity
Based on `digital-creative-agency.aura.build`:
- **Magnetic:** Buttons and cards should feel like they have gravity.
- **Glows:** Hover states shouldn't just change color; they should emit light.
- **Scroll:** Smooth (Lenis) is mandatory. Elements should parallax or reveal slowly.

---

## 🎯 Specific Reference Breakdown

| Site | Key Takeaway for Zaitex |
|:-----|:------------------------|
| **Frontend Engineer** | The **"Technical Precision"**. Use of tiny monospaced details to sell expertise. |
| **Digital Creative** | The **"Ethereal Light"**. Use of colored glows (Blue/Purple/Lime) to break the darkness. |
| **Studio Creative** | The **"Bento Structure"**. How to organize complex case studies into a clean grid. |

---

## 🚀 Implementation Strategy

1.  **Reset `globals.css`**: Establish the deep black base and fluid spacing variables.
2.  **Typography System**: Install strict font families (Sans + Mono) and define the "Huge vs Tiny" scale.
3.  **The Grid Engine**: Build a reusable `BentoGrid` component that handles the "Liquid" layout logic.
4.  **Texture Layer**: Add a global grain/noise overlay to kill the "flat digital" look.
