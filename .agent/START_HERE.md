---
name: START_HERE
description: Hard operating contract for all AI agents using Zaitex Engine. Must be read before any task execution. This file overrides legacy pipeline behavior.
---

# Zaitex Engine — START HERE (Operating Contract)

This document defines **how you are allowed to think and operate** inside the Zaitex Engine.

You are not free-roaming.
You are a controlled system operating inside defined phases.

Failure to follow this contract causes:
- Token waste
- Design drift
- Random global changes
- Broken architecture

---

# 1) CORE RULE

Before doing anything:

1. Read this file.
2. Read `.agent/core/INDEX.md`.
3. Identify MODE + PHASE.
4. Activate ONE allowed skill.
5. Respect change budget.
6. Stop.

You do NOT:
- Read the entire `.agent/` folder.
- Reinterpret the full pipeline.
- Combine multiple skills unless explicitly allowed.
- Improve unrelated parts of the project.

## TL;DR Activation Protocol

When activating a skill:

1) Read that skill’s TL;DR first.
2) If TL;DR is sufficient, execute without reading further.
3) If more clarity is needed, read only the relevant sections of that same skill.
4) Do not read multiple skills to “be safe”. Routing is handled by INDEX.

---

# 2) THINKING CONSTRAINTS

You operate under **Phase-Gated Execution**.

This means:

- You may only use skills allowed by the current PHASE.
- You may only modify files within declared change budget.
- You may not redesign during production.
- You may not "optimize" unrelated sections.
- You may not escalate scope without permission.

---

# 3) GLOBAL READ PROHIBITION

In production phases:

You are NOT allowed to:
- Read all skills
- Re-evaluate architecture globally
- Audit the entire project
- Refactor broadly

Unless the user explicitly writes:

UNLOCK: allow global review

Without that keyword:
Stay local.
Stay scoped.
Stay within one skill.

---

# 4) DESIGN UNCERTAINTY PROTOCOL

If at any point you detect:

- Conflicting stylistic direction
- Identity-level changes
- “Feels off” feedback without specificity
- Need to change radius/surface/typography system globally
- Temptation to redesign multiple sections

You must STOP and redirect to:

→ `18.5-section-sandbox`

Production is not a place for experimentation.

---

# 5) BUDGET ENFORCEMENT

Before making edits, declare change budget:

- Micro: 1 file, ≤ 80 lines
- Small: ≤ 3 files, ≤ 200 lines
- Medium: ≤ 8 files, ≤ 500 lines
- Large: Concept phases only (18.5 / 19 / Aura migration)

If task exceeds declared budget:
- Stop
- Propose smaller step
- Or redirect to proper phase

Never silently exceed budget.

---

# 6) MODE DISCIPLINE

MODE is decided in PHASE 0 by `00-brief-architect`.

Possible modes:

- AURA
- LITE
- ENGINE

You may NOT switch modes mid-project
unless the user explicitly requests a strategic shift.

---

# 7) AURA RULES

If MODE = AURA:

- Aura template is considered pre-concepted.
- Do NOT run 18 / 18.5 / 19 by default.
- Do NOT redesign structure unless client demands identity shift.
- Focus on alignment, content, polish, performance.

Aura is execution-first.

---

# 8) PRODUCTION RULE

Production phases are for:

- Building
- Aligning
- Optimizing
- Polishing

Production is NOT for:
- Exploring new layout systems
- Changing visual language
- Inventing new identity

If identity changes → redirect to 18.5.

---

# 9) MICRO EDITOR PRINCIPLE

When task is small and localized:

- Prefer Micro changes.
- Touch the fewest files possible.
- Preserve structure.
- Avoid rewriting entire sections.

Surgical precision over cleverness.

---

# 10) PERFORMANCE DISCIPLINE

You do not:

- Add heavy dependencies casually.
- Introduce animated filters or expensive effects.
- Inflate bundle size.
- Increase complexity without justification.

Premium ≠ heavy.

---

# 11) WHEN UNSURE

If you do not know which skill to use:

1. Re-read INDEX.
2. Identify problem type.
3. Select the closest single skill.
4. If ambiguity remains → ask a specific clarification question.

Do NOT guess.
Do NOT improvise a new workflow.

---

# 12) FINAL PRINCIPLE

The Zaitex Engine is built to:

- Separate exploration from execution.
- Prevent agent drift.
- Reduce token waste.
- Maintain architectural clarity.

Your job is not to be creative at random.

Your job is to operate within the system.

---

# EXECUTION ENTRY POINT

After reading this file:

→ Open `.agent/core/INDEX.md`
→ Determine MODE + PHASE
→ Activate exactly one allowed skill
→ Declare change budget
→ Execute
→ Stop