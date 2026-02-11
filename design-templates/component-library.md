# Component Library

This is your catalog of reusable components. Document each component with usage examples, variants, and visual references.

---

## 🧩 Component Index

- [Buttons](#buttons)
- [Cards](#cards)
- [Hero Sections](#hero-sections)
- [Pricing Tables](#pricing-tables)
- [Forms](#forms)
- [Navigation](#navigation)
- [Visual Effects](#visual-effects)
- [Custom Components](#custom-components)

---

## Buttons

### Primary Button
**Usage**: Main call-to-action buttons

**Variants**:
- Default
- Hover
- Disabled
- Loading

**Code Pattern**:
```tsx
<button className="btn-primary">
  Click Me
</button>
```

**Screenshot**:
<!-- ![Primary Button](../references/component-examples/button-primary.png) -->

---

### Secondary Button
**Usage**: Secondary actions, less emphasis than primary

**Code Pattern**:
```tsx
<button className="btn-secondary">
  Learn More
</button>
```

---

## Cards

### Glass Card
**Usage**: Feature cards, content containers with glassmorphism effect

**Code Pattern**:
```tsx
<div className="glass-card">
  <h3>Card Title</h3>
  <p>Card content...</p>
</div>
```

**Screenshot**:
<!-- ![Glass Card](../references/component-examples/glass-card.png) -->

---

## Hero Sections

### Hero Type 1: [Name/Description]
**Usage**: Landing pages, main product pages

**Features**:
- Animated text
- Background effects
- CTA buttons

**Code Location**: [Link to component file]

**Screenshot**:
<!-- ![Hero Example](../references/hero-examples/hero-1.png) -->

---

## Pricing Tables

### Pricing Type 1: [Name/Description]
**Usage**: Pricing pages, subscription tiers

**Features**:
- 3-tier layout
- Highlighted "Popular" option
- Feature comparison

**Code Location**: [Link to component file]

**Screenshot**:
<!-- ![Pricing Example](../references/pricing-examples/pricing-1.png) -->

---

## Forms

### Contact Form
**Usage**: Contact pages, lead generation

**Fields**:
- Name
- Email
- Message

**Code Pattern**:
```tsx
<form className="contact-form">
  {/* Form fields */}
</form>
```

---

## Navigation

### Main Navigation
**Usage**: Site-wide navigation

**Features**:
- Responsive mobile menu
- Smooth scroll
- Active state indicators

---

## Visual Effects

### Available Effects Components

#### Text Scramble
**File**: [`components/zaitex/text-scramble.tsx`](file:///c:/Users/Fabian/Desktop/Antigravity/New%20setup%20test%202/zaitex-test-setup-2/components/zaitex/text-scramble.tsx)

**Usage**: Animated text reveal with scrambling effect

#### Gradient Border
**File**: [`components/zaitex/gradient-border.tsx`](file:///c:/Users/Fabian/Desktop/Antigravity/New%20setup%20test%202/zaitex-test-setup-2/components/zaitex/gradient-border.tsx)

**Usage**: Wrapper component for animated gradient borders

---

## Custom Components

> Add your custom-built components here as you create them

### [Component Name]
**Usage**: [When to use this component]

**Props**:
- `prop1`: Description
- `prop2`: Description

**Code Pattern**:
```tsx
<ComponentName prop1="value" prop2="value" />
```

**Screenshot**:
<!-- ![Component Preview](../references/component-examples/custom-component.png) -->

---

## 📝 Usage Notes

### How to Add New Components

1. **Build the component** in your codebase
2. **Take a screenshot** of the rendered component
3. **Save screenshot** to `.agent/design/references/component-examples/`
4. **Document here** with description, code pattern, and embedded screenshot
5. **Update the Component Index** at the top

### Naming Conventions

- Use descriptive, consistent names
- Prefix with type when helpful (e.g., `GlassCard`, `HeroAnimated`)
- Keep component files organized in logical directories
