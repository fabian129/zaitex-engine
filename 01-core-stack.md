# Zaitex Engine — Core Stack & Standards
**Version:** 2.0

This document defines the mandatory environment configuration for any project using the Zaitex Engine.

---

## 📦 Mandatory Dependencies

```bash
# Core UI & Motion
npm install framer-motion lenis lucide-react class-variance-authority clsx tailwind-merge

# 3D Experience (Three.js + Drei Helpers)
npm install three @react-three/fiber @react-three/drei
npm install -D @types/three

# Advanced Scrolly-telling (GSAP)
npm install gsap @gsap/react
```

---

## 🛡️ Robust Component Patterns

### 1. Canvas & Ref Handling
**Problem:** TypeScript strict mode often flags canvas access as "possibly null."

**Standard Pattern:**
- Do not rely on closure capture of `ref.current` inside classes.
- Explicitly pass `width`, `height`, and `context` to update/draw methods.
- Ensure `useEffect` cleanup handles listener removal.

### 2. Polymorphic Components
**Problem:** Dynamic `as` props can cause type errors.

**Standard Pattern:**
- Use `const Comp = as as any;` casting inside the component body if generic typing becomes overly restrictive.

### 3. Image Optimization
**Problem:** Large unoptimized images cause performance issues.

**Standard Pattern:**
- Always use `next/image` with `fill`, `sizes`, and `priority` props.
- Images larger than 2MB should be resized before committing.
- Use `unoptimized` only as a last resort for extremely large images.

---

## 🏗️ Build Verification

Always run the following check before confirming a feature complete:

```bash
npm run build
```

**Reason:** Dev server (Turbopack) is permissive; Production build is strict.

---

## 📁 Required Project Structure

```
project-root/
├── .agent/                    # Agent configuration
│   ├── core/                  # Universal skills & templates
│   ├── design/                # Project-specific DNA
│   └── project/               # Content & assets
├── components/
│   ├── ui/                    # shadcn components
│   ├── sections/              # Page sections
│   └── decorations/           # Visual effects
├── app/                       # Next.js App Router
├── lib/                       # Utilities
└── public/
    └── images/                # Optimized images only
```
