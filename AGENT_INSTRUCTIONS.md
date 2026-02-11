# Zaitex Engine — Agent Instructions

This document defines how AI agents should operate when building websites using the Zaitex Engine.

---

# PART 1 — BASE OPERATIONS (All Projects)

## 🎯 Core Philosophy

**You are not just writing code. You are crafting premium digital experiences.**

Every decision should serve:
1. **Visual Excellence** — Sites should look Awwwards-worthy
2. **User Experience** — Premium feel, smooth interactions
3. **Maintainability** — Clean code, documented decisions
4. **Performance** — Fast loads, smooth animations

---

## 📋 Before Starting Any Work

### 1. Read the DNA
Always check `.agent/design/active-dna.md` for:
- Color palette (Primary, Neutral, Semantic)
- Typography system (Families, Scale, Weights)
- Spacing scale
- Visual effects (Shadows, Glass, Gradients)
- Motion DNA (Intensity, Scroll, Hover, Entrance)
- Signatures (Cards, Buttons, Backgrounds, Layout)
- Design principles

### 2. Check Existing Components
Before building new, search for existing solutions:
- `components/` folder
- Section templates in `.agent/core/section-templates/`

### 3. Understand the Client Type
| Type | Style | Motion | Typical Layout |
|:-----|:------|:-------|:---------------|
| Corporate | Clean, professional | Subtle | Grid, symmetric |
| Creative/Agency | Bold, experimental | Expressive | Bento, broken grid |
| E-commerce | Conversion-focused | Minimal | Product grids |
| Restaurant/Hospitality | Warm, inviting | Smooth | Full-bleed images |
| Tech/SaaS | Modern, technical | Magnetic, spring | Asymmetric |

---

## 🔧 Skill Reference

| Skill | When to Use |
|:------|:------------|
| `01-design-director` | Setting overall direction |
| `02-page-planner` | Planning page structure |
| `03-layout-architect` | Choosing layouts (bento, grids, etc.) |
| `04-component-selector` | Picking components |
| `05-component-architect` | Building new components |
| `06-motion-choreographer` | Adding animations |
| `07-copywriter` | Writing content |
| `08-performance-guardian` | Optimizing speed |
| `09-style-propagator` | Ensuring DNA consistency |
| `10-accessibility-auditor` | Checking a11y |
| `11-browser-validator` | Testing browsers |
| `12-deployment-packager` | Shipping |
| `14-seo-specialist` | SEO (apply during build + audit before deploy) |
| `15-web-debugger` | Debugging issues (decision trees, token-efficient) |

---

## 🎨 Visual Quality Standards

### Hero Sections
- Large, confident typography (min 4rem desktop)
- Clear visual hierarchy
- Single primary CTA
- Consider: background patterns, gradients, subtle motion

### Cards & Grids
- Use Bento for variety (mixed card sizes)
- Consistent border radius from DNA
- Hover states are mandatory
- Consider: stagger animations, magnetic effects

### Images
- Never stretch or distort
- Always specify aspect ratios
- Consider: reveal animations, parallax, grain overlays

### Motion
- Entrance: fade + subtle translate
- Hover: scale 1.02-1.05, lift shadow
- Scroll: parallax only when intentional
- Always respect `prefers-reduced-motion`

---

## ⚡ Performance Rules
1. **Images:** Max 200KB per image, use WebP
2. **Fonts:** Max 3 weights per family
3. **Animations:** Use `transform` and `opacity` only
4. **Filters:** No animated feTurbulence or per-element SVG filters. Static noise overlay (opacity ≤ 0.05) is OK.
5. **Bundle:** Lazy load below-fold sections

---

## 🔄 Decision Making Process
```
1. What is the GOAL of this section?
   └── Convert? Inform? Impress? Build trust?

2. What PATTERN serves that goal?
   └── Reference layout-architect for options

3. What MOTION level fits the DNA?
   └── Check motion-choreographer for intensity

4. What COMPONENTS already exist?
   └── Don't rebuild what's there

5. Does it FEEL premium?
   └── If not, iterate
```

---

## 📝 Communication Style
- Be concise
- State what's done, not what you'll do
- Flag blockers immediately
- Ask specific questions when unsure
- Don't guess on brand decisions

---

## 📦 File Hygiene
```
components/
├── ui/              # Base components (Button, Card, etc.)
├── sections/        # Page sections (Hero, Features, etc.)
└── layout/          # Navbar, Footer, etc.

public/
├── assets/
│   ├── images/
│   └── videos/
└── favicon/

.agent/
├── core/            # Universal engine (don't modify per-project)
└── design/          # Project-specific DNA
```

---

## 🎯 Quality Checklist
Before marking work as complete:

- [ ] Follows DNA (colors, fonts, spacing)
- [ ] Responsive (mobile, tablet, desktop)
- [ ] Accessible (keyboard, screen reader)
- [ ] Performant (no layout shifts, fast load)
- [ ] Motion respects reduced-motion
- [ ] No console errors
- [ ] Clean code (ESLint passing)
- [ ] SEO: Meta tags, single H1, alt texts, schema markup

---

# PART 2 — ADVANCED OPERATIONS (3D / Interactive Projects Only)

> **Activate this section when:** User requests 3D scenes, immersive effects, or complex interactive experiences.

## Additional Skill

| Skill | When to Use |
|:------|:------------|
| `13-immersive-architect` | 3D scenes, organic effects, mouse interactions |

---

## 🚦 Operating Modes

### AUTO Mode (Default for 3D)
- Agent picks optimal values based on scene calibration
- Minimal Leva controls exposed
- Goal: 80% done, user tweaks 20%

### TWEAK Mode
- Full Leva controls exposed
- Calibrated ranges based on scene measurements
- **Trigger:** User says "give me full controls" or "TWEAK mode"

---

## 🎨 Color States

### SANDBOX
- Any colors allowed
- Full color pickers in Leva
- **Use for:** Testing materials, exploring looks

### BRAND-LOCK
- Colors from DNA only
- **Use for:** Production builds, client deliverables

---

## 🚨 Crystallize Checkpoint
When 3D work feels messy, ask yourself:

**RED FLAGS (Consider Reset):**
- Am I constantly working around earlier mistakes?
- Are there 3+ "temporary fixes" in the code?
- Did we just discover a fundamentally better approach?

**GREEN FLAGS (Keep Going):**
- Core architecture is still sound
- We're just adding features
- Messy code is isolated to one component

If RED > GREEN, propose a reset to the user.

---

## 📦 Additional File Structure (3D)
```
components/
└── scenes/          # 3D components

public/
└── assets/
    └── models/      # 3D models (.glb)
```

---

## ⚡ 3D Performance Rules
- Max 50k triangles per scene
- Textures: 1024×1024 max (512 for mobile)
- Always provide static fallback image
