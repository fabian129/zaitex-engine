# Active DNA — [Project Name]

> Single source of truth for all visual decisions. Every skill reads from this file.
> Location: `.agent/design/active-dna.md`

---

## 🎨 Color Palette

### Primary Colors
```
Brand Primary:    #___
Brand Secondary:  #___
Accent:           #___
```

### Neutral Colors
```
Background:  #___
Foreground:  #___
Muted:       #___
Border:      #___
```

### Semantic Colors
```
Success:  #___
Warning:  #___
Error:    #___
Info:     #___
```

---

## 📝 Typography

### Font Families
```
Heading:  [Font Name], sans-serif
Body:     [Font Name], sans-serif
Mono:     [Font Name], monospace
```

### Type Scale
```
Display:     72px / 4.5rem
H1:          48px / 3rem
H2:          36px / 2.25rem
H3:          30px / 1.875rem
H4:          24px / 1.5rem
H5:          20px / 1.25rem
H6:          18px / 1.125rem
Body Large:  18px / 1.125rem
Body:        16px / 1rem
Body Small:  14px / 0.875rem
Caption:     12px / 0.75rem
```

### Font Weights
```
Light:     300
Regular:   400
Medium:    500
Semibold:  600
Bold:      700
```

---

## 📐 Spacing System

```
xs:   4px    (0.25rem)
sm:   8px    (0.5rem)
md:   16px   (1rem)
lg:   24px   (1.5rem)
xl:   32px   (2rem)
2xl:  48px   (3rem)
3xl:  64px   (4rem)
4xl:  96px   (6rem)
```

---

## ✨ Visual Effects

### Shadows
```css
shadow-sm:   0 1px 2px rgba(0, 0, 0, 0.05)
shadow-md:   0 4px 6px rgba(0, 0, 0, 0.1)
shadow-lg:   0 10px 15px rgba(0, 0, 0, 0.1)
glow:        0 0 20px rgba([accent], 0.5)
```

### Glassmorphism
```css
backdrop-filter: blur(10px)
background: rgba(255, 255, 255, 0.05)
border: 1px solid rgba(255, 255, 255, 0.1)
```

### Gradients
```css
gradient-1: linear-gradient(135deg, #___ 0%, #___ 100%)
gradient-2: linear-gradient(to right, #___, #___)
```

---

## 🎬 Motion DNA

### Intensity Level: [Subtle / Expressive / Luxury]

```
Scroll:     [Native / Lenis Smooth]
Hover:      [Lift + Shadow / Magnetic / Scale]
Entrance:   [Fade up / Clip reveal / Stagger]
Easing:     cubic-bezier(___, ___, ___, ___)
```

### Duration
```
Fast:    150ms   (hover states, toggles)
Normal:  300ms   (most transitions)
Slow:    500ms   (page transitions, complex animations)
```

### Lenis Config (if Smooth Scroll)
```
lerp:      0.1
duration:  1.2
```

---

## 📱 Breakpoints

```
mobile:      640px
tablet:      768px
desktop:     1024px
wide:        1280px
ultra-wide:  1536px
```

---

## 🔑 Signatures

> These define what makes THIS project visually unique.
> Signatures override all defaults. If a reference conflicts with a Signature, the Signature wins.

```
Cards:        [ex. Sharp corners, 1px border zinc-800, no shadow, hover: lift + border glow]
Buttons:      [ex. Pill shape, primary bg, shimmer sweep on hover]
Backgrounds:  [ex. Noise overlay 0.03 + dot grid 0.15, no particles]
Layout:       [ex. Asymmetric 60/40, max-w-7xl, generous py-32 sections]
Icons:        [ex. Lucide, 24px, stroke-width 1.5, text-muted]
Hover:        [ex. All interactive elements: scale 1.02 + shadow grow, 300ms ease-out]
Borders:      [ex. 1px solid zinc-800 on cards, no borders on sections]
Border Radius:[ex. rounded-lg on cards, rounded-full on buttons, no rounded-3xl anywhere]
Images:       [ex. Always rounded-lg, never full-bleed, parallax on hero only]
Nav:          [ex. Transparent → blur on scroll, logo left, links right, no hamburger on desktop]
```

---

## 🎯 Design Principles

1. **[Principle Name]**: [Description]
2. **[Principle Name]**: [Description]
3. **[Principle Name]**: [Description]
4. **[Principle Name]**: [Description]
5. **[Principle Name]**: [Description]

---

## 🖼️ Design References

### Approved References
```
[Site/Image 1]: [URL or description] — What we took from it: [pattern/vibe]
[Site/Image 2]: [URL or description] — What we took from it: [pattern/vibe]
```

### Rejected References (and Why)
```
[Site/Image]: [URL] — Why not: [too heavy, wrong vibe, etc.]
```

---

## 📋 Generation Notes

```
Created by:     [Design Director / Manual / Aura Migration]
Created on:     [Date]
Last updated:   [Date]
Locked:         [Yes / No — if Yes, do not modify without user approval]
```