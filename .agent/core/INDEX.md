---
name: INDEX
description: Phase router + execution controller for Zaitex Engine. Always read this AFTER START_HERE. This file decides the current MODE, which skills are allowed, and where to redirect when uncertain. Runtime routing happens here — NOT in skill-routing.md.
---

# Zaitex Engine — INDEX (Phase Router)

## TL;DR
**Runtime routing is:**
1) Read `.agent/START_HERE.md`  
2) Read this `INDEX.md`  
3) Identify **MODE** + **PHASE**  
4) Activate **ONE** skill (or the allowed 2-step sequence explicitly listed)  
5) Respect **Change Budget**  
6) Stop and report
7) Read ONLY that skill’s TL;DR block first

**If uncertain about style/structure → redirect to 18.5.**  
**If using Aura templates → concept is pre-done; do not run 18/18.5/19 unless needed.**

---

# 0) First Decision: MODE

Choose MODE based on project reality:

## MODE A — AURA (Template-Accelerated)  ✅ default for most small/medium projects
Use when:
- Client needs “modern premium upgrade” (e.g., 2007 → 2026)
- Speed matters
- Aura template quality is sufficient
- No need to invent a new layout language

Core idea:
**Aura already solved concepting.** You execute and align.

## MODE B — LITE (Fast Custom)
Use when:
- Aura doesn’t fit
- You still want a custom feel
- But you do NOT need deep concept exploration

Core idea:
**Minimal concept pass, then build.**

## MODE C — ENGINE (Full Custom)
Use when:
- High-ticket / portfolio case / unique layout language
- Brand identity needs concepting
- You expect multiple rounds of style exploration

Core idea:
**Concept hard first, then execute.**

---

# 1) Problem Type Router (before choosing a skill)

Identify what the user is asking:

### STYLE / IDENTITY CHANGE (global)
Examples:
- round ↔ sharp, glass ↔ flat, “more editorial”, “more warm”, “change the whole feel”
→ **Always return to 18.5** (even mid-production). Lock DNA update before proceeding.

### LOCAL TWEAK (section-level)
Examples:
- spacing feels tight, CTA hierarchy, swap images, adjust grid in one section
→ Stay in production. Use Micro Editor + appropriate single skill.

### BUG / BROKEN BEHAVIOR
Examples:
- layout breaks, hydration, animation bug, event handling, console errors
→ Use 15-web-debugger (decision-tree), then Micro Editor.

### QUALITY / POLISH
Examples:
- “feels cheap”, “needs premium”, micro interactions, finishing
→ 16-polish-pass + 09-style-propagator (if consistency issue)

---

# 2) Phase Definitions

Phases are gated. Only allowed skills may run in a phase.

## PHASE 0 — Intake & Routing
Goal: decide MODE, gather constraints, set direction entry.
Allowed skills:
- `00-brief-architect` (required)

Outputs required:
- brief artifacts
- MODE decision: AURA / LITE / ENGINE
- asset folder path(s) if available (images/videos)

Stop condition:
- Do not proceed without explicit MODE.

---

## PHASE 1 — DNA & Concept Entry (depends on MODE)

### MODE AURA
Goal: select Aura template + prepare migration inputs.
Allowed skills:
- `00-brief-architect` (template selection signals)
- `17-aura-migration`

Optional:
- `18.5-section-sandbox` (ONLY if template mismatch or client requests identity shift)

Hard rule:
- **Do NOT run 18-brand-moodboard or 19-section-prototyper by default in Aura mode.**

### MODE LITE
Goal: quick direction lock without deep exploration.
Allowed skills:
- `18-brand-moodboard` (light)
- `18.5-section-sandbox` (mini pass; limited iterations)

Stop condition:
- Direction chosen + DNA locked (v2 or v2-lite).

### MODE ENGINE
Goal: full concept lock.
Allowed skills:
- `18-brand-moodboard`
- `18.5-section-sandbox`
- `19-section-prototyper` (creative gate)

Stop condition:
- DNA locked + prototype proves direction.

---

## PHASE 2 — Production Build (execution only)
Goal: build pages/sections without changing identity.
Allowed skills:
- `02-page-planner`
- `03-layout-architect`
- `04-component-selector`
- `05-component-architect`
- `06-motion-choreographer`
- `07-copywriter`
- `14-seo-specialist` (apply continuously)

Hard rule:
- If any “style uncertainty” appears → **STOP** → redirect to **18.5**.

Hard rule:
Default for small adjustments: 21-micro-editor.
If adjustment grows beyond budget → escalate.

---

## PHASE 3 — Consistency, Performance, QA
Goal: consistency + speed + correctness.
Allowed skills:
- `09-style-propagator`
- `08-performance-guardian`
- `10-accessibility-auditor`
- `11-browser-validator`

---

## PHASE 4 — Polish & Ship
Goal: premium finish + deploy.
Allowed skills:
- `16-polish-pass`
- `12-deployment-packager`

---

# 3) Mandatory Redirect Rules (anti-drift)

## Redirect to 18.5 (Design Lab) when:
- “Feels off” but user cannot specify
- Conflicting feedback exists (“both minimal and editorial are good”)
- Identity-level changes are requested
- You are about to change radius/surface/typography energy/image strategy globally
- You are tempted to “improve the whole site” without a locked direction

## Redirect to 15 (Debug) when:
- There is a bug / error / broken behavior
- Something is inconsistent across browsers
- Motion causes jank or breaks layout

## Redirect to Micro Editor when:
- User wants a narrow change in one file
- A small fix can be applied surgically
- You must respect a strict diff budget

---

# 4) Allowed Skill Sequences (the ONLY multi-skill passes)

By default: **ONE skill per run.**

Allowed 2-step sequences:

### Bug fix
1) `15-web-debugger`
2) `21-miccro-editor.md` (apply patch)

### Production consistency fix
1) `09-style-propagator`
2) `21-miccro-editor.md` (apply minimal alignments)

### Aura path build
1) `17-aura-migration`
2) `07-copywriter` (then stop; subsequent steps are separate runs)

Anything beyond this requires explicit user instruction:
`UNLOCK: allow multi-skill pass`

---

# 5) Preconditions (gates) for key skills

## 17-aura-migration Preconditions
- Aura template selected
- Target project structure exists (where to migrate to)
- Assets folder identified or placeholders approved
If missing → return to 00 to collect.

## 18.5-section-sandbox Preconditions
- Moodboard exists OR user requests direction exploration
- Image folder exists OR placeholders allowed
If user only wants quick build → use LITE rules or Aura.

## 19-section-prototyper Preconditions (must be strict)
- DNA locked (or 18.5 completed)
- Direction chosen
- No unresolved style uncertainty
If ANY uncertainty → **redirect to 18.5**

---

# 6) Change Budgets (global rule)

Every run must declare a change budget before editing:

- **Micro**: 1 file, ≤ 80 lines changed
- **Small**: ≤ 3 files, ≤ 200 lines changed total
- **Medium**: ≤ 8 files, ≤ 500 lines changed total
- **Large**: only allowed in Concept phases (18.5/19) or Aura migration

If the requested task exceeds the budget:
- stop
- propose the smallest possible next move
- or redirect to correct phase

---

# 7) Quick Start Recipes

## Recipe: AURA (small/medium client, fastest premium)
1) `00-brief-architect` → decide MODE=AURA + pick template
2) `17-aura-migration` → migrate template into project
3) `07-copywriter` → replace copy + tone
4) `09-style-propagator` → align with DNA
5) `14-seo-specialist` → meta, H1, structure
6) `16-polish-pass` → premium finishing
7) `08/10/11` → performance + QA
8) `12-deployment-packager` → ship

If client requests identity shift → jump to `18.5` (mini), then continue.

## Recipe: LITE (custom but fast)
1) `00-brief-architect` → MODE=LITE
2) `18-brand-moodboard` (light) → establish direction
3) `18.5-section-sandbox` (mini) → lock direction + image strategy
4) Production build (02→03→04→05→06→07→14)
5) QA + ship (09→08→10→11→16→12)

## Recipe: ENGINE (full custom)
1) `00` → MODE=ENGINE
2) `18` → moodboard
3) `18.5` → sandbox (full) + lock DNA
4) `19` → prototype gate (2–3 sections)
5) Production + QA + ship

---

# 8) Notes (important)
- `Pipeline reference.md` is **reference-only**. Never use it to route runtime work.
- If you are in production and you feel tempted to redesign: **you are in the wrong phase.**
- In production: do not read the whole engine. Read only:
  - START_HERE
  - INDEX
  - the single chosen skill

- Skills are activated via TL;DR first.
- Deep reading is allowed only within the selected skill.

---