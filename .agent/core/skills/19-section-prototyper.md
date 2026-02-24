---
name: section-prototyper
description: Creative gate skill. Converts locked DNA v2 into real Next.js section prototypes (2–3 max) to validate direction before full production. Strictly forbidden to redefine identity. Redirects to 18.5 if uncertainty appears.
---

# Section Prototyper (19)

## TL;DR
**Phase:** Concept → Production Bridge  
**Input:** Active DNA v2 (locked) + direction-merge output (from 18.5 or Aura path)  
**Output:** 2–3 real Next.js sections (production-grade structure)  
**Change Budget:** LARGE (2–3 sections max; no full build)
**Stop:** After 2–3 sections validated  
**Redirect:** If identity unclear → 18.5. If structural debt appears → rebuild module, not patch.

---

# Objective

Section Prototyper is the **creative gate**.

It exists to:
- Translate DNA v2 into real production-ready structure.
- Validate spacing, hierarchy, motion, and responsiveness.
- Catch implementation issues before scaling the build.

It does NOT:
- Redesign identity.
- Re-open direction debates.
- Explore alternative vibes.
- Perform full-page builds.

---

# Preconditions (Hard Gate)

You may NOT run this skill unless:

1) **Active DNA v2 is locked**
2) A clear direction has been selected (from 18.5 or Aura alignment)
3) There is no stylistic uncertainty
4) MODE is LITE or ENGINE  
   (In AURA mode this skill is usually skipped.)

If any of the above is false:
→ STOP  
→ Redirect to `18.5-section-sandbox`

---

# When to Run

Run 19 when:
- Concept direction is approved.
- You want to validate real production layout behavior.
- You need to test spacing rhythm in real breakpoints.
- You need proof before scaling to entire site.

Do NOT run 19 for:
- Minor tweaks
- Aura-only alignment
- Bug fixes
- Design exploration

---

# Scope Rules

19 builds only:

- Hero section
- One supporting structural section (e.g., Services / Bento / Feature grid)
- Optional third section only if needed to validate pacing

Maximum: 3 sections.

Not allowed:
- Navbar
- Footer
- Full page assembly
- Multi-page scaffolding
- SEO polish
- Performance optimization pass

This is validation, not full production.

---

# Implementation Rules

Unlike 18.5, this is real production code.

Use:
- Next.js structure
- Existing component architecture
- Existing UI primitives
- Motion system already defined
- Design tokens from active-dna.md

Do NOT:
- Create new global design tokens
- Modify tailwind config globally
- Add new dependencies
- Reinterpret the visual language
- Add placeholder hacks “just for now”

---

# Identity Lock Rule

19 must respect:

- Radius system
- Surface language
- Typography scale
- Spacing scale
- Image strategy
- Motion intensity

If you feel tempted to:
- Change border radii
- Introduce new surface style
- Switch image strategy
- Increase density dramatically
- “Fix vibe” globally

→ STOP  
→ Redirect to 18.5.

19 is not allowed to redefine identity.

---

# Build Discipline

Each section must:

- Be self-contained
- Follow modular architecture
- Stay under ~300 lines per module (preferred)
- Avoid cascading style overrides
- Avoid hard-coded spacing outside DNA scale

If code begins to require workarounds:
- Stop and simplify
- Rebuild that section cleanly
- Do not layer hacks

---

# Validation Checklist

After building 2–3 sections:

Check:

- Desktop hierarchy clarity
- Mobile readability
- CTA dominance
- Rhythm between sections
- Image crop consistency
- Motion smoothness (no jank)
- No console errors

If issues are identity-level → redirect to 18.5  
If issues are local → route to Micro Editor (21)  

---

# Stop Condition

Stop after:

- 2–3 validated sections exist
- DNA v2 feels correctly translated into code
- No structural debt introduced

Do NOT continue building additional sections.

Scaling happens in Production Phase via:
- 02 → 03 → 04 → 05 → 06 → etc.

---

# Escalation Rules

If prototype reveals:

### Identity mismatch
→ 18.5

### Structural mess / hacks emerging
→ Rebuild section cleanly (05-component-architect)

### Bug / rendering issue
→ 15-web-debugger → 21-micro-editor

---

# Output Format

At completion, report:

- Sections created
- Files added
- Approximate LOC per section
- Any constraints discovered
- Confirmation that DNA v2 was respected
- Explicit STOP

---

# Core Principle

18.5 explores.
19 validates.
Production scales.

If 19 starts exploring, it has violated the system.