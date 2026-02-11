# How to Use the Design Reference System

This guide explains how to use the `.agent/design/` structure to manage design inspiration and build reusable components.

---

## 📁 Directory Structure

```
.agent/design/
├── active-dna.md          # Your main style guide
├── component-library.md      # Catalog of reusable components
└── references/               # Screenshot storage
    ├── hero-examples/        # Hero section inspiration
    ├── pricing-examples/     # Pricing layout inspiration
    ├── component-examples/   # Button, card, form examples
    └── misc/                 # Other design references
```

---

## 🎨 Workflow: From Inspiration to Component

### Step 1: Find Inspiration
Browse sites like:
- [Dribbble](https://dribbble.com)
- [Awwwards](https://www.awwwards.com)
- [Behance](https://www.behance.net)
- [Land-book](https://land-book.com)
- Real production websites you admire

### Step 2: Save Screenshots
When you find a design you like:

1. **Take a screenshot** (Windows: `Win + Shift + S`)
2. **Save to the appropriate folder**:
   ```
   .agent/design/references/hero-examples/dribbble-hero-1.png
   .agent/design/references/pricing-examples/stripe-pricing.png
   .agent/design/references/component-examples/glassmorphism-card.png
   ```
3. **Use descriptive filenames** so you remember what they are

### Step 3: Document in active-dna.md
Open `active-dna.md` and add your reference:

```markdown
## 🖼️ Design References

### Hero Sections

![Modern SaaS Hero](file:///c:/Users/Fabian/Desktop/Antigravity/New%20setup%20test%202/zaitex-test-setup-2/.agent/design/references/hero-examples/dribbble-hero-1.png)
*Reference: Dribbble - Clean hero with animated gradient background*

### Component Examples

![Glassmorphism Card](file:///c:/Users/Fabian/Desktop/Antigravity/New%20setup%20test%202/zaitex-test-setup-2/.agent/design/references/component-examples/glassmorphism-card.png)
*Reference: Frosted glass card with blur effect*
```

**Important**: Use absolute paths and the `file:///` protocol so I can see the images!

### Step 4: Request the Build
Now you can simply say:

> "Build me a hero section like the one in active-dna.md under Hero Sections"

Or:

> "Create a pricing section similar to the Stripe reference in .agent/design/references/"

---

## 🎯 Using active-dna.md

### Define Your Style
As you build components, extract common patterns:

**Colors**: After building a few sections, you'll notice which colors you use repeatedly. Document them:
```markdown
## 🎨 Color Palette
Primary: #6366F1 (Indigo)
Accent: #EC4899 (Pink)
Background: #0F172A (Dark Blue)
```

**Typography**: Document your font choices:
```markdown
## 📝 Typography
Heading: 'Inter', sans-serif
Body: 'Inter', sans-serif
Display: 'Space Grotesk', sans-serif
```

**Spacing**: Establish consistent spacing:
```markdown
Section padding: 96px vertical, 24px horizontal
Card gap: 24px
Element spacing: 16px
```

### Reference Existing Styles
When asking me to build something new:

> "Use the color palette from active-dna.md"
> "Match the typography in active-dna.md"

---

## 📚 Using component-library.md

### Document Components You Build
After I build a component for you, document it:

```markdown
## Hero Sections

### Animated Hero with Gradient
**Usage**: Main landing page hero
**Features**: 
- Text scramble animation
- Gradient background
- CTA buttons with hover effects

**Code Location**: `app/page.tsx` (lines 10-45)

**Screenshot**:
![Hero Preview](file:///path/to/screenshot.png)

**When to reuse**: Any landing page needing dramatic entrance
```

### Reuse Components
Next time you need a similar component:

> "Build me a hero like 'Animated Hero with Gradient' from component-library.md"

---

## 💡 Pro Tips

### 1. Organize by Type
Keep screenshots organized:
- `hero-examples/` - Full-width hero sections
- `pricing-examples/` - Pricing tables and cards
- `component-examples/` - Buttons, forms, cards, etc.
- `misc/` - Full page layouts, navigation, footers

### 2. Use Descriptive Names
❌ `screenshot1.png`
✅ `dribbble-glassmorphism-card.png`

### 3. Add Context
When documenting, include:
- Where you found it
- What you like about it
- When to use it

### 4. Build a Design Language
After 3-4 projects, you'll have a consistent style. Document it in `active-dna.md` so every project feels cohesive.

### 5. Link Everything
Use markdown links to connect:
- Components to their code files: `[see code](file:///path/to/component.tsx)`
- Screenshots to active-dna.md
- Component library to actual implementations

---

## 🚀 Quick Start Example

Let's say you found an amazing hero on Dribbble:

1. **Save screenshot**: `.agent/design/references/hero-examples/dribbble-dark-hero.png`

2. **Document it**:
   ```markdown
   # In active-dna.md
   ### Hero Sections
   ![Dark Animated Hero](file:///c:/Users/Fabian/Desktop/Antigravity/New%20setup%20test%202/zaitex-test-setup-2/.agent/design/references/hero-examples/dribbble-dark-hero.png)
   ```

3. **Request the build**:
   > "Build a hero section matching the 'Dark Animated Hero' reference in active-dna.md"

4. **After I build it, document the result**:
   ```markdown
   # In component-library.md
   ### Dark Animated Hero
   **Built**: 2026-01-28
   **Code**: app/page.tsx
   **Features**: Mesh gradient background, text scramble, dual CTAs
   ![Final Result](file:///path/to/final-screenshot.png)
   ```

---

## 📞 Working Together

### When Asking Me to Build:
✅ "Build a pricing section like the one in `.agent/design/references/pricing-examples/stripe.png`"
✅ "Use the color palette from active-dna.md"
✅ "Make it match the style in component-library.md > Glass Card"

### I'll Do This:
1. Open and view your reference images
2. Extract the design patterns
3. Build the component matching your documented style
4. Suggest updates to active-dna.md and component-library.md

---

You're all set! Start collecting designs you love, and we'll build them together! 🎨✨
