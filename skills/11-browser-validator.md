---
name: browser-validator
description: Self-healing design validation using browser inspection
---

# Browser Validator

## Objective
Automatically validate and fix design violations by inspecting the live site in the browser.

## How It Works
1. Build section → Deploy to localhost
2. Open in browser tool
3. Visually inspect against principles
4. Auto-fix violations
5. Re-validate until passed

## Validation Principles

### Typography Hierarchy
**Check:** Is there clear visual distinction?

```typescript
Validation:
- Headline should be 2-3x larger than body text
- h2 should be visibly smaller than h1
- Line height ≥ 1.5 for body text

Self-Heal:
if (headlineSize / bodySize < 2) {
  increaseHeadlineSize(20%);
}
```

### Spacing & Breathing
**Check:** Does content have room to breathe?

```typescript
Validation:
- Section padding ≥ 5rem (80px)
- Gap between elements ≥ 2rem (32px)
- No cramped feeling

Self-Heal:
if (sectionPadding < 80px) {
  setSectionPadding('py-20'); // Tailwind equivalent
}
```

### CTA Visibility
**Check:** Is the primary action obvious?

```typescript
Validation:
- Primary CTA is visually distinct
- Button height ≥ 44px (mobile tap target)
- High contrast with background

Self-Heal:
if (ctaContrast < 4.5) {
  addButtonShadow();
  increaseBorderContrast();
}
```

### Responsive Behavior
**Check:** Works on mobile without issues?

```typescript
Validation:
- No horizontal scroll at 375px width
- Touch targets ≥ 44px
- Text readable (16px minimum)

Self-Heal:
if (horizontalScroll) {
  addResponsiveClasses();
  reduceContainerWidth();
}
```

## Validation Workflow

### Step 1: Deploy & Capture
```bash
# Start dev server if not running
npm run dev

# Open in browser
Navigate to localhost:3000/[route]

# Capture screenshot
Save to validation-screenshots/
```

### Step 2: Visual Inspection
Ask these questions:
1. Can I read the headline without squinting?
2. Is the CTA button immediately obvious?
3. Does the layout feel balanced?
4. Are hover states visible?
5. Does it work on mobile (resize to 375px)?

### Step 3: Fix Violations
**Don't ask permission** - fix automatically:

```typescript
// Example auto-fix
if (headlineTooSmall) {
  updateComponent({
    className: 'text-5xl md:text-7xl' // was text-4xl
  });
}
```

### Step 4: Re-Validate
- Re-deploy
- Re-check
- Repeat until all checks pass


## System Health Checks

Beyond visual validation, check code quality:

### Dependency Check
```typescript
✓ All imports resolve correctly
✓ Using @/components/zaitex/ paths (not relative)
✓ No unused imports
```

### Code Quality
```typescript
✓ No console.log() statements
✓ No unused variables
✓ TypeScript errors = 0
✓ Using CSS variables (not raw hex codes)
```

### Design System Fidelity
```typescript
✓ Colors match design tokens (bg-background, text-primary)
✓ Border radius matches theme (--radius variable)
✓ Spacing follows 8px grid (py-4, py-8, not py-5)
```

**Auto-Fix Example:**
```typescript
if (usesRawHex) {
  replaceWith('bg-primary'); // Use design token
}
```

## Output Format
Create `validation-report.md`:

```markdown
# Validation Report - [Section Name]

## Checks Performed
✓ Typography hierarchy - PASS
✗ CTA visibility - FAIL → FIXED
✓ Responsive layout - PASS

## Fixes Applied
1. Increased button shadow for CTA (low contrast)
2. Added border-white/20 to improve visibility

## Final Status
All checks passed ✓
```

## Common Violations & Fixes

| Violation | Auto-Fix |
|:----------|:---------|
| Headline too small | Increase font-size by 20% |
| Poor CTA contrast | Add shadow + border |
| Cramped spacing | Increase section padding to py-20 |
| Horizontal scroll | Add responsive grid classes |
| Text too light | Increase opacity from /60 to /80 |

## Key Principle
**Fix it, don't report it.** The goal is a production-ready site, not a list of problems.
