---
name: polish-pass
description: The final creative layer. Runs AFTER a page is functionally complete to add micro-interactions, decorative effects, and signature details that elevate a site from "clean" to "memorable." Use this skill whenever a page is built and working but feels generic, flat, or lacks personality. Also trigger when the user says "make it special", "add polish", "add details", "it needs more life", "Awwwards quality", or "it's too plain."
---

## TL;DR
**Skill:** 16 — Polish Pass  
**Phase:** Final Polish  
**Purpose:** Add premium micro-detailing  
**Change Budget:** SMALL  
**Stop:** After refinement without scope creep  
**Redirects:** If identity change needed → 18.5

# Polish Pass

## Objective
Take a working, well-structured page and add the 15-25 micro-details that make visitors feel like someone *cared*. This skill is the difference between a solid 8/10 and a genuine 10/10.

## Philosophy
**Not:** "Add effects everywhere."
**Instead:** "Where does a small detail amplify the message?"

Polish is not decoration. It's communication. A pulsing CTA says "this matters." A border beam on a feature card says "look here." A gradient text headline says "this is premium." Every effect must *earn its place*.

---

## When to Run
- Page is functionally complete (all sections built, responsive, animations working)
- Before Deployment Packager (skill 12)
- After Performance Guardian (skill 08) — polish must respect performance budgets

## Prerequisites
- [ ] All sections render correctly
- [ ] Responsive layout verified
- [ ] Base scroll animations working
- [ ] No console errors

---

## Phase 1: The Polish Audit

### Step 1: Walk the Page
Go through the page section by section and categorize every element:

| Category | What to Look For | Polish Priority |
|:---------|:-----------------|:----------------|
| **Hero CTA** | Primary button, the most important click | 🔴 HIGH |
| **Hero Headline** | First text the visitor reads | 🔴 HIGH |
| **Feature Cards** | The elements explaining your value | 🟡 MEDIUM |
| **Navigation** | Header, menu items, logo | 🟡 MEDIUM |
| **Section Transitions** | How sections flow into each other | 🟡 MEDIUM |
| **Social Proof** | Testimonials, logos, trust badges | 🟢 LOW |
| **Footer** | Links, copyright, secondary nav | 🟢 LOW |
| **Body Text** | Paragraphs, descriptions | ⚫ SKIP |

**Rule:** Never polish body text. It should be invisible and readable, not decorated.

### Step 2: Create the Polish Map

```markdown
## Polish Map: [Page Name]

### HIGH Priority
1. Hero CTA → [Effect] — [Why]
2. Hero Headline → [Effect] — [Why]

### MEDIUM Priority
3. Feature Card 1-3 → [Effect] — [Why]
4. Nav on scroll → [Effect] — [Why]

### LOW Priority (if budget allows)
5. Trust logos → [Effect] — [Why]

### Total Effects: [count]
### Estimated Performance Impact: [Minimal/Low/Medium]
```

**STOP POINT 🛑**: Present the Polish Map to the user. Ask: "This is what I'd add. Approve, modify, or skip any?"

---

## Phase 2: Constraints (Read Before Implementing)

### The Rules of Restraint

1. **Max 3 HIGH-intensity effects per page.** High-intensity = continuous animation, complex shader, or multi-property transition.
2. **Max 1 animated effect visible at any time in the viewport.** If hero has a shimmer button AND animated gradient text, they must be spaced so only one is in view.
3. **No competing timings.** If two elements animate, they must either be synchronized (same duration/easing) or clearly staggered (0.5s+ apart).
4. **Hover effects are free.** They only activate on interaction, so they don't add visual noise at rest.
5. **Mobile: reduce by 50%.** Cut continuous animations, keep hover-equivalents as tap states.
6. **Respect `prefers-reduced-motion`.** Every continuous animation must have a static fallback.

### Performance Budget
| Effect Type | Cost | Max Per Page |
|:------------|:-----|:-------------|
| CSS-only (gradients, shadows, transitions) | Free | Unlimited |
| CSS animation (keyframes) | Very Low | 10-15 |
| Framer Motion (hover/tap) | Low | 10-15 |
| Framer Motion (continuous/scroll) | Medium | 5-8 |
| GSAP ScrollTrigger | Medium | 5-8 |
| Canvas/WebGL | High | 1-2 |
| SVG filter animation | High | 1 |

---

## Phase 3: The Effect Library

This is the menu. Every effect has: what it does, when to use it, and exact implementation code. Grouped by what they apply to.

---

### 🔘 BUTTONS & CTAs

#### Effect B01: Shimmer Sweep
A light reflection sweeps across the button surface on repeat or hover.
**When:** Primary CTA that needs to draw attention continuously.
**Intensity:** Medium (continuous) or Low (hover-only).

```tsx
// CSS approach (best performance)
<button className="relative overflow-hidden group">
  <span className="relative z-10">Get Started</span>
  <div className="absolute inset-0 -translate-x-full group-hover:translate-x-full transition-transform duration-700 bg-gradient-to-r from-transparent via-white/20 to-transparent" />
</button>
```

```tsx
// Continuous version (CSS keyframe)
// Add to globals.css:
@keyframes shimmer {
  0% { transform: translateX(-100%); }
  100% { transform: translateX(100%); }
}

.shimmer-effect::after {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(90deg, transparent, rgba(255,255,255,0.15), transparent);
  animation: shimmer 3s ease-in-out infinite;
}
```

#### Effect B02: Expand Fill
Background color fills the button from a point on hover.
**When:** Secondary buttons, nav links, any button that should feel interactive but not scream for attention.
**Intensity:** Low.

```tsx
<button className="relative overflow-hidden group border border-white/20 px-6 py-3">
  <span className="relative z-10 group-hover:text-black transition-colors duration-300">
    Learn More
  </span>
  <div className="absolute inset-0 bg-white translate-y-full group-hover:translate-y-0 transition-transform duration-300 ease-out" />
</button>
```

Variants: `translate-y-full` (from bottom), `-translate-y-full` (from top), `translate-x-full` (from right), `-translate-x-full` (from left), `scale-0` (from center).

#### Effect B03: Text Swap
Button text slides out and new text slides in on hover.
**When:** CTAs where you want to reinforce the action. "Learn More" → "See Case Studies".
**Intensity:** Low.

```tsx
<button className="relative overflow-hidden h-12 px-6 group">
  <span className="block transition-transform duration-300 group-hover:-translate-y-full">
    Learn More
  </span>
  <span className="absolute inset-0 flex items-center justify-center translate-y-full transition-transform duration-300 group-hover:translate-y-0">
    See Case Studies →
  </span>
</button>
```

#### Effect B04: Border Draw
Border animates around the button on hover, like it's being drawn.
**When:** Minimal/clean designs where a fill would be too heavy.
**Intensity:** Low.

```tsx
// Using BorderBeam component from Zaitex
import { BorderBeam } from "@/components/zaitex/border-beam";

<button className="relative px-6 py-3 group">
  <span>Contact Us</span>
  <BorderBeam className="opacity-0 group-hover:opacity-100 transition-opacity" />
</button>
```

```tsx
// Pure CSS version
<button className="relative px-6 py-3 group">
  <span className="relative z-10">Contact Us</span>
  <span className="absolute bottom-0 left-0 w-0 h-[1px] bg-primary group-hover:w-full transition-all duration-300" />
  <span className="absolute top-0 right-0 w-0 h-[1px] bg-primary group-hover:w-full transition-all duration-300 delay-150" />
</button>
```

#### Effect B05: Pulse Ring
A ring expands outward from the button subtly on repeat.
**When:** Single most important CTA on the page. Use sparingly — max 1 per page.
**Intensity:** Medium (continuous).

```tsx
<div className="relative inline-block">
  <button className="relative z-10 px-6 py-3 bg-primary rounded-full">
    Book Now
  </button>
  <span className="absolute inset-0 rounded-full bg-primary/30 animate-ping" />
</div>
```

```tsx
// Subtler version with custom keyframe
@keyframes pulse-ring {
  0% { transform: scale(1); opacity: 0.4; }
  100% { transform: scale(1.5); opacity: 0; }
}

.pulse-ring::before {
  content: '';
  position: absolute;
  inset: -4px;
  border-radius: inherit;
  border: 2px solid currentColor;
  animation: pulse-ring 2s ease-out infinite;
}
```

#### Effect B06: Morphing Shape
Button border-radius shifts on hover for an organic feel.
**When:** Playful or creative brands. Not for corporate.
**Intensity:** Low.

```tsx
<button className="px-8 py-4 bg-primary rounded-[2rem] hover:rounded-[1rem] transition-all duration-500 ease-out">
  Explore
</button>
```

#### Effect B07: Magnetic Pull
Button subtly follows the cursor within a radius.
**When:** Hero CTA, important interactive elements.
**Intensity:** Low (only activates on proximity).

```tsx
// Use existing Magnetic component from Zaitex
import { Magnetic } from "@/components/zaitex/magnetic";

<Magnetic strength={0.3}>
  <button className="px-6 py-3 bg-primary">Get Started</button>
</Magnetic>
```

#### Effect B08: Glow on Hover
Button emits a colored glow matching its background on hover.
**When:** Dark backgrounds, premium feel.
**Intensity:** Low.

```tsx
<button className="px-6 py-3 bg-primary rounded-lg transition-shadow duration-300 hover:shadow-[0_0_30px_rgba(var(--color-primary-rgb),0.4)]">
  Start Free Trial
</button>
```

#### Effect B09: Split Reveal
Button text splits and reveals a background or icon on hover.
**When:** Creative portfolios, editorial sites.
**Intensity:** Low.

```tsx
<button className="relative overflow-hidden group px-8 py-4">
  <span className="inline-block transition-transform duration-300 group-hover:-translate-y-1 group-hover:opacity-0">
    View Work
  </span>
  <span className="absolute inset-0 flex items-center justify-center translate-y-4 opacity-0 group-hover:translate-y-0 group-hover:opacity-100 transition-all duration-300">
    → Portfolio
  </span>
</button>
```

#### Effect B10: Underline Expand
A line grows under the text on hover. Classic, always works.
**When:** Navigation links, text links, minimal designs.
**Intensity:** Very Low.

```tsx
<a className="relative group">
  About Us
  <span className="absolute bottom-0 left-0 w-0 h-[2px] bg-current group-hover:w-full transition-all duration-300" />
</a>
```

Variant — from center:
```tsx
<span className="absolute bottom-0 left-1/2 w-0 h-[2px] bg-current group-hover:w-full group-hover:left-0 transition-all duration-300" />
```

---

### 🃏 CARDS & CONTAINERS

#### Effect C01: Border Beam
Animated light that travels along the card border.
**When:** Feature cards, pricing cards, anything that needs to feel "active."
**Intensity:** Medium (continuous).

```tsx
// Use existing Zaitex component
import { BorderBeam } from "@/components/zaitex/border-beam";

<div className="relative rounded-2xl bg-card p-6">
  <BorderBeam size={200} duration={8} />
  {/* Card content */}
</div>
```

#### Effect C02: Gradient Border
An animated gradient moves along the card border.
**When:** Premium cards, featured items, selected states.
**Intensity:** Medium (continuous).

```tsx
// Wrapper approach
<div className="relative p-[1px] rounded-2xl bg-gradient-to-r from-primary via-purple-500 to-primary bg-[length:200%_100%] animate-gradient-x">
  <div className="rounded-2xl bg-card p-6">
    {/* Card content */}
  </div>
</div>

// globals.css
@keyframes gradient-x {
  0%, 100% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
}
.animate-gradient-x {
  animation: gradient-x 4s ease infinite;
}
```

#### Effect C03: Tilt / 3D Perspective
Card tilts toward the cursor on hover for a 3D feel.
**When:** Portfolio cards, product cards, any grid where hover differentiation matters.
**Intensity:** Low (hover only).

```tsx
"use client";
import { motion, useMotionValue, useSpring, useTransform } from "framer-motion";
import { useRef, MouseEvent } from "react";

export function TiltCard({ children }: { children: React.ReactNode }) {
  const ref = useRef<HTMLDivElement>(null);
  const x = useMotionValue(0.5);
  const y = useMotionValue(0.5);

  const rotateX = useSpring(useTransform(y, [0, 1], [8, -8]), { stiffness: 300, damping: 30 });
  const rotateY = useSpring(useTransform(x, [0, 1], [-8, 8]), { stiffness: 300, damping: 30 });

  const handleMouse = (e: MouseEvent) => {
    if (!ref.current) return;
    const rect = ref.current.getBoundingClientRect();
    x.set((e.clientX - rect.left) / rect.width);
    y.set((e.clientY - rect.top) / rect.height);
  };

  const reset = () => { x.set(0.5); y.set(0.5); };

  return (
    <motion.div
      ref={ref}
      style={{ rotateX, rotateY, transformPerspective: 800 }}
      onMouseMove={handleMouse}
      onMouseLeave={reset}
      className="will-change-transform"
    >
      {children}
    </motion.div>
  );
}
```

#### Effect C04: Glass Reflection
A light streak moves across the card surface, like light on glass.
**When:** Glassmorphism cards, dark theme cards, premium feel.
**Intensity:** Low (hover) or Medium (continuous).

```tsx
<div className="relative overflow-hidden rounded-2xl bg-white/5 backdrop-blur-lg p-6 group">
  {/* Reflection */}
  <div className="absolute inset-0 -translate-x-full group-hover:translate-x-full transition-transform duration-1000 bg-gradient-to-r from-transparent via-white/10 to-transparent" />
  {/* Content */}
  <div className="relative z-10">{children}</div>
</div>
```

#### Effect C05: Hover Content Reveal
Hidden content slides up from the bottom of the card on hover.
**When:** Portfolio grids, team members, product cards with details.
**Intensity:** Low.

```tsx
<div className="relative overflow-hidden rounded-2xl h-[400px] group">
  <img src="/image.jpg" alt="..." className="w-full h-full object-cover" />
  
  {/* Overlay that slides up */}
  <div className="absolute inset-x-0 bottom-0 translate-y-full group-hover:translate-y-0 transition-transform duration-500 ease-out bg-gradient-to-t from-black/90 to-transparent p-6">
    <h3 className="text-white font-bold">Project Name</h3>
    <p className="text-white/70 mt-2">Description here</p>
  </div>
</div>
```

#### Effect C06: Background Shift
Card background color or gradient changes smoothly on hover.
**When:** Feature grids where you want each card to feel distinct on interaction.
**Intensity:** Very Low.

```tsx
<div className="rounded-2xl p-6 bg-card transition-colors duration-500 hover:bg-primary/5">
  {/* Content */}
</div>
```

```tsx
// Gradient version
<div className="rounded-2xl p-6 bg-gradient-to-br from-card to-card hover:from-primary/5 hover:to-purple-500/5 transition-all duration-700">
  {/* Content */}
</div>
```

#### Effect C07: Stacked Depth
Card shows ghost copies behind it, creating a "deck" effect.
**When:** Testimonial cards, case studies, "we have many" messaging.
**Intensity:** Very Low (static).

```tsx
<div className="relative">
  {/* Back layers */}
  <div className="absolute inset-0 rounded-2xl bg-card/50 transform rotate-2 scale-[0.97] translate-y-2" />
  <div className="absolute inset-0 rounded-2xl bg-card/30 transform -rotate-1 scale-[0.94] translate-y-4" />
  {/* Main card */}
  <div className="relative rounded-2xl bg-card p-6 shadow-xl">
    {/* Content */}
  </div>
</div>
```

#### Effect C08: Lift & Shadow Grow
Classic hover: card lifts up and shadow expands. Simple but essential.
**When:** Any card grid. This is the baseline hover.
**Intensity:** Very Low.

```tsx
<div className="rounded-2xl bg-card p-6 shadow-md transition-all duration-300 hover:-translate-y-2 hover:shadow-2xl">
  {/* Content */}
</div>
```

#### Effect C09: Spotlight / Hover Light
A radial gradient follows the mouse inside the card.
**When:** Dark themes, feature cards, pricing cards.
**Intensity:** Low (hover only).

```tsx
"use client";
import { useRef, useState, MouseEvent } from "react";

export function SpotlightCard({ children }: { children: React.ReactNode }) {
  const ref = useRef<HTMLDivElement>(null);
  const [pos, setPos] = useState({ x: 0, y: 0 });
  const [hovering, setHovering] = useState(false);

  const handleMouse = (e: MouseEvent) => {
    if (!ref.current) return;
    const rect = ref.current.getBoundingClientRect();
    setPos({ x: e.clientX - rect.left, y: e.clientY - rect.top });
  };

  return (
    <div
      ref={ref}
      onMouseMove={handleMouse}
      onMouseEnter={() => setHovering(true)}
      onMouseLeave={() => setHovering(false)}
      className="relative overflow-hidden rounded-2xl bg-card p-6 border border-white/10"
    >
      {hovering && (
        <div
          className="pointer-events-none absolute -inset-px opacity-20 transition-opacity duration-300"
          style={{
            background: `radial-gradient(400px circle at ${pos.x}px ${pos.y}px, rgba(var(--color-primary-rgb), 0.3), transparent 60%)`,
          }}
        />
      )}
      <div className="relative z-10">{children}</div>
    </div>
  );
}
```

#### Effect C10: Clip Reveal on Scroll
Card content is masked and reveals as it enters the viewport.
**When:** Any card that enters from below. Adds drama to grid entrances.
**Intensity:** Low (one-time).

```tsx
"use client";
import { motion } from "framer-motion";

<motion.div
  initial={{ clipPath: "inset(100% 0 0 0)" }}
  whileInView={{ clipPath: "inset(0% 0 0 0)" }}
  transition={{ duration: 0.8, ease: [0.16, 1, 0.3, 1] }}
  viewport={{ once: true, margin: "-50px" }}
  className="rounded-2xl bg-card p-6"
>
  {/* Content */}
</motion.div>
```

#### Effect C11: Scale Down Peer
When hovering one card, siblings scale down slightly. Focus effect.
**When:** Feature grids, team sections, pricing tables. Creates hierarchy on hover.
**Intensity:** Low.

```tsx
// Parent wrapper applies group behavior
<div className="grid grid-cols-3 gap-6 group/container">
  {items.map((item) => (
    <div
      key={item.id}
      className="rounded-2xl bg-card p-6 transition-all duration-300
                 hover:scale-105 hover:shadow-2xl
                 group-hover/container:opacity-60 group-hover/container:scale-95
                 hover:!opacity-100 hover:!scale-105"
    >
      {/* Content */}
    </div>
  ))}
</div>
```

#### Effect C12: Accordion Expand
Card expands to reveal more content on click/hover, pushing siblings.
**When:** FAQ, feature details, service descriptions.
**Intensity:** Low.

```tsx
"use client";
import { motion, AnimatePresence } from "framer-motion";
import { useState } from "react";

export function ExpandCard({ title, children }: { title: string; children: React.ReactNode }) {
  const [open, setOpen] = useState(false);

  return (
    <motion.div
      layout
      onClick={() => setOpen(!open)}
      className="rounded-2xl bg-card p-6 cursor-pointer"
    >
      <motion.h3 layout="position" className="font-bold">{title}</motion.h3>
      <AnimatePresence>
        {open && (
          <motion.div
            initial={{ opacity: 0, height: 0 }}
            animate={{ opacity: 1, height: "auto" }}
            exit={{ opacity: 0, height: 0 }}
            className="overflow-hidden"
          >
            <div className="pt-4">{children}</div>
          </motion.div>
        )}
      </AnimatePresence>
    </motion.div>
  );
}
```

---

### ✏️ TEXT & TYPOGRAPHY

#### Effect T01: Character Stagger Reveal
Text reveals character by character from bottom with rotation.
**When:** Hero headlines, section titles on scroll.
**Intensity:** Medium (one-time).

```tsx
// Use GSAP + SplitType (see Motion Choreographer PART 3)
// Reference: motion-choreographer → "Stagger Text Reveal"
```

#### Effect T02: Text Scramble
Characters scramble randomly before resolving to final text.
**When:** Tech brands, status labels, "system online" messaging.
**Intensity:** Medium (one-time).

```tsx
// Use existing TextScramble component from Zaitex
import { TextScramble } from "@/components/zaitex/text-scramble";

<TextScramble text="System Architecture" />
```

#### Effect T03: Animated Gradient Text
Text filled with a moving gradient.
**When:** Hero headlines on dark backgrounds, premium feel.
**Intensity:** Low (continuous but CSS-only).

```tsx
<h1 className="text-6xl font-bold bg-gradient-to-r from-white via-primary to-white bg-[length:200%_100%] bg-clip-text text-transparent animate-gradient-x">
  Build Something Beautiful
</h1>

// globals.css (if not already added)
@keyframes gradient-x {
  0%, 100% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
}
.animate-gradient-x {
  animation: gradient-x 6s ease infinite;
}
```

#### Effect T04: Underline Draw
A line draws itself under text on hover or on scroll-enter.
**When:** Section headings, links, emphasized words.
**Intensity:** Very Low.

```tsx
// Hover version
<span className="relative group">
  Our Mission
  <span className="absolute bottom-0 left-0 w-0 h-[2px] bg-primary group-hover:w-full transition-all duration-500 ease-out" />
</span>
```

```tsx
// Scroll-enter version
<motion.span className="relative inline-block">
  Our Mission
  <motion.span
    className="absolute bottom-0 left-0 h-[2px] bg-primary origin-left"
    initial={{ scaleX: 0 }}
    whileInView={{ scaleX: 1 }}
    transition={{ duration: 0.8, delay: 0.3, ease: [0.16, 1, 0.3, 1] }}
    viewport={{ once: true }}
  />
</motion.span>
```

#### Effect T05: Word-by-Word Opacity (Scrub)
Text where each word goes from dim to full opacity as you scroll through.
**When:** Manifesto sections, storytelling, long-form statements.
**Intensity:** Medium (scroll-linked).

```tsx
"use client";
import { useRef } from "react";
import { useGSAP } from "@gsap/react";
import gsap from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

export function ScrubText({ text }: { text: string }) {
  const containerRef = useRef<HTMLParagraphElement>(null);

  useGSAP(() => {
    if (!containerRef.current) return;
    const words = containerRef.current.querySelectorAll(".scrub-word");
    
    gsap.fromTo(words,
      { opacity: 0.15 },
      {
        opacity: 1,
        stagger: 0.05,
        scrollTrigger: {
          trigger: containerRef.current,
          start: "top 80%",
          end: "bottom 40%",
          scrub: true,
        },
      }
    );
  }, { scope: containerRef });

  return (
    <p ref={containerRef} className="text-4xl font-bold leading-relaxed">
      {text.split(" ").map((word, i) => (
        <span key={i} className="scrub-word inline-block mr-[0.3em] opacity-15">
          {word}
        </span>
      ))}
    </p>
  );
}
```

#### Effect T06: Number Counter Roll
Numbers count up from 0 to target value when entering viewport.
**When:** Stats sections, metrics, "100+ clients" type content.
**Intensity:** Low (one-time).

```tsx
"use client";
import { useRef, useEffect, useState } from "react";
import { useInView, motion } from "framer-motion";

export function Counter({ target, duration = 2, suffix = "" }: { target: number; duration?: number; suffix?: string }) {
  const ref = useRef<HTMLSpanElement>(null);
  const isInView = useInView(ref, { once: true });
  const [count, setCount] = useState(0);

  useEffect(() => {
    if (!isInView) return;
    let start = 0;
    const step = target / (duration * 60);
    const timer = setInterval(() => {
      start += step;
      if (start >= target) {
        setCount(target);
        clearInterval(timer);
      } else {
        setCount(Math.floor(start));
      }
    }, 1000 / 60);
    return () => clearInterval(timer);
  }, [isInView, target, duration]);

  return <span ref={ref}>{count.toLocaleString()}{suffix}</span>;
}
```

Usage: `<Counter target={500} suffix="+" />`

#### Effect T07: Typewriter
Text types out character by character.
**When:** Terminal aesthetics, code-themed brands, "building" metaphors.
**Intensity:** Medium (one-time).

```tsx
"use client";
import { useState, useEffect } from "react";
import { useInView } from "framer-motion";
import { useRef } from "react";

export function Typewriter({ text, speed = 50 }: { text: string; speed?: number }) {
  const ref = useRef<HTMLSpanElement>(null);
  const isInView = useInView(ref, { once: true });
  const [displayed, setDisplayed] = useState("");

  useEffect(() => {
    if (!isInView) return;
    let i = 0;
    const timer = setInterval(() => {
      setDisplayed(text.slice(0, i + 1));
      i++;
      if (i >= text.length) clearInterval(timer);
    }, speed);
    return () => clearInterval(timer);
  }, [isInView, text, speed]);

  return (
    <span ref={ref}>
      {displayed}
      <span className="animate-pulse">|</span>
    </span>
  );
}
```

#### Effect T08: Blur to Sharp
Text starts blurred and becomes sharp on scroll.
**When:** Dramatic reveals, hero subtitles, section entrances.
**Intensity:** Low (one-time).

```tsx
<motion.h2
  initial={{ filter: "blur(10px)", opacity: 0 }}
  whileInView={{ filter: "blur(0px)", opacity: 1 }}
  transition={{ duration: 0.8, ease: "easeOut" }}
  viewport={{ once: true }}
  className="text-5xl font-bold"
>
  Crystal Clear Strategy
</motion.h2>
```

#### Effect T09: Highlight Marker
A colored background "marker" draws behind specific words.
**When:** Emphasizing key phrases, like a real highlighter.
**Intensity:** Very Low (one-time).

```tsx
<motion.span className="relative inline-block">
  <span className="relative z-10">game changer</span>
  <motion.span
    className="absolute bottom-1 left-0 right-0 h-[40%] bg-primary/20 -z-0"
    initial={{ scaleX: 0 }}
    whileInView={{ scaleX: 1 }}
    transition={{ duration: 0.6, delay: 0.5, ease: "easeOut" }}
    viewport={{ once: true }}
    style={{ originX: 0 }}
  />
</motion.span>
```

#### Effect T10: Text Fade Stagger
Lines or words fade in one by one with stagger.
**When:** Body text entrances, lists, feature descriptions.
**Intensity:** Low (one-time).

```tsx
<motion.div
  initial="hidden"
  whileInView="visible"
  viewport={{ once: true }}
  variants={{
    hidden: {},
    visible: { transition: { staggerChildren: 0.08 } },
  }}
>
  {lines.map((line, i) => (
    <motion.p
      key={i}
      variants={{
        hidden: { opacity: 0, y: 10 },
        visible: { opacity: 1, y: 0, transition: { duration: 0.5 } },
      }}
    >
      {line}
    </motion.p>
  ))}
</motion.div>
```

---

### ⭐ ICONS & SMALL ELEMENTS

#### Effect I01: Pulse Glow
Icon emits a soft, rhythmic glow.
**When:** Status indicators, feature icons that should feel "alive."
**Intensity:** Low (continuous but subtle).

```tsx
<div className="relative">
  <Icon className="w-6 h-6 text-primary relative z-10" />
  <div className="absolute inset-0 bg-primary/30 rounded-full blur-md animate-pulse" />
</div>
```

#### Effect I02: Draw SVG
Icon strokes draw themselves on scroll-enter.
**When:** Feature sections with line icons, process steps.
**Intensity:** Low (one-time).

```tsx
"use client";
import { motion } from "framer-motion";

export function DrawIcon({ children }: { children: React.ReactNode }) {
  return (
    <motion.div
      initial={{ opacity: 0 }}
      whileInView={{ opacity: 1 }}
      viewport={{ once: true }}
      className="[&_svg]:overflow-visible [&_path]:stroke-primary [&_path]:fill-none
                 [&_path]:[stroke-dasharray:100] [&_path]:[stroke-dashoffset:100]
                 [&_path]:animate-draw"
    >
      {children}
    </motion.div>
  );
}

// globals.css
@keyframes draw {
  to { stroke-dashoffset: 0; }
}
.animate-draw path {
  animation: draw 1.5s ease-out forwards;
}
```

#### Effect I03: Bounce Entrance
Icon bounces into view. Playful but not childish.
**When:** Feature lists, step indicators, notification badges.
**Intensity:** Very Low (one-time).

```tsx
<motion.div
  initial={{ scale: 0, opacity: 0 }}
  whileInView={{ scale: 1, opacity: 1 }}
  transition={{ type: "spring", stiffness: 400, damping: 15 }}
  viewport={{ once: true }}
>
  <Icon className="w-8 h-8" />
</motion.div>
```

#### Effect I04: Float
Element bobs up and down continuously. Dreamlike.
**When:** Decorative elements, floating badges, hero accents.
**Intensity:** Low (continuous but CSS-only).

```tsx
@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-10px); }
}

.animate-float {
  animation: float 4s ease-in-out infinite;
}
```

```tsx
<div className="animate-float">
  <Badge>New</Badge>
</div>
```

#### Effect I05: Spin on Hover
Subtle rotation on hover. Works on icons, logos, decorative elements.
**When:** Social icons, tool icons, settings icons.
**Intensity:** Very Low.

```tsx
<Icon className="w-6 h-6 transition-transform duration-500 hover:rotate-180" />
```

Half spin: `hover:rotate-90`. Full spin: `hover:rotate-[360deg]`.

#### Effect I06: Icon Morph
Icon transitions smoothly between two states.
**When:** Hamburger → X, Play → Pause, Plus → Minus.
**Intensity:** Very Low.

```tsx
// For hamburger → X, use Framer Motion layout animations
<motion.div layout className="flex flex-col gap-1.5 w-6">
  <motion.span
    layout
    animate={open ? { rotate: 45, y: 6 } : { rotate: 0, y: 0 }}
    className="w-full h-[2px] bg-current"
  />
  <motion.span
    layout
    animate={open ? { opacity: 0 } : { opacity: 1 }}
    className="w-full h-[2px] bg-current"
  />
  <motion.span
    layout
    animate={open ? { rotate: -45, y: -6 } : { rotate: 0, y: 0 }}
    className="w-full h-[2px] bg-current"
  />
</motion.div>
```

#### Effect I07: Stagger Grid Icons
Icons in a feature grid enter one by one with delay.
**When:** Any section with 3+ icons in a grid.
**Intensity:** Low (one-time).

```tsx
<motion.div
  className="grid grid-cols-3 gap-8"
  initial="hidden"
  whileInView="visible"
  viewport={{ once: true }}
  variants={{ visible: { transition: { staggerChildren: 0.1 } } }}
>
  {features.map((f) => (
    <motion.div
      key={f.id}
      variants={{
        hidden: { opacity: 0, y: 20 },
        visible: { opacity: 1, y: 0, transition: { duration: 0.5 } },
      }}
    >
      <f.icon className="w-8 h-8 text-primary" />
      <h3>{f.title}</h3>
    </motion.div>
  ))}
</motion.div>
```

---

### 🌌 BACKGROUNDS & ATMOSPHERE

#### Effect A01: Aurora
Slow-moving color blobs that blend like northern lights.
**When:** Hero backgrounds, dark themes, premium/luxury.
**Intensity:** Medium (continuous).

```tsx
<div className="absolute inset-0 overflow-hidden">
  <div className="absolute top-1/4 -left-1/4 w-[600px] h-[600px] rounded-full bg-primary/20 blur-[120px] animate-aurora-1" />
  <div className="absolute bottom-1/4 -right-1/4 w-[500px] h-[500px] rounded-full bg-purple-500/15 blur-[120px] animate-aurora-2" />
  <div className="absolute top-1/2 left-1/2 w-[400px] h-[400px] rounded-full bg-blue-500/10 blur-[120px] animate-aurora-3" />
</div>

// globals.css
@keyframes aurora-1 {
  0%, 100% { transform: translate(0, 0) scale(1); }
  33% { transform: translate(50px, -30px) scale(1.1); }
  66% { transform: translate(-20px, 40px) scale(0.95); }
}
@keyframes aurora-2 {
  0%, 100% { transform: translate(0, 0) scale(1); }
  33% { transform: translate(-40px, 30px) scale(1.05); }
  66% { transform: translate(30px, -50px) scale(1.1); }
}
@keyframes aurora-3 {
  0%, 100% { transform: translate(0, 0) scale(1); }
  50% { transform: translate(40px, 40px) scale(1.15); }
}
.animate-aurora-1 { animation: aurora-1 15s ease-in-out infinite; }
.animate-aurora-2 { animation: aurora-2 18s ease-in-out infinite; }
.animate-aurora-3 { animation: aurora-3 20s ease-in-out infinite; }
```

#### Effect A02: Moving Gradient Orbs
Large, soft gradient circles that drift slowly.
**When:** Lighter version of Aurora. Works on light backgrounds too.
**Intensity:** Low-Medium (continuous but CSS-only).

```tsx
<div className="absolute inset-0 overflow-hidden opacity-30">
  <div className="absolute w-[500px] h-[500px] rounded-full bg-gradient-radial from-primary/40 to-transparent animate-float" style={{ top: '10%', left: '20%' }} />
  <div className="absolute w-[400px] h-[400px] rounded-full bg-gradient-radial from-purple-500/30 to-transparent animate-float" style={{ top: '50%', right: '10%', animationDelay: '-5s' }} />
</div>
```

#### Effect A03: Light Leak
A soft light spot that drifts subtly, like a camera lens effect.
**When:** Hero sections, feature showcases, photographic content.
**Intensity:** Low.

```tsx
<div className="absolute top-0 right-1/4 w-[600px] h-[600px] bg-gradient-radial from-orange-300/10 to-transparent blur-3xl animate-float opacity-40 pointer-events-none" />
```

#### Effect A04: Noise/Grain Overlay
Static noise texture over the entire page.
**When:** Almost always. Adds analog warmth and prevents "digital flat" feel.
**Intensity:** Very Low (static).

```tsx
// Use existing NoiseOverlay from Zaitex
// Reference: aura-migration skill → "Noise/Grain Overlay"
import { NoiseOverlay } from "@/components/ui/noise-overlay";
```

**Rule:** Keep opacity at 0.02-0.05. Higher = gritty/editorial. Lower = premium.

#### Effect A05: Vignette
Radial gradient darkening at edges. Focuses attention on center content.
**When:** Hero sections, fullscreen sections, image-heavy pages.
**Intensity:** Very Low (static).

```tsx
<div className="pointer-events-none absolute inset-0 bg-[radial-gradient(ellipse_at_center,transparent_50%,rgba(0,0,0,0.3)_100%)]" />
```

#### Effect A06: Animated Mesh Gradient
Multiple color stops that shift positions slowly.
**When:** Hero backgrounds, CTA sections, premium brands.
**Intensity:** Medium (continuous).

```tsx
// Use existing MeshGradient from Zaitex if available
// Or implement with CSS:
<div className="absolute inset-0 bg-gradient-to-br from-primary/10 via-purple-500/5 to-blue-500/10 bg-[length:400%_400%] animate-gradient-xy" />

// globals.css
@keyframes gradient-xy {
  0%, 100% { background-position: 0% 0%; }
  25% { background-position: 100% 0%; }
  50% { background-position: 100% 100%; }
  75% { background-position: 0% 100%; }
}
.animate-gradient-xy {
  animation: gradient-xy 20s ease infinite;
}
```

#### Effect A07: Parallax Dots/Grid
The background grid or dot pattern moves at a different speed than content.
**When:** Adds depth to any section with a DotGridPattern or GridPattern.
**Intensity:** Low.

```tsx
"use client";
import { motion, useScroll, useTransform } from "framer-motion";

export function ParallaxGrid({ children }: { children: React.ReactNode }) {
  const { scrollY } = useScroll();
  const y = useTransform(scrollY, [0, 3000], [0, -200]);

  return (
    <div className="relative">
      <motion.div style={{ y }} className="absolute inset-0 pointer-events-none">
        {/* Your grid/dot pattern */}
      </motion.div>
      <div className="relative z-10">{children}</div>
    </div>
  );
}
```

---

### 📜 SCROLL-BASED

#### Effect S01: Scroll Progress Bar
A thin line at the top showing how far down the page the user has scrolled.
**When:** Long pages, articles, single-page sites.
**Intensity:** Very Low.

```tsx
"use client";
import { motion, useScroll } from "framer-motion";

export function ScrollProgress() {
  const { scrollYProgress } = useScroll();

  return (
    <motion.div
      style={{ scaleX: scrollYProgress }}
      className="fixed top-0 left-0 right-0 h-[2px] bg-primary origin-left z-50"
    />
  );
}
```

#### Effect S02: Section Color Shift
Background color transitions smoothly as you scroll between sections.
**When:** Single-page sites, storytelling pages, brand showcases.
**Intensity:** Low (CSS-only possible).

```tsx
"use client";
import { useGSAP } from "@gsap/react";
import gsap from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

export function ColorShiftPage() {
  const containerRef = useRef<HTMLDivElement>(null);

  useGSAP(() => {
    const sections = gsap.utils.toArray<HTMLElement>(".color-section");
    sections.forEach((section) => {
      const color = section.dataset.bgColor;
      ScrollTrigger.create({
        trigger: section,
        start: "top 60%",
        onEnter: () => gsap.to("body", { backgroundColor: color, duration: 0.8 }),
        onEnterBack: () => gsap.to("body", { backgroundColor: color, duration: 0.8 }),
      });
    });
  }, { scope: containerRef });

  return (
    <div ref={containerRef}>
      <section className="color-section" data-bg-color="#0A0A0A">...</section>
      <section className="color-section" data-bg-color="#1a1a2e">...</section>
      <section className="color-section" data-bg-color="#F5F5F7">...</section>
    </div>
  );
}
```

#### Effect S03: Scale on Scroll
Element grows as it enters the viewport and shrinks as it leaves.
**When:** Hero images, feature illustrations, section headers.
**Intensity:** Low.

```tsx
<motion.div
  initial={{ scale: 0.9, opacity: 0 }}
  whileInView={{ scale: 1, opacity: 1 }}
  transition={{ duration: 0.6, ease: [0.16, 1, 0.3, 1] }}
  viewport={{ once: true, margin: "-100px" }}
>
  {/* Content */}
</motion.div>
```

#### Effect S04: Blur on Exit
Section blurs as it scrolls out of view. Creates depth.
**When:** Storytelling pages, editorial content, immersive experiences.
**Intensity:** Medium (scroll-linked).

```tsx
"use client";
import { motion, useScroll, useTransform } from "framer-motion";
import { useRef } from "react";

export function BlurOnExit({ children }: { children: React.ReactNode }) {
  const ref = useRef<HTMLDivElement>(null);
  const { scrollYProgress } = useScroll({
    target: ref,
    offset: ["start start", "end start"],
  });
  const blur = useTransform(scrollYProgress, [0.5, 1], [0, 10]);
  const opacity = useTransform(scrollYProgress, [0.5, 1], [1, 0.3]);

  return (
    <motion.div ref={ref} style={{ filter: blur.get() ? `blur(${blur.get()}px)` : "none", opacity }}>
      {children}
    </motion.div>
  );
}
```

#### Effect S05: Horizontal Reveal
Content slides in from the side as you scroll.
**When:** Before/after comparisons, timeline entries, feature reveals.
**Intensity:** Low (one-time).

```tsx
<motion.div
  initial={{ x: -60, opacity: 0 }}
  whileInView={{ x: 0, opacity: 1 }}
  transition={{ duration: 0.7, ease: [0.16, 1, 0.3, 1] }}
  viewport={{ once: true }}
>
  {/* Content */}
</motion.div>
```

From right: use `x: 60` in initial.

#### Effect S06: Parallax Image
Image moves at different speed than its container.
**When:** Hero images, section backgrounds, editorial layouts.
**Intensity:** Low.

```tsx
// Reference: motion-choreographer → "Parallax Image Wrapper"
import { ParallaxImage } from "@/components/zaitex/parallax-image";
```

#### Effect S07: Sticky Reveal Stack
Cards stack on top of each other as you scroll, each pushing the previous.
**When:** Feature showcases, process steps, pricing tiers.
**Intensity:** Medium (scroll-linked + pinning).

```tsx
// Reference: motion-choreographer → PART 6 "Pinned Scroll Sections"
// Also see: aura-migration skill → "MethodStack" pattern
```

#### Effect S08: Text Parallax Banner
A wide text banner that scrolls horizontally as you scroll vertically.
**When:** Section dividers, brand statements, decorative breaks.
**Intensity:** Low.

```tsx
"use client";
import { motion, useScroll, useTransform } from "framer-motion";

export function ParallaxBanner({ text }: { text: string }) {
  const { scrollY } = useScroll();
  const x = useTransform(scrollY, [0, 3000], [0, -500]);

  return (
    <div className="overflow-hidden py-12">
      <motion.div style={{ x }} className="flex whitespace-nowrap gap-8">
        {Array(4).fill(null).map((_, i) => (
          <span key={i} className="text-[8vw] font-bold text-foreground/5 uppercase">
            {text} •
          </span>
        ))}
      </motion.div>
    </div>
  );
}
```

---

### 🖱️ CURSOR & INTERACTION

#### Effect X01: Custom Cursor
Replace default cursor with a designed circle that follows the mouse.
**When:** Portfolio sites, creative agencies, immersive experiences.
**Intensity:** Medium (continuous).

```tsx
"use client";
import { motion, useMotionValue, useSpring } from "framer-motion";
import { useEffect } from "react";

export function CustomCursor() {
  const x = useMotionValue(0);
  const y = useMotionValue(0);
  const springX = useSpring(x, { stiffness: 300, damping: 30 });
  const springY = useSpring(y, { stiffness: 300, damping: 30 });

  useEffect(() => {
    const move = (e: MouseEvent) => { x.set(e.clientX); y.set(e.clientY); };
    window.addEventListener("mousemove", move);
    return () => window.removeEventListener("mousemove", move);
  }, [x, y]);

  return (
    <>
      {/* Main cursor */}
      <motion.div
        style={{ x: springX, y: springY }}
        className="fixed top-0 left-0 w-4 h-4 -translate-x-1/2 -translate-y-1/2 rounded-full bg-primary pointer-events-none z-[9999] mix-blend-difference"
      />
      {/* Trailing ring */}
      <motion.div
        style={{ x: springX, y: springY }}
        className="fixed top-0 left-0 w-10 h-10 -translate-x-1/2 -translate-y-1/2 rounded-full border border-primary/50 pointer-events-none z-[9999]"
      />
    </>
  );
}
```

**Note:** Hide default cursor with `cursor: none` on body. Always provide fallback for touch devices.

#### Effect X02: Hover Spotlight
A radial light follows the cursor over a dark surface.
**When:** Dark hero sections, feature grids, interactive backgrounds.
**Intensity:** Low (hover only).

```tsx
// See Effect C09 (SpotlightCard) for per-card version
// For full-section version:
"use client";
import { useRef, useState, MouseEvent } from "react";

export function SpotlightSection({ children }: { children: React.ReactNode }) {
  const ref = useRef<HTMLElement>(null);
  const [pos, setPos] = useState({ x: 0, y: 0 });

  const handleMouse = (e: MouseEvent) => {
    if (!ref.current) return;
    const rect = ref.current.getBoundingClientRect();
    setPos({ x: e.clientX - rect.left, y: e.clientY - rect.top });
  };

  return (
    <section
      ref={ref}
      onMouseMove={handleMouse}
      className="relative overflow-hidden"
    >
      <div
        className="pointer-events-none absolute -inset-px opacity-30"
        style={{
          background: `radial-gradient(600px circle at ${pos.x}px ${pos.y}px, rgba(var(--color-primary-rgb), 0.15), transparent 60%)`,
        }}
      />
      <div className="relative z-10">{children}</div>
    </section>
  );
}
```

#### Effect X03: Ripple Click
A ripple effect expands from the click point, like Material Design but subtler.
**When:** Buttons, interactive cards, any clickable surface.
**Intensity:** Very Low (event-driven).

```tsx
"use client";
import { useState, MouseEvent } from "react";

interface Ripple {
  x: number;
  y: number;
  id: number;
}

export function RippleButton({ children, className, ...props }: React.ButtonHTMLAttributes<HTMLButtonElement>) {
  const [ripples, setRipples] = useState<Ripple[]>([]);

  const handleClick = (e: MouseEvent<HTMLButtonElement>) => {
    const rect = e.currentTarget.getBoundingClientRect();
    const ripple = {
      x: e.clientX - rect.left,
      y: e.clientY - rect.top,
      id: Date.now(),
    };
    setRipples((prev) => [...prev, ripple]);
    setTimeout(() => setRipples((prev) => prev.filter((r) => r.id !== ripple.id)), 600);
    props.onClick?.(e);
  };

  return (
    <button {...props} onClick={handleClick} className={`relative overflow-hidden ${className}`}>
      {ripples.map((ripple) => (
        <span
          key={ripple.id}
          className="absolute w-[200px] h-[200px] -translate-x-1/2 -translate-y-1/2 rounded-full bg-white/20 animate-ripple pointer-events-none"
          style={{ left: ripple.x, top: ripple.y }}
        />
      ))}
      <span className="relative z-10">{children}</span>
    </button>
  );
}

// globals.css
@keyframes ripple {
  0% { transform: translate(-50%, -50%) scale(0); opacity: 1; }
  100% { transform: translate(-50%, -50%) scale(1); opacity: 0; }
}
.animate-ripple {
  animation: ripple 0.6s ease-out;
}
```

#### Effect X04: Cursor Text Ring
Text that orbits the cursor in a circle. Shows on specific hover targets.
**When:** Portfolio links, "view project" indicators, creative sites.
**Intensity:** Medium (continuous while hovering).

```tsx
"use client";
import { motion, useMotionValue, useSpring } from "framer-motion";
import { useEffect, useState } from "react";

export function CursorTextRing({ text = "View Project • " }: { text?: string }) {
  const x = useMotionValue(0);
  const y = useMotionValue(0);
  const springX = useSpring(x, { stiffness: 200, damping: 25 });
  const springY = useSpring(y, { stiffness: 200, damping: 25 });
  const [visible, setVisible] = useState(false);

  useEffect(() => {
    const move = (e: MouseEvent) => { x.set(e.clientX); y.set(e.clientY); };
    window.addEventListener("mousemove", move);
    return () => window.removeEventListener("mousemove", move);
  }, [x, y]);

  // Expose show/hide via data attributes
  useEffect(() => {
    const show = () => setVisible(true);
    const hide = () => setVisible(false);
    document.querySelectorAll("[data-cursor-text]").forEach((el) => {
      el.addEventListener("mouseenter", show);
      el.addEventListener("mouseleave", hide);
    });
    return () => {
      document.querySelectorAll("[data-cursor-text]").forEach((el) => {
        el.removeEventListener("mouseenter", show);
        el.removeEventListener("mouseleave", hide);
      });
    };
  }, []);

  const repeated = text.repeat(3);

  return (
    <motion.div
      style={{ x: springX, y: springY }}
      className="fixed top-0 left-0 -translate-x-1/2 -translate-y-1/2 pointer-events-none z-[9999]"
    >
      <motion.svg
        width="120" height="120"
        animate={{ rotate: 360, opacity: visible ? 1 : 0, scale: visible ? 1 : 0.5 }}
        transition={{ rotate: { repeat: Infinity, duration: 8, ease: "linear" }, opacity: { duration: 0.3 }, scale: { duration: 0.3 } }}
      >
        <path id="curve" d="M 60,60 m -45,0 a 45,45 0 1,1 90,0 a 45,45 0 1,1 -90,0" fill="none" />
        <text fontSize="10" fill="currentColor" className="text-white">
          <textPath href="#curve">{repeated}</textPath>
        </text>
      </motion.svg>
    </motion.div>
  );
}

// Usage: Add data-cursor-text to hover targets
<a href="/project" data-cursor-text>
  <img src="/project.jpg" alt="..." />
</a>
```

---

### 🔀 SECTION TRANSITIONS & DIVIDERS

#### Effect D01: Fade Overlap
Sections overlap slightly with fading edges so they blend together.
**When:** Long scrolling pages, storytelling, editorial.
**Intensity:** Very Low (static CSS).

```tsx
<section className="relative z-10 pb-32">
  {/* Section 1 content */}
  <div className="absolute bottom-0 left-0 right-0 h-32 bg-gradient-to-b from-transparent to-background pointer-events-none" />
</section>
<section className="relative z-20 -mt-16">
  {/* Section 2 content */}
</section>
```

#### Effect D02: Diagonal Divider
A diagonal line separating two sections.
**When:** Two-tone sections, breaking visual monotony.
**Intensity:** Very Low (static SVG/CSS).

```tsx
<div className="relative">
  <div className="absolute bottom-0 left-0 right-0 overflow-hidden leading-[0]">
    <svg viewBox="0 0 1200 120" preserveAspectRatio="none" className="w-full h-[60px]">
      <polygon points="0,120 1200,0 1200,120" className="fill-background" />
    </svg>
  </div>
</div>
```

#### Effect D03: Wave Divider
An SVG wave shape between sections.
**When:** Softer brands, organic feel, service companies.
**Intensity:** Very Low (static SVG).

```tsx
<div className="relative overflow-hidden leading-[0]">
  <svg viewBox="0 0 1200 120" preserveAspectRatio="none" className="w-full h-[80px]">
    <path
      d="M0,0 C300,100 900,0 1200,80 L1200,120 L0,120 Z"
      className="fill-background"
    />
  </svg>
</div>
```

#### Effect D04: Marquee / Infinite Scroll Text
A horizontal scrolling text banner as a section divider.
**When:** Brand statements, decorative breaks, client logos.
**Intensity:** Low (CSS animation).

```tsx
<div className="overflow-hidden py-8 border-y border-white/10">
  <div className="flex animate-marquee whitespace-nowrap">
    {Array(4).fill(null).map((_, i) => (
      <span key={i} className="text-6xl font-bold text-foreground/5 mx-8">
        DESIGN • DEVELOP • DEPLOY • ITERATE •
      </span>
    ))}
  </div>
</div>

// globals.css
@keyframes marquee {
  0% { transform: translateX(0); }
  100% { transform: translateX(-50%); }
}
.animate-marquee {
  animation: marquee 30s linear infinite;
}
```

---

### 🔄 NAVIGATION & HEADER

#### Effect N01: Navbar Blur on Scroll
Navigation gets a backdrop blur and background when user scrolls.
**When:** Almost always. Baseline navigation behavior.
**Intensity:** Very Low.

```tsx
"use client";
import { useState, useEffect } from "react";

export function Navbar() {
  const [scrolled, setScrolled] = useState(false);

  useEffect(() => {
    const handle = () => setScrolled(window.scrollY > 50);
    window.addEventListener("scroll", handle, { passive: true });
    return () => window.removeEventListener("scroll", handle);
  }, []);

  return (
    <nav className={`fixed top-0 w-full z-50 transition-all duration-300 ${
      scrolled
        ? "bg-background/80 backdrop-blur-lg border-b border-white/10 py-3"
        : "bg-transparent py-6"
    }`}>
      {/* Nav content */}
    </nav>
  );
}
```

#### Effect N02: Logo Shrink on Scroll
Logo scales down when navbar becomes compact.
**When:** Sites with prominent logos.
**Intensity:** Very Low.

```tsx
<img
  src="/logo.svg"
  alt="Logo"
  className={`transition-all duration-300 ${scrolled ? "h-8" : "h-12"}`}
/>
```

#### Effect N03: Active Link Indicator
An animated underline or dot that moves to the active nav item.
**When:** Single-page sites, section-based navigation.
**Intensity:** Low.

```tsx
// Using Framer Motion layout animation
<nav className="flex gap-8 relative">
  {links.map((link) => (
    <a key={link.href} href={link.href} className="relative py-2" onClick={() => setActive(link.href)}>
      {link.label}
      {active === link.href && (
        <motion.span
          layoutId="nav-indicator"
          className="absolute bottom-0 left-0 right-0 h-[2px] bg-primary"
          transition={{ type: "spring", stiffness: 400, damping: 30 }}
        />
      )}
    </a>
  ))}
</nav>
```

#### Effect N04: Stagger Menu Items
Mobile menu items enter with staggered animation.
**When:** Hamburger menus, fullscreen nav overlays.
**Intensity:** Low (one-time per open).

```tsx
<AnimatePresence>
  {menuOpen && (
    <motion.div
      initial={{ opacity: 0 }}
      animate={{ opacity: 1 }}
      exit={{ opacity: 0 }}
      className="fixed inset-0 bg-background z-40"
    >
      <motion.nav
        initial="closed"
        animate="open"
        exit="closed"
        variants={{ open: { transition: { staggerChildren: 0.08 } }, closed: {} }}
        className="flex flex-col items-center justify-center h-full gap-8"
      >
        {links.map((link) => (
          <motion.a
            key={link.href}
            href={link.href}
            variants={{
              closed: { opacity: 0, y: 30 },
              open: { opacity: 1, y: 0 },
            }}
            className="text-4xl font-bold"
          >
            {link.label}
          </motion.a>
        ))}
      </motion.nav>
    </motion.div>
  )}
</AnimatePresence>
```

---

### 🔲 LOADING & PAGE TRANSITIONS

#### Effect L01: Page Loader
A branded loading animation that plays on initial page load.
**When:** Sites with heavy assets (3D, many images), premium feel.
**Intensity:** Medium (one-time).

```tsx
"use client";
import { motion, AnimatePresence } from "framer-motion";
import { useState, useEffect } from "react";

export function PageLoader() {
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    const timer = setTimeout(() => setLoading(false), 2000);
    return () => clearTimeout(timer);
  }, []);

  return (
    <AnimatePresence>
      {loading && (
        <motion.div
          initial={{ opacity: 1 }}
          exit={{ opacity: 0 }}
          transition={{ duration: 0.5, ease: "easeInOut" }}
          className="fixed inset-0 z-[9999] bg-background flex items-center justify-center"
        >
          <motion.div
            initial={{ scale: 0.8, opacity: 0 }}
            animate={{ scale: 1, opacity: 1 }}
            transition={{ duration: 0.5 }}
          >
            <img src="/logo.svg" alt="Loading" className="w-16 h-16" />
          </motion.div>
        </motion.div>
      )}
    </AnimatePresence>
  );
}
```

#### Effect L02: Content Skeleton
Placeholder shimmer while content loads.
**When:** Dynamic content, CMS-driven pages, image grids.
**Intensity:** Very Low.

```tsx
<div className="rounded-2xl bg-muted animate-pulse h-[300px]" />

// Custom shimmer:
@keyframes skeleton {
  0% { background-position: -200% 0; }
  100% { background-position: 200% 0; }
}
.skeleton {
  background: linear-gradient(90deg, hsl(var(--muted)) 25%, hsl(var(--muted-foreground) / 0.1) 50%, hsl(var(--muted)) 75%);
  background-size: 200% 100%;
  animation: skeleton 1.5s ease-in-out infinite;
}
```

#### Effect L03: Stagger Page Entry
All sections on the page enter with a stagger on initial load.
**When:** Every page. This is the baseline "page feels alive" effect.
**Intensity:** Low (one-time).

```tsx
<motion.main
  initial="hidden"
  animate="visible"
  variants={{
    hidden: { opacity: 0 },
    visible: {
      opacity: 1,
      transition: { staggerChildren: 0.15 },
    },
  }}
>
  {sections.map((Section, i) => (
    <motion.div
      key={i}
      variants={{
        hidden: { opacity: 0, y: 30 },
        visible: { opacity: 1, y: 0, transition: { duration: 0.6, ease: [0.16, 1, 0.3, 1] } },
      }}
    >
      <Section />
    </motion.div>
  ))}
</motion.main>
```

---

## Phase 4: Implementation Order

When implementing effects, follow this sequence:

1. **Global effects first:** NoiseOverlay, CustomCursor, ScrollProgress, Navbar scroll behavior
2. **Hero section:** Headline effect, CTA effect, background atmosphere
3. **Section entrances:** Scroll-triggered reveals for all sections
4. **Interactive elements:** Card hovers, button effects
5. **Decorative:** Section dividers, floating elements, marquees
6. **Final pass:** Check timing conflicts, verify mobile, test reduced motion

---

## Phase 5: Verify

### The Squint Test
Squint at the page. The polished elements should be *felt* more than *seen*. If any effect jumps out as distracting, reduce its intensity or remove it.

### Checklist
- [ ] No two continuous animations compete in the same viewport
- [ ] Mobile has 50% fewer continuous effects
- [ ] `prefers-reduced-motion` disables all continuous animations
- [ ] Performance budget respected (check Performance Guardian)
- [ ] Effects reinforce content hierarchy, not fight it
- [ ] Page still looks great with JavaScript disabled (graceful degradation)

---

## Cross-Skill References

| When You Need... | Go To |
|:-----------------|:------|
| Choosing layout for polished section | **Layout Architect** |
| Animation timing and physics | **Motion Choreographer** |
| Performance impact of added effects | **Performance Guardian** |
| Existing Zaitex components to use | **Component Selector** |
| Verifying accessibility after polish | **Accessibility Auditor** |

---

## Key Principle
**Polish is the art of knowing where to stop.** A page with 5 perfectly chosen details beats a page with 25 competing effects. Every effect must pass one test: "Does this make the visitor *feel* something, or just *see* something?"
