---
name: layout-architect
description: Strategic layout decision framework. Determines the best component structure to serve content goals.
---

# Layout Architect

## Objective
Translate content strategy into smart component layouts using the Zaitex Stack.

## Philosophy
**Not:** "Use grid-cols-3"  
**Instead:** "Why grid-cols-3? What serves the content best?"

---

## Decision Framework

### Question 1: What's the Content Type?

#### Hero / Landing
**Goal:** Grab attention, communicate value  
**Common Patterns:**
- Centered single-column (focus)
- Split 50/50 (visual + text)
- Asymmetric 60/40 (emphasis on one side)

**Components to consider:**
- Background: Layered (Grid + Lines + Particles) for premium feel
- CTA: `ShinyGlassButton` for primary action
- Text effects: `TextScramble` for tech vibe

#### Portfolio / Grid
**Goal:** Show multiple items, allow scanning  
**Common Patterns:**
- Masonry grid (varied heights)
- Even grid 2-3 columns
- Featured + grid (1 large, rest small)

**Components:**
- Cards with hover effects
- Staggered entrance animations
- Subtle background pattern

#### Features / Services
**Goal:** Explain multiple concepts clearly  
**Common Patterns:**
- Icon + text blocks (3-4 columns on desktop)
- Timeline (vertical flow)
- Comparison table

**Components:**
- Icon from `lucide-react`
- Grid with gap-8 or gap-12
- Hover lift effect

---

## Layout Patterns (The Proven Formulas)

### Pattern: Hero Split
**When:** Need visual + text balance
```tsx
<section className="min-h-screen grid lg:grid-cols-2">
  <div>{/* Left: Text content */}</div>
  <div>{/* Right: Visual or HUD */}</div>
</section>
```

### Pattern: Centered Impact
**When:** Single strong message
```tsx
<section className="min-h-screen flex items-center justify-center">
  <div className="max-w-4xl text-center">
    {/* Headline + CTA */}
  </div>
</section>
```

### Pattern: Grid Showcase
**When:** 6-12 items to display
```tsx
<div className="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
  {items.map(item => <Card key={item.id} {...item} />)}
</div>
```

---

## Responsive Strategy

### Mobile-First Thinking
```tsx
// Base: Mobile (stack everything)
className="flex flex-col gap-4"

// Tablet: Some horizontal layout
className="flex flex-col md:flex-row gap-4"

// Desktop: Full grid
className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8"
```

### Common Breakpoints
- **sm (640px)**: Rare, usually skip
- **md (768px)**: Tablet, introduce columns
- **lg (1024px)**: Desktop, full layout
- **xl (1280px)**: Large screens, max-w constraints

---

## Background Layer Strategy

### Question: How much atmosphere?

#### Subtle (Professional/Corporate)
```tsx
<DotGridPattern className="opacity-15" />
// That's it. Clean and simple.
```

#### Medium (Modern Tech)
```tsx
<DotGridPattern className="opacity-30" />
<GlowingLines count={5} className="opacity-40" />
// Two layers, balanced
```

#### Bold (Premium Showcase)
```tsx
<DotGridPattern className="opacity-40" />
<GlowingLines count={8} className="opacity-40" />
<ParticleField count={60} className="opacity-60" />
<Vignette />
// Full "Aura Stack"
```

**Rule:** More text content = lower background opacity

---

## Component Integration (Zaitex Stack)

### Available Components
Import from `@/components/zaitex/`:
- Background: `DotGridPattern`, `GridPattern`, `GlowingLines`, `ParticleField`
- Effects: `AmbientGlow`, `PulsatingGlow`, `MeshGradient`
- Interactive: `ShinyGlassButton`, `TextScramble`
- Layout: `EdgeFade`, `BorderBeam`

### Decision Tree Example
```
Goal: Modern tech feel, good performance

Background?
  → DotGridPattern (tech structure) ✓
  → GlowingLines (energy) ✓
  → ParticleField? (would be cool but...)
    → Check: Is this mobile-first? YES
    → Skip particles (performance)

Buttons?
  → ShinyGlassButton (premium feel) ✓

Text effects?
  → TextScramble for labels (HUD vibe) ✓
  → Skip for body text (readability)
```

---

## Animation Strategy

### Entrance Choreography
```tsx
// Section wrapper
<motion.section
  initial={{ opacity: 0 }}
  whileInView={{ opacity: 1 }}
  transition={{ duration: 0.6 }}
>
  {/* Individual items */}
  {items.map((item, idx) => (
    <motion.div
      key={idx}
      initial={{ opacity: 0, y: 20 }}
      whileInView={{ opacity: 1, y: 0 }}
      transition={{ delay: idx * 0.1, duration: 0.5 }}
    >
      {item}
    </motion.div>
  ))}
</motion.section>
```

**Rule:** Stagger children by 0.1 delay for grid items

---

## Spacing System

### Section Padding (Vertical)
```tsx
"py-12"  // Minimal (mobile)
"py-20"  // Standard (desktop resume)
"py-32"  // Generous (hero, feature sections)
```

### Content Spacing (Between Elements)
```tsx
"gap-4"  // Tight (related items)
"gap-8"  // Standard (grid cards)
"gap-12" // Generous (major sections)
```

### Container Max Width
```tsx
"max-w-7xl" // Standard (most content)
"max-w-4xl" // Narrow (reading text)
"max-w-full" // No limit (full-width heroes)
```

---

## Output Format

Create `docs/layout-plan.md`:
```markdown
# [Section Name] Layout Plan

## Goal
[What this section achieves]

## Pattern
[Which pattern: Split, Centered, Grid]

## Components
- Background: DotGridPattern + GlowingLines
- Buttons: ShinyGlassButton (primary CTA)
- Layout: grid lg:grid-cols-2

## Responsive
Mobile: Stack vertical
Desktop: Side-by-side 50/50

## Animation
Fade in on view, stagger children
```

---

## Key Principle
**Every layout decision must serve the content and user goal.**  
If you can't explain why you chose a layout, reconsider.

---

# PART 2 — 2026 LAYOUT PATTERNS

## Bento Grid (Mixed-Size Cards)

The signature layout of modern design. Cards of different sizes create visual hierarchy.

### Pattern: Bento 2x2 with Feature

```tsx
<div className="grid grid-cols-4 grid-rows-2 gap-4 h-[600px]">
  {/* Feature card - spans 2 columns */}
  <div className="col-span-2 row-span-2 bg-card rounded-3xl p-8">
    Large Feature
  </div>
  
  {/* Standard cards */}
  <div className="col-span-1 row-span-1 bg-card rounded-3xl p-6">
    Small 1
  </div>
  <div className="col-span-1 row-span-1 bg-card rounded-3xl p-6">
    Small 2
  </div>
  <div className="col-span-2 row-span-1 bg-card rounded-3xl p-6">
    Wide Bottom
  </div>
</div>
```

### Pattern: Apple-Style Bento

```tsx
<div className="grid grid-cols-3 gap-6">
  {/* Row 1: 2 + 1 */}
  <div className="col-span-2 aspect-[2/1] bg-card rounded-3xl" />
  <div className="col-span-1 aspect-square bg-card rounded-3xl" />
  
  {/* Row 2: 1 + 2 (inverted) */}
  <div className="col-span-1 aspect-square bg-card rounded-3xl" />
  <div className="col-span-2 aspect-[2/1] bg-card rounded-3xl" />
</div>
```

### Responsive Bento

```tsx
<div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
  <div className="md:col-span-2 lg:col-span-2 lg:row-span-2">Feature</div>
  <div>Standard</div>
  <div>Standard</div>
  <div className="md:col-span-2">Wide</div>
</div>
```

---

## Broken Grid (Items Escape Container)

Content breaks the expected boundaries for visual tension.

### Pattern: Image Bleeds Out

```tsx
<section className="relative py-20 overflow-visible">
  <div className="max-w-7xl mx-auto px-8">
    <div className="grid lg:grid-cols-2 gap-16 items-center">
      {/* Text stays in grid */}
      <div>
        <h2>Breaking Boundaries</h2>
        <p>Content here...</p>
      </div>
      
      {/* Image breaks right edge */}
      <div className="relative lg:absolute lg:right-0 lg:w-[55%] lg:-mr-[10%]">
        <img src="/image.jpg" className="w-full rounded-l-3xl" />
      </div>
    </div>
  </div>
</section>
```

### Pattern: Text Over Image Edge

```tsx
<div className="relative">
  <img src="/bg.jpg" className="w-full h-[600px] object-cover" />
  
  {/* Text box breaks image boundary */}
  <div className="absolute -bottom-16 left-8 right-8 lg:left-16 lg:right-auto lg:w-1/2">
    <div className="bg-background p-8 rounded-2xl shadow-2xl">
      <h3>Overlapping Content</h3>
      <p>Creates depth and visual interest</p>
    </div>
  </div>
</div>
```

---

## Overlap Pattern (Intentional Layering)

Elements deliberately overlap to create depth.

### Pattern: Card Stack

```tsx
<div className="relative h-[500px]">
  {/* Back card */}
  <div className="absolute top-0 left-0 w-[80%] h-[400px] bg-muted rounded-3xl" />
  
  {/* Front card - offset */}
  <div className="absolute top-16 left-16 w-[80%] h-[400px] bg-card rounded-3xl shadow-2xl" />
  
  {/* Floating element */}
  <div className="absolute top-32 right-0 w-48 h-48 bg-primary rounded-2xl" />
</div>
```

### Pattern: Image + Text Overlap

```tsx
<div className="relative">
  <div className="w-[70%] h-[400px]">
    <img src="/image.jpg" className="w-full h-full object-cover rounded-3xl" />
  </div>
  
  {/* Text card overlapping image */}
  <div className="absolute top-1/2 right-0 transform -translate-y-1/2 w-[50%] bg-background p-8 rounded-2xl shadow-xl">
    <h3>Overlapping Text</h3>
    <p>Creates visual hierarchy</p>
  </div>
</div>
```

---

## Asymmetric Split

Breaking the 50/50 rule for more dynamic compositions.

### Pattern: 60/40 Split

```tsx
<section className="grid lg:grid-cols-5 gap-8 items-center">
  {/* 60% - 3 columns */}
  <div className="lg:col-span-3">
    <img src="/hero.jpg" className="rounded-3xl" />
  </div>
  
  {/* 40% - 2 columns */}
  <div className="lg:col-span-2">
    <h1>Asymmetric Balance</h1>
    <p>More visual interest than 50/50</p>
  </div>
</section>
```

### Pattern: 70/30 Extreme

```tsx
<section className="grid lg:grid-cols-10 gap-4">
  <div className="lg:col-span-7">Main Content Area</div>
  <div className="lg:col-span-3">Sidebar / CTA</div>
</section>
```

### Pattern: Offset Vertical

```tsx
<div className="grid lg:grid-cols-2 gap-8">
  {/* Left column - normal */}
  <div className="pt-0">Content 1</div>
  
  {/* Right column - pushed down */}
  <div className="pt-32 lg:pt-48">Content 2</div>
</div>
```

---

## Magazine Layout (Mixed Density)

Varying text and image density like editorial design.

### Pattern: Feature Article

```tsx
<article className="grid lg:grid-cols-12 gap-8">
  {/* Full-width hero */}
  <div className="col-span-12">
    <img src="/hero.jpg" className="w-full aspect-[21/9] object-cover rounded-3xl" />
  </div>
  
  {/* Title area - offset */}
  <div className="col-span-12 lg:col-span-8 lg:col-start-3">
    <h1 className="text-7xl font-bold">Feature Title</h1>
    <p className="text-xl text-muted-foreground mt-4">Subtitle text here</p>
  </div>
  
  {/* Body - narrow column */}
  <div className="col-span-12 lg:col-span-6 lg:col-start-4">
    <p className="text-lg leading-relaxed">Body content...</p>
  </div>
  
  {/* Pull quote - breaks out */}
  <div className="col-span-12 lg:col-span-10 lg:col-start-2 py-16">
    <blockquote className="text-4xl font-light italic text-center">
      "A pull quote that breaks the column width"
    </blockquote>
  </div>
</article>
```

---

## Practical CSS Variables for Layouts

Define in `globals.css`:

```css
:root {
  --grid-gap-tight: 1rem;     /* 16px */
  --grid-gap-normal: 2rem;    /* 32px */
  --grid-gap-loose: 3rem;     /* 48px */
  
  --radius-card: 1.5rem;      /* 24px - modern rounded */
  --radius-card-lg: 2rem;     /* 32px - extra rounded */
  
  --overlap-offset: 4rem;     /* 64px - overlap amount */
  --bleed-amount: 10%;        /* how far to bleed out of container */
}
```

---

## Layout Selection Guide

| Goal | Pattern | Key Properties |
|:-----|:--------|:---------------|
| Show multiple features | Bento Grid | `grid-cols-4`, mixed spans |
| Create tension | Broken Grid | `overflow-visible`, negative margins |
| Add depth | Overlap | `absolute`, `z-index`, `shadow-2xl` |
| Dynamic hero | Asymmetric Split | `grid-cols-5`, `col-span-3` |
| Editorial feel | Magazine | Variable column widths |
