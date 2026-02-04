---
name: web-debugger
description: Token-efficient debugging for web issues. Uses decision trees to diagnose problems quickly without broad exploration.
---

# Web Debugger — Agent-First Debugging

## Philosophy

**Debugging is expensive. Be surgical, not exploratory.**

This skill provides decision trees: check the most likely cause first, then escalate.

---

# DECISION TREES BY SYMPTOM

## 🐢 SLOW LOADING / PERFORMANCE

### First: Check Images

```
SYMPTOM: Site loads slowly

CHECK 1: Are images in public/ folder being used directly?
├── YES → Images are not optimized!
│   FIX: Use Next.js <Image> component instead of <img>
│   
│   // BAD (unoptimized, full size download)
│   <img src="/images/hero.jpg" />
│   
│   // GOOD (auto-optimized, lazy loaded)
│   import Image from "next/image";
│   <Image src="/images/hero.jpg" width={1200} height={800} alt="..." />
│
└── NO → Check image file sizes

CHECK 2: Are image files > 200KB?
├── YES → Images too large
│   FIX: Compress before adding to project
│   - Use squoosh.app or tinypng.com
│   - Convert to WebP format
│   - Resize to max 2000px width
│
└── NO → Move to next check

CHECK 3: Are there many images loading at once?
├── YES → Missing lazy loading
│   FIX: Add loading="lazy" or use Next.js Image (auto)
│
└── NO → Performance issue is not images
```

### Second: Check Fonts

```
CHECK 4: Are fonts loading slowly?
├── Check: Multiple font weights imported?
│   FIX: Max 3 weights per family (400, 500, 700)
│
├── Check: Fonts from external CDN?
│   FIX: Self-host via next/font
│   
│   import { Inter } from "next/font/google";
│   const inter = Inter({ subsets: ["latin"] });
│
└── Check: Flash of unstyled text (FOUT)?
    FIX: Add font-display: swap or use next/font
```

### Third: Check Bundle

```
CHECK 5: Large JavaScript bundle?
├── Check: Are heavy libraries imported in main bundle?
│   FIX: Dynamic import
│   
│   // BAD
│   import HeavyComponent from "@/components/HeavyComponent";
│   
│   // GOOD
│   const HeavyComponent = dynamic(() => import("@/components/HeavyComponent"));
│
└── Check: Is 3D code loading on all pages?
    FIX: Only import 3D on pages that use it
```

---

## 👻 COMPONENT NOT RENDERING

```
SYMPTOM: Component doesn't show up (no error)

CHECK 1: Is it imported correctly?
├── Typo in import path?
├── Wrong export (default vs named)?
│   
│   // If component uses: export default Foo
│   import Foo from "./Foo";  // Correct
│   
│   // If component uses: export function Foo
│   import { Foo } from "./Foo";  // Correct
│
└── File exists at that path?

CHECK 2: Is it conditionally hidden?
├── Check for: {condition && <Component />}
├── Is condition ever true?
├── Check for: style={{ display: "none" }} or visibility
│
└── Check for: className with opacity-0 or hidden

CHECK 3: Is the parent rendering?
├── If parent is conditionally rendered, child won't show
│
└── Check parent component for same issues

CHECK 4: Is it a server/client mismatch?
├── Component uses hooks but missing "use client"?
│   FIX: Add "use client" at top of file
│
└── Component uses browser APIs (window, document)?
    FIX: Wrap in useEffect or add "use client"
```

---

## 💥 HYDRATION ERRORS

```
SYMPTOM: "Hydration failed" or "Text content mismatch"

CHECK 1: Date/time rendering?
├── Dates render differently on server vs client
│   FIX: Use suppressHydrationWarning or format in useEffect
│
└── Check: new Date() in render? → Move to useEffect

CHECK 2: Random values?
├── Math.random() in render?
│   FIX: Generate in useEffect, store in state
│
└── UUID generation in render?
    FIX: Generate once, use key from data

CHECK 3: Browser-only APIs?
├── window.innerWidth in render?
├── localStorage in render?
│   FIX: All browser APIs in useEffect only
│
└── navigator, document in render?
    FIX: Guard with typeof window !== "undefined"

CHECK 4: Third-party scripts?
├── Script modifying DOM?
│   FIX: Load scripts dynamically with next/script
│
└── Browser extensions modifying page?
    FIX: Test in incognito mode
```

---

## 🎨 STYLING NOT WORKING

```
SYMPTOM: CSS not applying as expected

CHECK 1: Class name typo?
├── Tailwind class misspelled?
├── Using CSS Modules but forgot .module.css?
│
└── Custom class not defined in globals.css?

CHECK 2: Specificity issue?
├── Another style overriding?
│   DEBUG: Use browser DevTools → computed styles
│
├── !important somewhere?
│   FIX: Remove !important, fix cascade
│
└── Order of classes matters in Tailwind
    FIX: Later classes should override earlier

CHECK 3: CSS Modules import issue?
├── Using className={styles.foo}?
├── Class name in file matches what you're using?
│
└── Forgot to import styles?
    import styles from "./Component.module.css";

CHECK 4: Tailwind not processing?
├── File in content array in tailwind.config?
│   FIX: Ensure file path is included
│
└── Class being purged in production?
    FIX: Don't generate class names dynamically
    
    // BAD - will be purged
    className={`text-${color}-500`}
    
    // GOOD - full class name preserved
    className={variants[color]}
```

---

## 🔗 ROUTING / NAVIGATION ISSUES

```
SYMPTOM: Link not working or wrong page

CHECK 1: Using correct component?
├── For internal links: use next/link
│   import Link from "next/link";
│   <Link href="/about">About</Link>
│
└── For external links: use <a> with target="_blank"
    <a href="https://..." target="_blank" rel="noopener">

CHECK 2: Href path correct?
├── Starts with / for absolute paths?
├── File exists in app/ directory?
│
└── Dynamic route params correct?
    /blog/[slug] → /blog/my-post

CHECK 3: Page not found (404)?
├── File named page.tsx (not page.js or index.tsx)?
├── Correct folder structure?
│   app/about/page.tsx → /about
│
└── layout.tsx wrapping correctly?
```

---

## 🖼️ IMAGE ISSUES

```
SYMPTOM: Image not showing

CHECK 1: Path correct?
├── Public folder images: /image.jpg (not public/image.jpg)
├── Imported images: import img from "@/assets/image.jpg"
│
└── External images: Add domain to next.config.js
    images: { domains: ["example.com"] }

CHECK 2: Next.js Image specific?
├── Missing width/height or fill?
│   FIX: Always specify dimensions or use fill
│
├── Using fill without parent positioning?
│   FIX: Parent needs position: relative
│
└── Unoptimized external image?
    FIX: Add to next.config.js images.remotePatterns

CHECK 3: Image exists?
├── Check file actually exists at path
├── Check case sensitivity (Linux servers are case-sensitive)
│
└── Check file extension matches (.jpg vs .jpeg vs .png)
```

---

## 🎬 ANIMATION ISSUES

### Animation Not Playing

```
SYMPTOM: Animation doesn't trigger or play

CHECK 1: Is it a client component?
├── Framer Motion requires "use client"
│   FIX: Add "use client" at top of file
│
└── Check: Any hooks used? → Must be client component

CHECK 2: Is the animation trigger correct?
├── Framer Motion:
│   - whileInView: Element must enter viewport
│   - animate: Plays immediately on mount
│   - whileHover: Only on mouse hover
│
├── GSAP:
│   - Is gsap.registerPlugin(ScrollTrigger) called?
│   - Is useGSAP hook wrapping the animation?
│
└── Check: Is animation inside conditional render that's false?

CHECK 3: Is the component mounted?
├── Animation inside useEffect with empty deps? → Runs once on mount
├── Animation depends on state that hasn't updated?
│
└── Try adding a console.log to confirm component renders

CHECK 4: Are animation props correct?
├── Framer Motion:
│   - initial, animate, exit all need matching keys
│   - variants must match the keys used
│
└── GSAP:
    - Selector exists? (gsap.to(".my-class") → is .my-class in DOM?)
    - GSAP runs before DOM ready? → Use useGSAP or useLayoutEffect
```

### Animation Performance (Jank/Stutter)

```
SYMPTOM: Animation is choppy or stutters

CHECK 1: Are you animating expensive properties?
├── BAD: width, height, top, left, margin, padding
│   These trigger layout recalculation every frame
│
├── GOOD: transform, opacity
│   These are GPU-accelerated
│
└── FIX: Use transform instead
    // BAD
    animate={{ left: 100 }}
    
    // GOOD
    animate={{ x: 100 }}

CHECK 2: Too many elements animating?
├── Check: Animating 50+ elements simultaneously?
│   FIX: Stagger them or reduce count
│
└── Check: Particle systems or many moving objects?
    FIX: Use CSS animations or canvas for many items

CHECK 3: Animation causing re-renders?
├── State updating every frame?
│   FIX: Use useRef for values that don't need re-render
│
├── Framer Motion: Use motion values instead of state
│   const x = useMotionValue(0);
│
└── GSAP: Animations are outside React render cycle (usually fine)

CHECK 4: Memory leak?
├── Animation never stops?
├── Scroll listener not cleaned up?
│
└── FIX: Return cleanup function from useEffect
    useEffect(() => {
      const animation = gsap.to(...);
      return () => animation.kill();
    }, []);
```

### Framer Motion Specific

```
SYMPTOM: Framer Motion animation broken

CHECK 1: Missing AnimatePresence for exit animations?
├── Exit animations only work inside <AnimatePresence>
│
└── FIX:
    <AnimatePresence>
      {show && <motion.div exit={{ opacity: 0 }} />}
    </AnimatePresence>

CHECK 2: whileInView not triggering?
├── Element must be in viewport
├── Parent has overflow: hidden cutting it off?
│
└── FIX: Add viewport={{ once: true, margin: "-100px" }}

CHECK 3: Variants not applying?
├── Check: Are variant keys matching?
│   variants={{ hidden: {...}, visible: {...} }}
│   initial="hidden" animate="visible"
│
└── Check: Parent has variants but children don't inherit?
    FIX: Add variants to children or use staggerChildren

CHECK 4: Layout animations broken?
├── Using layout prop?
├── Other elements not using layout?
│
└── FIX: All siblings should have layout prop for smooth transitions
```

### GSAP / ScrollTrigger Specific

```
SYMPTOM: GSAP animation not working

CHECK 1: Plugin registered?
├── ScrollTrigger needs registration
│   FIX: gsap.registerPlugin(ScrollTrigger);
│
└── Same for TextPlugin, SplitText, etc.

CHECK 2: Running before DOM ready?
├── Animation runs on SSR (server)?
│   FIX: Use useGSAP hook or check typeof window
│
└── Element doesn't exist when GSAP runs?
    FIX: Use refs, not class selectors
    
    // BAD - might not exist
    gsap.to(".my-element", {...});
    
    // GOOD - guaranteed to exist
    const ref = useRef(null);
    gsap.to(ref.current, {...});

CHECK 3: ScrollTrigger not firing?
├── Trigger element correct?
│   scrollTrigger: { trigger: ".element" }
│
├── Start/end positions off-screen?
│   FIX: Check start: "top 80%" means when top of element hits 80% of viewport
│
└── Page height changed after ScrollTrigger initialized?
    FIX: ScrollTrigger.refresh() after dynamic content loads

CHECK 4: Animation works but snaps/jumps?
├── scrub: true should make it smooth
├── If using scrub: 1, animation takes 1 second to catch up
│
└── Check: Animation values reasonable for scroll distance?
```

---

## 🔧 BUILD ERRORS

```
SYMPTOM: Build fails

CHECK 1: Read the error message carefully
├── Line number mentioned? → Go directly there
├── Module not found? → Check import path
│
└── Type error? → Fix TypeScript type

CHECK 2: Common build errors
├── "Cannot find module"
│   FIX: npm install, check package.json
│
├── "Unexpected token"
│   FIX: Syntax error, check for missing brackets/quotes
│
├── "X is not a function"
│   FIX: Wrong import (default vs named)
│
└── "window is not defined"
    FIX: Code running on server, add "use client" or useEffect
```

---

# DEBUGGING PROTOCOL

When user reports an issue:

```
1. IDENTIFY the symptom category (above)
2. FOLLOW the decision tree in order
3. CHECK the most likely cause FIRST
4. FIX before moving to next check
5. VERIFY the fix worked

DO NOT:
- Search the entire codebase blindly
- Read large files to "understand context"
- Try multiple fixes simultaneously
- Guess without checking
```

---

# COMMON PITFALLS (Agent Mistakes)

| Mistake | Why It's Wrong | Do This Instead |
|:--------|:---------------|:----------------|
| Using `<img>` for local images | No optimization, full file served | Use `next/image` |
| Dropping images in public/ at full size | 5MB images load slow | Optimize first, max 200KB |
| Adding "use client" everywhere | Breaks SSR benefits | Only where needed |
| Dynamic Tailwind classes | Gets purged in prod | Use object lookup |
| Browser APIs in render | Hydration errors | Wrap in useEffect |
| Re-reading whole files to debug | Token waste | Check specific lines |
