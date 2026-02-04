name: motion-choreographer
description: Expert Motion Designer. Implements advanced physics, scroll-linked animations, and smooth scrolling interactions.
---

# Motion Choreographer Logic

## 1. Objective
Elevate the "feel" of the application from static HTML to a premium, fluid experience. You are responsible for **Physics**, **Scroll Interaction**, and **Micro-Animations**.
You work *after* the Section Builder has laid out the DOM.

## 2. Toolkit (The Motion Stack)
- **Framer Motion**: For all layout transitions and state changes.
- **Lenis (React)**: For smooth, momentum-based scrolling (MANDATORY for "High-End" DNA).
- **CSS Variables**: Use `--transition-spring` (e.g., `cubic-bezier(...)`) for consistency.

## 3. DNA Triggers
Check `design_dna.atomic_mapping.motion`:

### A. Intensity: "Subtle" (Corporate/SaaS)
- **Physics**: Stiff, fast, no bounce.
- **Scroll**: Standard native scroll.
- **Micro**: Fade-in on hover.
- **Execution**:
  - Use `duration: 0.3, ease: "easeInOut"`.
  - No continuous staggered lists.

### B. Intensity: "Expressive" (Tech/Modern)
- **Physics**: Soft spring, slight overshoot.
- **Scroll**: Lenis Smooth Scroll enabled.
- **Micro**: Magnetic buttons, scale-up on hover.
- **Execution**:
  - Use `type: "spring", stiffness: 200, damping: 20`.
  - Implementing `ScrollTrigger` logic (elements slide up as they enter viewport).
  - Wrap entire page in `<ReactLenis root>`.

### C. Intensity: "Luxury" (Fashion/Portfolio)
- **Physics**: Slow, heavy, viscous fluid feel.
- **Scroll**: Slow momentum, parallax images.
- **Micro**: Image reveals with clip-path.
- **Execution**:
  - `duration: 0.8, ease: [0.16, 1, 0.3, 1]`.
  - Parallax: `useScroll` + `useTransform(scrollY, [0, 1000], [0, 200])`.

## 4. The Physics Engine (Contextual Awareness)
Standard motion is "Action -> Reaction". **Contextual Motion** is "Environment -> Reaction".
You must now simulate physical presence.

### A. Velocity-Based Skew (The "Jelly" Effect)
When scrolling fast, content should deform to show speed.
- **Hook:** `useVelocity` -> `useTransform(velocity, [-1000, 1000], [-5, 5])` applied to `skewY`.

### B. Magnetic Fields (The "Gravity" Effect)
Important interactables (Buttons, Cards) should have a gravity well.
- **Behavior:** The element translates `x, y` towards the cursor position within a radius.
- **Result:** The UI feels "sticky" and substantial.

### C. Mouse Parallax (The "Depth" Effect)
The background layers (Atmosphere) should move slightly opposite to mouse movement (`client.x`), creating a 2.5D window effect.

## 5. Implementation Rules
1. **Never block the main thread.** Use specific transform properties (`x`, `y`, `scale`, `opacity`, `rotate`).
2. **Respect Reduced Motion.** Always wrap heavy animations in `useReducedMotion()` checks.
3. **Orchestration.** If a section has >3 items (e.g., Features Grid), ALWAYS use `staggerChildren: 0.1`.

## 5. Output format
You output the *wrapper code* or *hook logic* to wrap existing components.

```tsx
// Example: Parallax Image Wrapper
"use client";
import { motion, useScroll, useTransform } from "framer-motion";
import { useRef } from "react";

export function ParallaxImage({ src, alt }) {
  const ref = useRef(null);
  const { scrollYProgress } = useScroll({ target: ref, offset: ["start end", "end start"] });
  const y = useTransform(scrollYProgress, [0, 1], ["-10%", "10%"]);

  return (
    <div ref={ref} className="overflow-hidden rounded-lg">
      <motion.img style={{ y }} src={src} alt={alt} className="w-full h-full object-cover" />
    </div>
  );
}
```

---

# PART 2 — GSAP ECOSYSTEM (Advanced Scroll)

## When to Use GSAP vs Framer Motion

| Use Case | Tool | Why |
|:---------|:-----|:----|
| Hover/click states | Framer Motion | Simpler, React-native |
| Entrance animations | Framer Motion | `whileInView` is easy |
| Scroll-linked timelines | **GSAP ScrollTrigger** | More powerful, pinning |
| Pinning sections | **GSAP ScrollTrigger** | Framer can't do this |
| Text character animation | **GSAP + SplitType** | Per-letter control |
| Complex sequences | **GSAP Timeline** | Better orchestration |

## Required Packages

```bash
npm install gsap @gsap/react
```

## Setup Pattern

```tsx
"use client";
import { useGSAP } from "@gsap/react";
import gsap from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

export function ScrollSection() {
  useGSAP(() => {
    gsap.to(".animate-me", {
      scrollTrigger: {
        trigger: ".animate-me",
        start: "top 80%",
        end: "bottom 20%",
        scrub: true,
      },
      y: -50,
      opacity: 1,
    });
  });

  return <div className="animate-me opacity-0">Content</div>;
}
```

---

# PART 3 — TEXT ANIMATIONS

## SplitType for Character Animation

```bash
npm install split-type
```

### Pattern: Stagger Text Reveal

```tsx
"use client";
import { useGSAP } from "@gsap/react";
import gsap from "gsap";
import SplitType from "split-type";
import { useRef } from "react";

export function AnimatedHeadline({ children }: { children: string }) {
  const ref = useRef<HTMLHeadingElement>(null);

  useGSAP(() => {
    if (!ref.current) return;
    
    const split = new SplitType(ref.current, { types: "chars" });
    
    gsap.from(split.chars, {
      opacity: 0,
      y: 50,
      rotateX: -90,
      stagger: 0.02,
      duration: 0.8,
      ease: "back.out(1.7)",
    });
  }, []);

  return (
    <h1 ref={ref} className="text-6xl font-bold">
      {children}
    </h1>
  );
}
```

### Pattern: Text Scramble Effect

```tsx
// For "hacker" style text reveals
import { useGSAP } from "@gsap/react";
import gsap from "gsap";
import { TextPlugin } from "gsap/TextPlugin";

gsap.registerPlugin(TextPlugin);

export function ScrambleText({ text }: { text: string }) {
  const ref = useRef<HTMLSpanElement>(null);

  useGSAP(() => {
    gsap.to(ref.current, {
      duration: 1.5,
      text: {
        value: text,
        scrambleText: { chars: "upperCase", revealDelay: 0.5 },
      },
    });
  });

  return <span ref={ref}></span>;
}
```

---

# PART 4 — CLIP-PATH REVEALS

## Pattern: Image Reveal on Scroll

```tsx
"use client";
import { useGSAP } from "@gsap/react";
import gsap from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

export function RevealImage({ src, alt }: { src: string; alt: string }) {
  const containerRef = useRef<HTMLDivElement>(null);

  useGSAP(() => {
    gsap.fromTo(
      containerRef.current,
      { clipPath: "inset(100% 0 0 0)" },
      {
        clipPath: "inset(0% 0 0 0)",
        duration: 1.2,
        ease: "power3.inOut",
        scrollTrigger: {
          trigger: containerRef.current,
          start: "top 80%",
        },
      }
    );
  });

  return (
    <div ref={containerRef} className="overflow-hidden">
      <img src={src} alt={alt} className="w-full h-full object-cover" />
    </div>
  );
}
```

## Clip-Path Vocabulary

| Effect | From | To |
|:-------|:-----|:---|
| Reveal from bottom | `inset(100% 0 0 0)` | `inset(0% 0 0 0)` |
| Reveal from top | `inset(0 0 100% 0)` | `inset(0 0 0% 0)` |
| Reveal from left | `inset(0 100% 0 0)` | `inset(0 0% 0 0)` |
| Circle expand | `circle(0% at 50% 50%)` | `circle(100% at 50% 50%)` |
| Diagonal wipe | `polygon(0 0, 0 0, 0 100%)` | `polygon(0 0, 100% 0, 100% 100%, 0 100%)` |

---

# PART 5 — MAGNETIC CURSOR (Full Implementation)

```tsx
"use client";
import { motion, useMotionValue, useSpring } from "framer-motion";
import { useRef, MouseEvent } from "react";

interface MagneticProps {
  children: React.ReactNode;
  strength?: number;
}

export function Magnetic({ children, strength = 0.3 }: MagneticProps) {
  const ref = useRef<HTMLDivElement>(null);
  const x = useMotionValue(0);
  const y = useMotionValue(0);

  const springX = useSpring(x, { stiffness: 150, damping: 15 });
  const springY = useSpring(y, { stiffness: 150, damping: 15 });

  const handleMouse = (e: MouseEvent) => {
    if (!ref.current) return;
    const rect = ref.current.getBoundingClientRect();
    const centerX = rect.left + rect.width / 2;
    const centerY = rect.top + rect.height / 2;
    
    x.set((e.clientX - centerX) * strength);
    y.set((e.clientY - centerY) * strength);
  };

  const reset = () => {
    x.set(0);
    y.set(0);
  };

  return (
    <motion.div
      ref={ref}
      style={{ x: springX, y: springY }}
      onMouseMove={handleMouse}
      onMouseLeave={reset}
    >
      {children}
    </motion.div>
  );
}
```

**Usage:**
```tsx
<Magnetic strength={0.4}>
  <button className="px-6 py-3 bg-primary">Hover Me</button>
</Magnetic>
```

---

# PART 6 — PINNED SCROLL SECTIONS

```tsx
"use client";
import { useGSAP } from "@gsap/react";
import gsap from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

export function PinnedSection() {
  const containerRef = useRef<HTMLDivElement>(null);

  useGSAP(() => {
    const panels = gsap.utils.toArray<HTMLElement>(".panel");
    
    gsap.to(panels, {
      xPercent: -100 * (panels.length - 1),
      ease: "none",
      scrollTrigger: {
        trigger: containerRef.current,
        pin: true,
        scrub: 1,
        end: () => "+=" + (containerRef.current?.offsetWidth || 0),
      },
    });
  });

  return (
    <div ref={containerRef} className="flex overflow-hidden">
      <div className="panel w-screen h-screen flex-shrink-0">Panel 1</div>
      <div className="panel w-screen h-screen flex-shrink-0">Panel 2</div>
      <div className="panel w-screen h-screen flex-shrink-0">Panel 3</div>
    </div>
  );
}
```

---

# REQUIRED PACKAGES SUMMARY

```json
{
  "dependencies": {
    "framer-motion": "^11.0.0",
    "gsap": "^3.12.0",
    "@gsap/react": "^2.1.0",
    "split-type": "^0.3.0",
    "@studio-freight/lenis": "^1.0.0"
  }
}
```
