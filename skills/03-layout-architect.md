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
