---
name: aura-migration
description: Converts raw HTML output from Aura.build (single-file HTML with inline CSS/JS) into clean Next.js components using the Zaitex Stack (Tailwind, GSAP, Lenis, Framer Motion). Use when a user provides an Aura.build export and wants it rebuilt as production-ready code in the existing project structure.
---

## TL;DR
**Skill:** 17 — Aura Migration  
**Phase:** Phase 1 (AURA mode)  
**Purpose:** Convert Aura template into project structure  
**Change Budget:** LARGE (migration only)  
**Stop:** After template is integrated cleanly  
**Redirects:** If identity mismatch → 18.5 (mini)

# Aura Migration

## Objective
Take the visual output from Aura.build — which looks great but is fragile — and rebuild it as stable, maintainable Next.js components using the Zaitex Stack. The design stays identical. The code becomes real.

## Philosophy
**Not:** "Rewrite everything from scratch."
**Instead:** "Preserve every visual decision. Replace every fragile pattern."

Aura gives you a pixel-perfect design that the client has approved. Your job is to honor that approval while making it actually work.

---

## When This Skill Triggers
- User provides a `.html` file exported from Aura.build
- User mentions "Aura", "aura.build", "convert this HTML", or "migrate this design"
- User pastes raw HTML with characteristics matching Aura output (single file, inline styles, CDN script tags for GSAP/Lenis/Tailwind)

---

## Phase 1: Ingest & Audit

### Step 1: Identify the File
Confirm you have the full HTML file. Aura exports are recognizable by:
- Single `.html` file with everything inline
- CDN links to Tailwind, GSAP, ScrollTrigger, Lenis, Iconify/Lucide
- CSS custom properties in `:root` (colors, fonts, easing)
- Inline `<style>` block with all styles
- Inline `<script>` block(s) at the bottom with GSAP timelines and Lenis init
- Comment markers like `<!-- CARD STACK -->`, `<!-- HERO -->` etc.

### Step 2: Extract the Four Layers
Parse the file and separate into:

| Layer | What to Extract | Where It Goes |
|:------|:----------------|:--------------|
| **Design Tokens** | CSS custom properties (`:root`), colors, fonts, easing curves, border-radius | `globals.css` or Tailwind config |
| **Structure** | HTML sections, semantic markup, content hierarchy | React components (JSX) |
| **Styles** | CSS classes, responsive rules, layout patterns | Tailwind classes + CSS modules where needed |
| **Animation** | GSAP timelines, ScrollTrigger configs, Lenis init, noise overlay | `useGSAP` hooks, Framer Motion, Lenis provider |

### Step 3: Create the Migration Map
Before writing any code, produce a brief migration map:

```markdown
## Migration Map: [Page Name]

### Design Tokens
- --c-bg: #F5F5F7 → bg-[#F5F5F7] or extend Tailwind theme
- --c-dark: #0A0A0A → text-[#0A0A0A]
- --c-card: #FFFFFF → bg-white
- --font-display: 'Space Grotesk' → font-display (Tailwind extend)
- --font-body: 'Inter' → font-body (Tailwind extend)
- --ease-out: cubic-bezier(0.16, 1, 0.3, 1) → reuse in GSAP

### Sections Identified
1. [Section Name] → ComponentName.tsx
2. [Section Name] → ComponentName.tsx
...

### Animation Inventory
- [Description] → GSAP ScrollTrigger / Framer Motion / CSS
- Smooth scroll → Lenis provider (already in stack)
- Noise overlay → CSS ::before on layout wrapper

### Image Inventory
- [image-1.jpg] → next/image with fill + object-cover
- [image-2.jpg] → next/image with explicit dimensions
...

### Known Fragile Patterns (Aura-specific)
- Inline background-image URLs → move to next/image or public/ assets
- Hardcoded viewport heights → replace with responsive units
- Script-tag GSAP → useGSAP hooks with proper cleanup
- Missing alt text → add meaningful alts
```

**STOP POINT 🛑**: Present the migration map to the user. Ask: "Does this capture everything? Any sections to skip or prioritize?"

---

## Phase 2: Translate

### Design Tokens → Tailwind Config / globals.css

Extract `:root` variables and decide placement:

```css
/* If tokens are project-wide, extend Tailwind */
/* tailwind.config.ts */
theme: {
  extend: {
    colors: {
      'c-bg': '#F5F5F7',
      'c-dark': '#0A0A0A',
      'c-card': '#FFFFFF',
    },
    fontFamily: {
      display: ['Space Grotesk', 'sans-serif'],
      body: ['Inter', 'sans-serif'],
    },
  },
}
```

```css
/* If tokens are page-specific, keep as CSS variables in globals.css */
:root {
  --ease-out: cubic-bezier(0.16, 1, 0.3, 1);
  --c-border: rgba(0, 0, 0, 0.08);
}
```

**Rule:** Colors and fonts go in Tailwind config. Easing curves and borders stay as CSS variables (GSAP and Tailwind both can reference them).

### Structure → React Components

Each identified section becomes a component. Follow these conventions:

```
app/
  [page-name]/
    page.tsx              ← Assembles sections
    components/
      HeroSection.tsx
      CardStack.tsx
      ContactSection.tsx
      ...
```

**Component template:**
```tsx
"use client";
import { useRef } from "react";
import { useGSAP } from "@gsap/react";
import gsap from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import Image from "next/image";

gsap.registerPlugin(ScrollTrigger);

export function SectionName() {
  const sectionRef = useRef<HTMLElement>(null);

  useGSAP(() => {
    // Migrate GSAP logic here
  }, { scope: sectionRef });

  return (
    <section ref={sectionRef} className="...">
      {/* Migrated markup */}
    </section>
  );
}
```

### Common Aura Patterns → Zaitex Equivalents

| Aura Pattern | Problem | Zaitex Solution |
|:-------------|:--------|:----------------|
| `<img src="...">` inline | No optimization, no lazy load | `<Image src={...} alt="..." fill className="object-cover" />` wrapped in relative container |
| `background-image: url(data:image/svg+xml,...)` noise | Works fine as-is | Keep as CSS `::before` on a layout wrapper |
| `position: sticky` card stack with JS | Fragile, breaks on resize | GSAP ScrollTrigger pin (see Motion Choreographer) |
| CDN `<script src="gsap">` | Global scope, no cleanup | `useGSAP` hook with scope and cleanup |
| CDN `<script src="lenis">` | Manual init, no React lifecycle | `<ReactLenis root>` provider in layout.tsx |
| Inline `<style>` with media queries | Unscoped, can conflict | Tailwind responsive classes (`md:`, `lg:`) + CSS module for complex cases |
| `opacity: 0` on body + JS reveal | Flash of invisible content | Framer Motion `AnimatePresence` or CSS `@starting-style` |
| Hardcoded `height: 80vh` on cards | Fragile on mobile | `h-[80vh] md:h-[85vh]` with responsive consideration |
| `perspective: 1000px` on parent | Can cause z-index issues in React | Keep, but isolate in component with `will-change: transform` |
| `.scrub-word { opacity: 0.15 }` text scrub | Relies on IntersectionObserver in script | GSAP ScrollTrigger `scrub: true` with `useGSAP` |

### Images → next/image

Every `<img>` tag gets converted:

```tsx
// Aura (fragile)
<img src="/some-image.jpg" style="width:100%;height:100%;object-fit:cover;" />

// Zaitex (stable)
<div className="relative w-full h-full">
  <Image
    src="/some-image.jpg"
    alt="Descriptive alt text"
    fill
    className="object-cover"
    sizes="(max-width: 768px) 100vw, 50vw"
  />
</div>
```

**Rule:** Always add `sizes` prop for responsive images. Always add meaningful `alt` text.

### Noise/Grain Overlay

Aura typically uses an SVG-based noise texture as a fixed overlay. This pattern works well as-is:

```tsx
// components/NoiseOverlay.tsx
export function NoiseOverlay() {
  return (
    <div
      className="pointer-events-none fixed inset-0 z-[9999] opacity-[0.03]"
      style={{
        backgroundImage: `url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.8' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E")`,
      }}
    />
  );
}
```

Place in `layout.tsx` above or below `{children}`.

---

## Phase 3: Animate

### Delegate to Motion Choreographer
For all animation decisions, **refer to the Motion Choreographer skill**. The migration skill's job is only to *identify* what animations exist in the Aura file and *map* them to the correct Motion Choreographer pattern.

### GSAP Migration Checklist

For each `gsap.to()` / `gsap.from()` / `gsap.timeline()` in the Aura source:

1. **Identify the trigger**: Is it scroll-based (`ScrollTrigger`), load-based, or interaction-based?
2. **Choose the tool**:
   - Scroll-linked → `useGSAP` + `ScrollTrigger` (stay with GSAP)
   - Hover/click → Framer Motion (simpler in React)
   - Page load → Framer Motion `initial` + `animate`
3. **Wrap in `useGSAP`**: Every GSAP call must be inside `useGSAP(() => { ... }, { scope: containerRef })` for proper cleanup
4. **Replace class selectors with refs**: Aura uses `.card-item`, `.scrub-word` etc. In React, use `useRef` or scoped selectors within the component

```tsx
// Aura (global scope, no cleanup)
gsap.to(".card-inner", {
  scrollTrigger: { trigger: ".card-item", start: "top top", scrub: true },
  scale: 0.9,
  opacity: 0.5,
});

// Zaitex (scoped, with cleanup)
useGSAP(() => {
  gsap.to(".card-inner", {
    scrollTrigger: { trigger: ".card-item", start: "top top", scrub: true },
    scale: 0.9,
    opacity: 0.5,
  });
}, { scope: sectionRef }); // Scopes all selectors to this ref
```

### Lenis Migration

Remove the CDN script and manual init. Replace with the React integration:

```tsx
// app/layout.tsx
import { ReactLenis } from "lenis/react";

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body>
        <ReactLenis root options={{ lerp: 0.1, duration: 1.2 }}>
          {children}
        </ReactLenis>
      </body>
    </html>
  );
}
```

---

## Phase 4: Verify & Deliver

### Visual Diff Checklist
After migration, verify against the Aura original:

- [ ] Colors match exactly (compare hex values)
- [ ] Typography matches (font family, weight, size, letter-spacing, line-height)
- [ ] Spacing matches (padding, margins, gaps)
- [ ] Border radius matches
- [ ] Scroll animations feel the same (timing, easing, triggers)
- [ ] Noise overlay is present and at correct opacity
- [ ] Responsive behavior works at mobile, tablet, desktop
- [ ] Images load correctly and don't flash/jump
- [ ] No layout shift on page load

### Common Post-Migration Issues

| Symptom | Likely Cause | Fix |
|:--------|:-------------|:----|
| Images flash on load | Missing `priority` prop on hero image | Add `priority` to above-fold images |
| Scroll animations jank | GSAP not using `will-change` | Add `will-change: transform` on animated elements |
| Layout shifts | `next/image` without explicit dimensions | Use `fill` with sized container or specify `width`/`height` |
| Fonts flash (FOUT) | Next.js font not configured | Use `next/font/google` instead of `<link>` tag |
| Noise overlay covers clicks | Missing `pointer-events-none` | Add `pointer-events-none` to overlay |
| Sticky sections broken | Lenis conflicts with GSAP pin | Ensure `ScrollTrigger.scrollerProxy` is not needed, or configure it |

### Font Migration
Replace the Google Fonts `<link>` tag with Next.js font optimization:

```tsx
// app/layout.tsx
import { Inter } from "next/font/google";
import localFont from "next/font/local";

const inter = Inter({ subsets: ["latin"], variable: "--font-body" });
const spaceGrotesk = Space_Grotesk({
  subsets: ["latin"],
  variable: "--font-display",
});

export default function RootLayout({ children }) {
  return (
    <html lang="en" className={`${inter.variable} ${spaceGrotesk.variable}`}>
      ...
    </html>
  );
}
```

---

## Cross-Skill References

This skill does **not** make design or layout decisions. It translates. For decisions, delegate:

| Decision | Delegate To |
|:---------|:------------|
| "Should this be a grid or flexbox?" | **Layout Architect** |
| "What animation pattern fits here?" | **Motion Choreographer** |
| "Is this section structure optimal?" | **Page Planner** |
| "Does this match the approved design?" | **Design Director** |

---

## Output Format

The migration produces:

```
app/[page-name]/
  page.tsx                    ← Section assembly
  components/
    HeroSection.tsx           ← Per-section components
    CardStack.tsx
    [OtherSections].tsx
    NoiseOverlay.tsx           ← Reusable noise texture
docs/
  migration-map-[page].md     ← The audit from Phase 1
```

Each component is self-contained with its own `useGSAP` hooks, refs, and scoped styles.

---

## Key Principles

1. **The design is approved.** Do not improve, redesign, or "modernize" the visual output. Match it exactly.
2. **Aura output is predictable.** Single HTML file, inline everything, CDN scripts. The parsing step is mechanical.
3. **Delegate, don't invent.** Use existing skills for layout and motion decisions. This skill is a translator, not a designer.
4. **Images are the #1 breakpoint.** Most Aura bugs come from fragile image handling. `next/image` solves this.
5. **Every GSAP call needs a scope.** No global selectors. No unscoped animations. `useGSAP` with `{ scope: ref }` always.
