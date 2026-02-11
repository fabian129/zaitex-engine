---
name: skill-routing
description: Mandatory routing sheet. Read this when starting any task and when switching between tasks. It tells you which skill to use, when to switch skills, and how skills feed into each other. If in doubt, check this sheet. Always.
---

# Skill Routing Sheet

## How to Use This Document
You are an agent with 16 skills. This sheet tells you **when to activate each one** and **when to hand off to another**. It is not a summary of what skills do — it is a routing table.

Read this at the start of every task. Re-read it every 5-10 prompts to check you haven't drifted.

---

## The Pipeline (Default Order)

```
01 Design Director → 02 Page Planner → 03 Layout Architect → 04 Component Selector
→ 05 Component Architect → 06 Motion Choreographer → 07 Copywriter
→ 08 Performance Guardian → 09 Style Propagator → 10 Accessibility Auditor
→ 11 Browser Validator → 12 Deployment Packager
```

**Parallel skills (use anytime):**
- `13 Immersive Architect` — only when 3D is involved
- `14 SEO Specialist` — during build (meta, headings, schema) AND before deploy (audit)
- `15 Web Debugger` — when something breaks
- `16 Polish Pass` — after the page works, before deployment
- `17 Aura Migration` — when converting Aura.build exports

---

## Routing Rules

### Starting a New Project (from scratch)

| Step | Skill | What You Produce | Stop Condition |
|:-----|:------|:-----------------|:---------------|
| 1 | **Design Director** | Design concept / DNA file | User approves a direction |
| 2 | **Page Planner** | Section flow with goals per section | User confirms structure |
| 3 | **Copywriter** | Headlines, CTAs, body copy per section | Copy approved (DO THIS BEFORE LAYOUT — copy length affects layout) |
| 4 | **Layout Architect** | Layout plan per section | — |
| 5 | **Component Selector** | Component list per section | — |
| 6 | **Component Architect** + **Motion Choreographer** | Built sections with animations | All sections render |
| 7 | **SEO Specialist** | Meta tags, schema, headings, sitemap | Applied during build |
| 8 | **Performance Guardian** | Optimization pass | All checks pass |
| 9 | **Style Propagator** | Tokens verified, config updated | Single source of truth confirmed |
| 10 | **Polish Pass** | Micro-details and effects | User approves polish map |
| 11 | **Accessibility Auditor** | Contrast, semantics, focus states | WCAG AA pass |
| 12 | **Browser Validator** | Visual QA | No violations |
| 13 | **Deployment Packager** | Env, analytics, deploy guide | Ready to ship |

### Starting from Aura Migration

| Step | Skill | What You Produce |
|:-----|:------|:-----------------|
| 1 | **Aura Migration** | Migration map → components | 
| 2 | **Style Propagator** | Extract tokens into active-dna.md and style-config.ts |
| 3 | **SEO Specialist** | Add meta, schema, headings (Aura files have none) |
| 4 | **Performance Guardian** | Validate images, animations, bundle |
| 5 | **Polish Pass** | Add micro-details if needed |
| 6 | **Accessibility Auditor** | Check contrast, alt text, focus states |
| 7 | **Deployment Packager** | Ship it |

### Adding a New Page to Existing Project

| Step | Skill |
|:-----|:------|
| 1 | **Style Propagator** — Read `active-dna.md` and `style-config.ts` FIRST |
| 2 | **Page Planner** — Plan sections |
| 3 | **Copywriter** — Write copy before building |
| 4 | **Layout Architect** → **Component Selector** → **Component Architect** + **Motion Choreographer** |
| 5 | **SEO Specialist** — Meta, headings, schema |
| 6 | **Performance Guardian** → **Polish Pass** → **Accessibility Auditor** |

### Fixing a Bug

| Step | Skill |
|:-----|:------|
| 1 | **Web Debugger** — Follow the decision tree for the symptom |
| 2 | If animation bug → also check **Motion Choreographer** (GSAP scope, Lenis conflicts) |
| 3 | If visual mismatch → check **Style Propagator** (is the component using tokens or hardcoded values?) |
| 4 | If performance issue → check **Performance Guardian** |

---

## Skill-to-Skill Triggers

These are the specific conditions where one skill MUST hand off to another. This is the most important section.

### Design Director
- **When done →** hand off to **Page Planner** with the approved DNA
- **If user provides a reference URL →** use Design Director to analyze it, don't skip to building
- **If user provides an Aura file →** skip Design Director, go to **Aura Migration**

### Page Planner
- **When done →** hand off to **Copywriter** BEFORE Layout Architect
- **If a section's goal is unclear →** stop and ask the user, don't guess
- **If the page is a single landing page →** still plan sections, don't skip this

### Copywriter
- **When done →** hand off to **Layout Architect** (copy informs layout, not the other way around)
- **If headline is >8 words →** flag to Layout Architect that hero needs more width
- **If CTA text is vague ("Learn More") →** rewrite it to be specific before proceeding

### Layout Architect
- **When choosing patterns →** check **Component Selector** for which components fit
- **If the layout needs sticky/pinned scrolling →** flag for **Motion Choreographer** (GSAP required)
- **If the layout is a Bento grid →** verify responsive behavior down to mobile before proceeding

### Component Selector
- **When selecting background layers →** check intensity against DNA motion level
- **If selecting 3+ animated background layers →** flag for **Performance Guardian** AND ensure `useReducedMotion` fallback
- **If a needed component doesn't exist →** hand off to **Component Architect**

### Component Architect
- **When building any component with state →** follow the Zaitex Standard (shell/core separation)
- **When component needs animation →** hand off animation logic to **Motion Choreographer**, don't inline it
- **When component is used >2 times →** register it in **Style Propagator** config

### Motion Choreographer
- **For hover/click/tap →** use Framer Motion
- **For scroll-linked animation →** use GSAP + ScrollTrigger with `useGSAP` + `{ scope: ref }`
- **For page entrance →** use Framer Motion `initial` + `animate`
- **For pinned sections →** use GSAP ScrollTrigger (Framer cannot pin)
- **For text character animation →** use GSAP + SplitType
- **NEVER use `useEffect` for GSAP.** Always `useGSAP`.
- **NEVER use global CSS selectors in GSAP.** Always scoped to a ref.
- **If Lenis + ScrollTrigger pin conflict →** check Web Debugger decision tree

### Copywriter
- **Must run BEFORE Layout Architect** — copy length determines layout
- **If writing for SEO →** coordinate with **SEO Specialist** for keyword placement
- **If writing CTAs →** make them specific actions, not generic "Learn More"

### Performance Guardian
- **Runs AFTER all sections are built, BEFORE Polish Pass**
- **If `next/image` is missing anywhere →** fix immediately, don't just flag
- **If feTurbulence is found →** OK if it's the NoiseOverlay at opacity < 0.05. NOT OK if animated or higher opacity
- **If animations use `width`, `height`, `top`, `left` →** replace with `transform` equivalents
- **If total page has >8 scroll-linked GSAP animations →** review and consolidate

### Style Propagator
- **Runs after building AND after any Aura Migration**
- **If a component uses hardcoded hex values →** replace with design tokens
- **If a new page is being built →** read `active-dna.md` FIRST before writing any code
- **After migration →** extract all Aura CSS variables into `active-dna.md` and `style-config.ts`

### Accessibility Auditor
- **Runs AFTER Polish Pass** (polish can introduce new contrast issues)
- **If white/light text on light background →** fix immediately
- **If icon-only button →** add `aria-label`
- **If decorative image →** use `alt=""`
- **If interactive element <44px →** increase touch target

### Browser Validator
- **Runs AFTER Accessibility Auditor**
- **Fix violations directly** — don't just report them
- **If horizontal scroll at 375px →** add responsive classes
- **If layout shift detected →** check images for missing dimensions

### SEO Specialist
- **Apply DURING build** (meta tags, headings, alt text, schema) — not just at the end
- **Each page needs:** unique title (50-60 chars), unique description (150-160 chars), one H1, OG image
- **After Aura Migration →** Aura files have zero SEO. Add everything.
- **Before deploy →** run full audit checklist

### Web Debugger
- **ONLY activate when something is broken** — not preventatively
- **Follow the decision tree for the symptom** — don't explore broadly
- **Common miss:** Lenis + GSAP ScrollTrigger pin conflict → check if `ScrollTrigger.scrollerProxy` is needed
- **Common miss:** `useEffect` instead of `useGSAP` → animations run before DOM ready or don't clean up

### Polish Pass
- **Runs AFTER Performance Guardian, BEFORE Accessibility Auditor**
- **Present the Polish Map to the user before implementing** — always
- **Max 3 high-intensity effects per page**
- **Max 1 continuous animation visible in viewport at once**
- **Mobile: cut continuous animations by 50%**
- **Every effect must answer: "Does this reinforce the content's purpose?"**
- **When choosing effects →** use the effect code from the library (B01-B10, C01-C12, etc.), don't invent new ones

### Aura Migration
- **Triggers when user provides an Aura.build HTML file**
- **Present migration map before writing code** — always
- **Every `<img>` → `next/image` with `fill` + `sizes` + `alt`**
- **Every GSAP call → `useGSAP` with `{ scope: ref }`**
- **After migration →** run Style Propagator, SEO Specialist, Performance Guardian in sequence
- **Does NOT redesign.** Matches the Aura visual output exactly.

### Immersive Architect
- **Only activates when 3D is requested**
- **Max 50k triangles per scene**
- **Always provide static fallback image**
- **If scene feels messy →** check Crystallize checkpoint (RED/GREEN flags)

---

## Common Drift Patterns (What Goes Wrong)

These are the mistakes agents make after 10+ prompts. Re-read this section when you feel lost.

| Drift | What Happens | Fix |
|:------|:-------------|:----|
| **Skipping Copywriter** | Agent builds layout first, then jams in copy that doesn't fit | Always write copy BEFORE choosing layout |
| **Skipping Page Planner** | Agent starts coding sections without a plan, sections feel random | Even a simple plan prevents this |
| **Polish during build** | Agent adds effects while building structure, creates messy code | Build clean first, polish as separate pass |
| **Hardcoding values** | Agent uses `bg-[#22C55E]` instead of `bg-primary` | Check Style Propagator — use tokens always |
| **Global GSAP selectors** | Agent uses `.card-item` instead of scoped ref | Every GSAP animation scoped to ref |
| **useEffect for GSAP** | Animation runs on server, no cleanup, memory leaks | Always `useGSAP` with scope |
| **Ignoring mobile** | Agent builds desktop-first and forgets responsive | Start mobile, add `md:` and `lg:` |
| **Too many effects** | Agent adds every cool thing it knows, page becomes a circus | Max 3 high-intensity per page, follow Polish Pass budget |
| **No stop points** | Agent runs through entire build without asking user | Stop after: DNA, page plan, copy, migration map, polish map |
| **Forgetting SEO** | Agent builds entire page with no meta tags or schema | Apply SEO DURING build, not just before deploy |
| **Redesigning Aura output** | Agent "improves" the design during migration | Aura Migration preserves design exactly. Period. |
| **Copying reference style** | Agent changes fonts/colors/radius to match a mid-build reference | Extract PATTERN only. Style comes from DNA. Always. |
| **Running full pipeline in sandbox** | Agent runs Design Director + Page Planner + Copywriter when user just wants to experiment | Skip to build. Iterate fast. Formalize later. |

---

## Mid-Build Reference Protocol

The user will frequently share reference images, URLs, or screenshots from Awwwards, Dribbble, or other sites **in the middle of building**. This is not a request to change the project's DNA. It is a request to extract a **pattern** and build it in the project's existing style.

### The Two-Layer Rule

Every reference has two layers. You extract one and ignore the other:

| Layer | Definition | Action |
|:------|:-----------|:-------|
| **Pattern** (EXTRACT) | Layout structure, component type, information hierarchy, how elements relate to each other, spacing *ratios*, visual rhythm | Use this. Build it. |
| **Style** (IGNORE) | Colors, fonts, border-radius, shadows, specific spacing values, animation choices | Discard. Use project DNA instead. |

### Examples

**User shows:** A metrics section with three large numbers in a row, separated by thin vertical lines, with small labels below each number.
**Pattern to extract:** Horizontal layout, three stats, vertical dividers, number + label hierarchy.
**Style to ignore:** The reference's font (you use yours), the reference's colors (you use yours), the reference's border-radius (you use yours).
**You build:** That exact layout structure using `active-dna.md` tokens, project fonts, project spacing scale.

**User shows:** A bento grid with glassmorphism cards, one large featured card spanning two rows.
**Pattern to extract:** Bento grid, mixed card sizes, featured card at 2x height, content hierarchy within cards.
**Style to ignore:** The glassmorphism values, the border-radius, the card colors.
**You build:** A bento grid using project card styles, project radius, project shadows. If the project DNA has sharp corners, the cards have sharp corners — even if the reference had rounded ones.

**User shows:** A hero section with a diagonal image split and text overlapping the image edge.
**Pattern to extract:** Diagonal composition, image-text overlap, broken grid layout.
**Style to ignore:** The specific angle, the font choices, the color palette.
**You build:** That composition pattern using Layout Architect's "Broken Grid" or "Overlap" patterns, styled with project DNA.

### The Process

When user shares a mid-build reference:

1. **Acknowledge the pattern:** "I see — [describe the pattern you're extracting]."
2. **Confirm the extraction:** "I'll build this with our existing DNA. The structure will match the reference, the styling stays ours."
3. **Build it.** Don't ask 5 follow-up questions. Don't run Design Director. Just extract the pattern and go.
4. **Only ask if ambiguous:** If the reference has a genuinely new interaction pattern (e.g., a component type you haven't built before), ask: "This uses [X pattern] which we don't have yet. Should I build it as a new component or adapt an existing one?"

### What NOT to Do

- ❌ Don't run Design Director to "analyze" a mid-build reference
- ❌ Don't update `active-dna.md` based on a mid-build reference
- ❌ Don't override Signatures — if `active-dna.md` says "sharp corners" and the reference has rounded corners, you keep sharp corners
- ❌ Don't change fonts, colors, or border-radius to match the reference
- ❌ Don't ask "should this affect the whole site?" — the answer is always no
- ❌ Don't treat a reference image as a pixel-perfect spec — it's a pattern source

---

## Sandbox Mode

When the user is experimenting — building components for fun, testing ideas, exploring new patterns — the full pipeline is overkill. Sandbox mode is faster and looser.

### When to Activate
- User says "let's experiment", "I want to try something", "just build it quick", "sandbox"
- User is building components for their own portfolio/agency, not a client
- User is iterating rapidly on a single section or component
- User is exploring a new effect or animation

### Sandbox Rules

| Normal Pipeline | Sandbox Mode |
|:----------------|:-------------|
| Design Director → Page Planner → Copywriter → Layout → Build | Skip to build. Use existing DNA. |
| Stop points for approval | Build fast, show result, iterate |
| Performance Guardian before polish | Skip unless user asks |
| Full SEO pass | Skip entirely |
| Accessibility audit | Skip unless user asks |
| Deployment Packager | Skip — this isn't shipping yet |

### What STILL Applies in Sandbox
- **Style Propagator:** Still use design tokens, not hardcoded values. Even experiments should be in the project's visual language.
- **Motion Choreographer:** Still use `useGSAP` with scope. Bad habits in sandbox leak into production.
- **Component Architect:** Still separate logic from layout. A good experiment becomes a real component later.
- **Polish Pass:** Actually — sandbox is the BEST time to try Polish Pass effects. User wants to see what B01 Shimmer Sweep looks like? Build it immediately.

### Sandbox Workflow
```
1. User describes what they want to try
2. Build it immediately (no planning phase)
3. Show result
4. User says "tweak X" or "try Y instead"
5. Iterate rapidly
6. When user is happy: "Let's keep this" → extract into proper component with full standards
```

---

## Quick Reference: "I'm Doing X, Which Skill?"

| I'm doing... | Use skill... |
|:-------------|:-------------|
| Starting a brand new project | 01 Design Director |
| Planning what sections a page needs | 02 Page Planner |
| Writing headlines and body text | 07 Copywriter |
| Choosing grid vs flex vs bento | 03 Layout Architect |
| Picking which components to use | 04 Component Selector |
| Building a new reusable component | 05 Component Architect |
| Adding entrance/scroll/hover animations | 06 Motion Choreographer |
| Converting an Aura.build file | 17 Aura Migration |
| Optimizing images and bundle | 08 Performance Guardian |
| Making sure colors and tokens are consistent | 09 Style Propagator |
| Adding micro-details and signature effects | 16 Polish Pass |
| Checking contrast, aria, semantics | 10 Accessibility Auditor |
| Visual QA in browser | 11 Browser Validator |
| Adding meta tags, schema, sitemap | 14 SEO Specialist |
| Preparing for Vercel deploy | 12 Deployment Packager |
| Something is broken | 15 Web Debugger |
| Building 3D scenes | 13 Immersive Architect |
| User shows a reference mid-build | Mid-Build Reference Protocol (above) |
| User wants to experiment/iterate fast | Sandbox Mode (above) |

---

## The One Rule
**If you're about to make a decision and you're not sure which skill covers it — re-read this sheet.** The answer is here. If it's genuinely not here, ask the user.
