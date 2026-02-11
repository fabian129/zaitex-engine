---
name: Performance Guardian
description: Enforces performance best practices for images, animations, and rendering to ensure smooth 60fps experiences.
---

# Performance Guardian

## Objective
Ensure every component and page achieves optimal performance, especially on mobile devices. This skill runs as a **mandatory checkpoint** before any section is considered "done."

---

## Pre-Commit Checklist

### 1. Image Optimization ✓

| Check | Rule |
|:------|:-----|
| Using `next/image`? | All images MUST use `next/image`, not `<img>` |
| Has `sizes` prop? | MUST have `sizes` for responsive loading |
| Has `priority`? | Above-fold images need `priority={true}` |
| File size < 500KB? | Resize/compress before committing |
| Format is WebP/AVIF? | Prefer modern formats |

**Auto-Fix Pattern:**
```tsx
// ❌ Bad
<img src="/hero.jpg" alt="Hero" />

// ✅ Good
<Image 
  src="/hero.jpg" 
  alt="Hero" 
  fill 
  sizes="100vw" 
  priority 
  className="object-cover"
/>
```

---

### 2. Animation Performance ✓

| Check | Rule |
|:------|:-----|
| Using transform properties? | Only `x`, `y`, `scale`, `rotate`, `opacity` |
| Avoid layout triggers? | Never animate `width`, `height`, `top`, `left` |
| `will-change` hint? | Add for parallax/scroll-linked elements |
| Reduced motion support? | Wrap heavy animations in `useReducedMotion()` |

**Auto-Fix Pattern:**
```tsx
// ❌ Bad - causes layout thrashing
<motion.div animate={{ width: "100%", left: 0 }} />

// ✅ Good - GPU accelerated
<motion.div animate={{ x: 0, scale: 1 }} />
```

---

### 3. Expensive Effects ✓

| Effect | Status | Alternative |
|:-------|:-------|:------------|
| `feTurbulence` SVG (animated or per-element) | ❌ AVOID | Use CSS noise texture or static PNG |
| `feTurbulence` SVG (static overlay, opacity ≤ 0.05) | ✅ OK | NoiseOverlay component — adds analog warmth without performance cost |
| Complex `blur()` on large elements | ⚠️ LIMIT | Use `blur(10px)` max, not `blur(60px)` |
| Multiple stacked filters | ❌ AVOID | Combine into single effect |
| Canvas animations | ⚠️ MONITOR | Limit to 60fps, cleanup on unmount |

---

### 4. Lazy Loading ✓

| Element | Strategy |
|:--------|:---------|
| Below-fold images | `priority={false}` (default) |
| Heavy components | Use `dynamic()` with `ssr: false` |
| 3D scenes | Load after page hydration |
| Videos | Use `loading="lazy"` and `preload="none"` |

**Pattern:**
```tsx
import dynamic from 'next/dynamic';

const Heavy3DScene = dynamic(() => import('@/components/Scene'), {
  ssr: false,
  loading: () => <div className="h-[600px] bg-muted animate-pulse" />
});
```

---

### 5. Bundle Size ✓

| Check | Rule |
|:------|:-----|
| Three.js used? | Only import what you need from `@react-three/drei` |
| Icons | Import individual icons, not entire packs |
| Fonts | Limit to 2-3 weights per font family |

---

## Runtime Checks

### Lighthouse Targets
- **Performance**: > 90
- **LCP** (Largest Contentful Paint): < 2.5s
- **FID** (First Input Delay): < 100ms
- **CLS** (Cumulative Layout Shift): < 0.1

### Console Warnings
Check for and eliminate:
- "Image could not be decoded"
- "Consider using next/image"
- "Large layout shift detected"
- "[Violation] 'requestAnimationFrame' handler took Xms"

---

## Integration Points

### After `06-motion-choreographer`
Performance Guardian reviews all animations added.

### Before `11-browser-validator`
No component passes to visual QA without performance sign-off.

---

## Output Format

When run, append to build notes:

```markdown
## Performance Check - [Component Name]
✓ Images: All using next/image with sizes
✓ Animations: GPU-accelerated transforms only
✓ Effects: No expensive filters detected
✓ Lazy Loading: Heavy components deferred
✓ Bundle: No unnecessary imports
```

---

## Key Principle
**Smooth beats fancy.** A simple, fast interface always wins over a laggy, complex one.
