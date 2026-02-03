---
name: Accessibility Auditor
description: Expert in ensuring WCAG compliance, contrast ratios, and visual readability.
---

# Accessibility Auditor Skill

## Objective
Ensure the digital product is accessible to all users (inclusive design) while optimizing visual clarity and readability.
**Core Standard**: WCAG 2.1 Level AA (minimum) / AAA (target).

## Analysis Workflow

### 1. Contrast & Color Audit
**Goal**: Eliminate "Invisible Text" and ensure readability.
*   **Check**: Are we using light text on light backgrounds?
*   **Action**: Scan for `text-white` or `text-slate-50` on `bg-white`, `bg-stone-50`, or `bg-background`.
*   **Rule**: Small text must have 4.5:1 contrast. Large text (bold 18pt+) must have 3:1.
    *   *Bad*: White text on Beiges/Light Greys.
    *   *Good*: `text-slate-900` or `text-primary` (if dark enough) on Light backgrounds.

### 2. Semantic Structure
**Goal**: Screen readers must understand the layout.
*   **Check**: Are headings (h1-h6) in logical order?
*   **Check**: Do buttons have descriptive labels (aria-labels if icon-only)?
*   **Check**: Do images have `alt` text? (Decorative images should have empty `alt=""`).

### 3. Visual Optimization (The "Sizzle")
**Goal**: Accessibility shouldn't be boring. It should improve the design.
*   **Spacing**: Is there enough "breathing room" (whitespace) for focus?
*   **Touch Targets**: Are buttons at least 44x44px for mobile users?
*   **Focus States**: Do interactive elements have visible focus rings (`focus-visible:ring`)?

## Implementation Strategy

### Pattern: The "Theme Switch"
When flipping a section from Dark to Light (e.g., in a redesign):
1.  **Inverse Text**: Change `text-white` -> `text-foreground` (or `text-slate-900`).
2.  **Inverse Muted**: Change `text-white/80` -> `text-secondary` (or `text-slate-600`).
3.  **Check Accents**: Ensure icon colors (`text-primary`) still pop against the new background.

### Routine
1.  **Scan** the file for color utility classes.
2.  **Identify** the container background color.
3.  **Verify** the text color contrasts.
4.  **Fix** immediately if failing WCAG AA.

## Example Fix
**Problem**:
```tsx
<section className="bg-stone-50"> {/* Light Background */}
  <h2 className="text-white">Our Services</h2> {/* INVISIBLE! */}
</section>
```

**Solution**:
```tsx
<section className="bg-stone-50">
  <h2 className="text-foreground">Our Services</h2> {/* Fixed */}
</section>
```
