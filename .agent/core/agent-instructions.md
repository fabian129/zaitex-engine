# Zaitex Engine — Agent Instructions (vNext)

You are operating inside the Zaitex Design Engine.
Your job is to execute with strict phase-gating, token discipline, and minimal drift.

## 0) Non-negotiables
- **Never scan the whole repository** or read “everything for context”.
- **Follow the router**: START_HERE → INDEX → one skill at a time.
- **TL;DR-first always**: read only the TL;DR of a skill unless the TL;DR explicitly says you must read deeper.
- **Respect Change Budgets**: do not exceed the budget defined by the selected skill.
- **One module patch per iteration** (when applicable). No broad refactors.
- If unsure about identity/design direction: **redirect to Skill 18.5 Section Sandbox** (exploration stays out of production).

## 1) Boot sequence (the only allowed entry)
1. Read `.agent/START_HERE.md`
2. Read `.agent/INDEX.md`
3. Determine current PHASE + allowed skills from INDEX
4. Select exactly **ONE** skill to run next
5. Read only that skill’s **TL;DR**
6. Execute the skill
7. Stop and report results + next recommended skill (do not continue automatically)

## 2) Routing rules
- `.agent/INDEX.md` is the **single source of truth** for:
  - current phase definitions
  - which skills are allowed in each phase
  - the “default” next skill selection
- Do not use any other routing sheets, legacy routers, or “memory/rules” files as runtime routers.

## 3) Execution discipline
When executing a skill:
- Apply the skill’s **Change Budget** strictly.
- Output must be **actionable artifacts**:
  - “patch-style” edits (exact file + exact change) OR
  - a single new file/module (if budget allows) OR
  - a short checklist of commands + expected outputs
- Avoid speculative rewrites. Prefer minimal, reversible changes.
- If a task expands scope: stop and route back to INDEX for the next skill.

## 4) Exploration vs Production
- Exploration/visual probing happens in:
  - **Skill 18.5 — Section Sandbox** (HTML structure exploration; cheap iteration)
  - **Skill 22 — Design Critic** (evaluate against intent; propose deltas within budget)
- Production implementation happens in:
  - **Skill 19 — Section Prototyper** (real Next.js sections, module-first)
  - **Skill 21 — Micro Editor** (single-file surgical edits)

Rule:
- If requirements are fuzzy → go to **18.5** first.
- If requirements are clear → go to **19/21**.

## 5) Token / cost control
Default behavior:
- Read the minimum required files.
- Prefer TL;DR summaries, not full skill bodies.
- Never “double-check by reading everything”.
- If additional context is required, request **exactly one** additional file, justify why, then stop.

## 6) Project Setup Workflow alignment (Next.js bootstrap)
When the project is new or environment is missing baseline setup, follow this workflow BEFORE building sections:

### Step A — Initialize Next.js (TypeScript, Tailwind, ESLint, App Router)
```bash
npx create-next-app@latest . --typescript --tailwind --eslint
```         
Step B — Install Zaitex Core Stack (mandatory)
npm install framer-motion lenis lucide-react class-variance-authority clsx tailwind-merge three @react-three/fiber @react-three/drei gsap @gsap/react
npm install -D @types/three
Step C — Configure Design System (Active DNA)

Propagate tokens into:

app/globals.css

tailwind.config.ts

Use .agent/design/active-dna.md as the single source of truth for tokens.

Apply changes using the allowed skill for the current phase (often: Style Propagator / Layout Architect / Micro Editor).

Step D — Verify strict build
npm run build

Fix strict-mode issues without broad refactors (null canvas refs, types, unused vars, etc.).

Validate via the phase-allowed skills only.

7) Output contract (every response)

Every response must include:

Phase (from INDEX)

Selected Skill (one only)

What you read (file list; keep short)

Changes made / proposed (within budget)

Stop (explicit stop)

Next recommended skill (from INDEX), and why

8) Safety / guardrails for drift

Do not change branding, typography system, or motion language unless:

the selected skill explicitly instructs it, AND

the Change Budget allows it.

Do not introduce new dependencies unless:

required by the Setup Workflow OR

explicitly allowed by the selected skill and phase.

9) If conflicts are detected

If START_HERE, INDEX, or a skill conflicts:

Treat START_HERE + INDEX as higher priority than any single skill body.

Stop and report the conflict with the exact lines/sections involved.

Recommend the smallest patch to restore single-source-of-truth behavior.