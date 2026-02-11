---
name: Style Propagator
description: Ensures global style consistency across all pages by using shared configuration and component patterns.
---

# Style Propagator

## Objective
When a design decision is made (e.g., "Hero icons should have a glow effect"), that decision must propagate to **all** pages automatically, without manually updating each one.

---

## The Problem It Solves

**Scenario:**
1. You build a Hero with animated icons on the homepage.
2. You build service pages with similar functionality.
3. You decide to change the icon color from green to blue.
4. **Without Style Propagator:** You manually edit 6 files.
5. **With Style Propagator:** You change 1 config file, all pages update.

---

## Architecture

### Level 1: Design Tokens (CSS Variables)

All colors, fonts, and spacing are defined in `globals.css` and referenced everywhere.

**File:** `app/globals.css`
```css
:root {
  --color-primary: #22C55E;
  --color-primary-glow: rgba(34, 197, 94, 0.3);
  --font-heading: 'DM Sans', sans-serif;
  --radius-card: 1.5rem;
  --shadow-card: 0 4px 20px rgba(0,0,0,0.08);
}
```

**Usage:**
```tsx
// ✅ Correct - uses variable
<div className="bg-primary shadow-card" />

// ❌ Wrong - hardcoded
<div className="bg-[#22C55E]" />
```

---

### Level 2: Shared Component Config

For complex patterns (animations, interaction styles), create a config file.

**File:** `lib/style-config.ts`
```typescript
export const heroConfig = {
  animation: {
    entrance: { initial: { opacity: 0, y: 20 }, animate: { opacity: 1, y: 0 } },
    duration: 0.6,
    stagger: 0.1,
  },
  iconStyle: {
    size: 'w-6 h-6',
    color: 'text-primary',
    glowOnHover: true,
  },
  backgroundLayers: ['GridPattern', 'OrganicBlob'],
};

export const cardConfig = {
  radius: 'rounded-3xl',
  shadow: 'shadow-xl shadow-black/5',
  hoverEffect: 'hover:shadow-2xl hover:-translate-y-1 transition-all duration-300',
};
```

**Usage in Components:**
```tsx
import { heroConfig, cardConfig } from '@/lib/style-config';

export function HeroSection() {
  return (
    <motion.div {...heroConfig.animation.entrance}>
      <Icon className={cn(heroConfig.iconStyle.size, heroConfig.iconStyle.color)} />
    </motion.div>
  );
}

export function ServiceCard() {
  return (
    <div className={cn(cardConfig.radius, cardConfig.shadow, cardConfig.hoverEffect)}>
      {/* content */}
    </div>
  );
}
```

---

### Level 3: Shared Section Components

For sections that appear on multiple pages (Header, Footer, CTA Banner), use shared components.

**File Structure:**
```
components/
├── sections/
│   ├── Navbar.tsx           # Used everywhere
│   ├── Footer.tsx           # Used everywhere
│   ├── CTABanner.tsx        # Used on homepage + service pages
│   └── HeroBase.tsx         # Base hero, extended per-page
```

**Pattern for Extendable Sections:**
```tsx
// components/sections/HeroBase.tsx
export function HeroBase({
  title,
  subtitle,
  cta,
  backgroundLayers = heroConfig.backgroundLayers,
  children,
}: HeroBaseProps) {
  return (
    <section className="relative min-h-screen">
      {backgroundLayers.map(Layer => <Layer key={Layer} />)}
      <div className="relative z-10">
        <h1>{title}</h1>
        <p>{subtitle}</p>
        {cta}
        {children}
      </div>
    </section>
  );
}

// app/page.tsx (Homepage)
<HeroBase title="Welcome" subtitle="Premium cleaning" cta={<Button>Book Now</Button>}>
  <FeaturedServices />
</HeroBase>

// app/tjanster/[slug]/page.tsx (Service Page)
<HeroBase title={service.title} subtitle={service.description} cta={<Button>Get Quote</Button>} />
```

---

## Propagation Checklist

When making a style change, ask:

| Question | If Yes |
|:---------|:-------|
| Is this a color/font/spacing? | Update `globals.css` variables |
| Is this an animation/interaction pattern? | Update `lib/style-config.ts` |
| Is this a section that appears multiple times? | Use a shared component |
| Is this page-specific? | OK to keep local, but document it |

---

## The "Single Source of Truth" Rule

**Every design decision should have exactly ONE place where it's defined.**

- Colors → `globals.css`
- Animations → `lib/style-config.ts`
- Section layouts → Shared components
- Project DNA → `.agent/design/active-dna.md`

---

## Active DNA File

The project's current visual DNA should be summarized in one file that the agent references.

**File:** `.agent/design/active-dna.md`
```markdown
# Active DNA — [Project Name]

## 🎨 Color Palette

### Primary Colors
Brand Primary: [hex]
Brand Secondary: [hex]
Accent: [hex]

### Neutral Colors
Background: [hex]
Foreground: [hex]
Muted: [hex]
Border: [hex]

### Semantic Colors
Success: [hex]
Warning: [hex]
Error: [hex]
Info: [hex]

## 📝 Typography

### Font Families
Heading: [Font Name]
Body: [Font Name]
Mono: [Font Name]

### Type Scale
Display: 72px / 4.5rem
H1: 48px / 3rem
H2: 36px / 2.25rem
H3: 30px / 1.875rem
H4: 24px / 1.5rem
Body Large: 18px / 1.125rem
Body: 16px / 1rem
Body Small: 14px / 0.875rem
Caption: 12px / 0.75rem

### Font Weights
Light: 300
Regular: 400
Medium: 500
Semibold: 600
Bold: 700

## 📐 Spacing System
xs: 4px
sm: 8px
md: 16px
lg: 24px
xl: 32px
2xl: 48px
3xl: 64px
4xl: 96px

## ✨ Visual Effects

### Shadows
shadow-sm: [value]
shadow-md: [value]
shadow-lg: [value]
glow: [value]

### Glassmorphism
backdrop-filter: blur([value])
background: rgba([values])
border: [value]

### Gradients
gradient-1: [value]
gradient-2: [value]

## 🎬 Motion DNA

### Intensity Level: [Subtle / Expressive / Luxury]
Scroll: [Native / Lenis Smooth]
Hover: [Lift + Shadow / Magnetic / Scale]
Entrance: [Fade up / Clip reveal / Stagger]
Easing: [cubic-bezier value]

### Duration
Fast: 150ms
Normal: 300ms
Slow: 500ms

## 📱 Breakpoints
mobile: 640px
tablet: 768px
desktop: 1024px
wide: 1280px

## 🔑 Signatures (What Makes This Project Unique)
Cards: [ex. Sharp corners, 1px border, no shadow]
Buttons: [ex. Pill shape, shimmer on hover]
Backgrounds: [ex. Noise overlay + dot grid, no particles]
Layout: [ex. Asymmetric 60/40, generous whitespace]
Icons: [ex. Lucide, 24px, stroke-width 1.5]
Hover: [ex. All cards lift + shadow grow, CTAs get glow]

## 🎯 Design Principles
1. [First principle]
2. [Second principle]
3. [Third principle]

## 🖼️ Design References
[Links or descriptions of approved reference sites/images]
```

---

## Integration Points

### Before building any section
Check `active-dna.md` and `lib/style-config.ts`.

### After making a style change
Update the config, not individual components.

### When building underpages
Import from shared sections, don't recreate.

---

## Key Principle
**Change once, update everywhere.** No design decision should require touching more than one file.
