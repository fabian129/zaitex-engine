---
name: component-selector
description: Smart decision framework for choosing Zaitex components
---

# Component Selector

## Objective
Match the right Zaitex component to the design goal through strategic thinking, not prescriptive rules.

## Decision Framework

### Question 1: What's the Aesthetic Goal?

#### Technical / Cyberpunk / Futuristic
**Components:**
- `ParticleField` - Vertical falling particles (Matrix-style)
- `GlowingLines` - Horizontal energy lines
- `TextScramble` - Character reveal effect
- `DotGridPattern` - Blueprint/schematic base

**Why:** These create movement and "alive" feeling

#### Premium / Luxury / Sophisticated
**Components:**
- `MeshGradient` - Smooth color transitions
- `ShinyGlassButton` - Reflective surfaces
- `AmbientGlow` - Soft, pulsating backgrounds
- `BorderBeam` - Elegant animated borders

**Why:** Subtle, high-quality feel without being loud

#### Minimal / Clean / Professional
**Components:**
- `DotGridPattern` (low opacity)
- `EdgeFade` - Subtle content fading
- `GridPattern` (static)

**Why:** Structure without distraction

---

### Question 2: Performance Priority?

#### High Performance (Mobile-First)
**Prefer:**
- Static patterns (`DotGridPattern`, `GridPattern`)
- CSS-only effects (`EdgeFade`)
- Minimal JavaScript

**Avoid:**
- Heavy animations (`ParticleField` with 100+ particles)
- Multiple layered effects

#### Showcase (Desktop Experience)
**Embrace:**
- Layered backgrounds (Grid + Lines + Particles)
- Complex animations
- Interactive effects

---

### Question 3: Content Density?

#### Text-Heavy / Information-Dense
**Background:**
- Low opacity (20-30%)
- Subtle patterns only
- No competing motion

**Why:** Background shouldn't fight for attention

#### Sparse / Visual-Focus
**Background:**
- Higher opacity (40-60%)
- Bold, animated effects
- Multiple layers

**Why:** Background becomes part of the experience

---

## Component Combinations (Proven Patterns)

### "Aura Stack" (What We Built)
```tsx
<DotGridPattern opacity={0.4} />
<GlowingLines count={8} opacity={0.4} />
<ParticleField count={60} opacity={0.6} />
<Vignette /> // Radial gradient overlay
```
**When:** Cyberpunk, tech, premium showcase  
**Performance:** Medium (desktop-first)

### "Luxury Minimal"
```tsx
<MeshGradient colors={subtle} slow />
<AmbientGlow soft />
```
**When:** High-end brands, fashion, luxury  
**Performance:** Good (CSS-heavy)

### "Professional Clean"
```tsx
<DotGridPattern opacity={0.15} />
<EdgeFade />
```
**When:** B2B, corporate, consulting  
**Performance:** Excellent (static)

---

## Button Selection

### Primary CTA (Most Important)
**Use:** `ShinyGlassButton variant="primary"`  
**Why:** Premium feel, built-in reflection

### Secondary Actions
**Use:** `ShinyGlassButton variant="secondary"`  
**Why:** Less prominent but consistent style

### Utility Buttons (Close, Nav)
**Use:** Standard `Button` from shadcn  
**Why:** Simpler, faster

---

## Text Effects

### When to Use `TextScramble`
✅ **Good for:**
- Status messages ("System online")
- Version numbers
- Small labels
- Easter eggs

❌ **Bad for:**
- Headlines (hard to read)
- Body text (annoying)
- CTAs (unclear)

---

## The Decision Process

Instead of "Use X", ask:

1. **What's the vibe?** (Technical/Premium/Minimal)
2. **What's the priority?** (Performance/Impact)
3. **How busy is content?** (Text-heavy/Sparse)
4. **What components match?** (Check combinations above)
5. **Validate:** Does this serve the user experience?

## Examples

**Brief:** "SaaS landing page, need to feel cutting-edge but professional"

**Think Through:**
1. Vibe: Technical but not cyberpunk (balance)
2. Priority: Good performance (B2B audience)
3. Content: Medium (features list + hero)
4. Match: DotGrid + GlowingLines (skip ParticleField for performance)
5. Validate: ✓ Feels tech-forward without being overwhelming

**Result:**
```tsx
<DotGridPattern className="opacity-30" />
<GlowingLines count={5} lineColor="blue" />
// Skip particles for performance
```

---

## Key Principle
**Think about the user experience first, component selection second.**
