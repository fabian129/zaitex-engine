---
name: micro-editor
description: Surgical patch skill for single-file edits. Used in production to apply minimal, controlled changes without refactors, redesigns, or scope creep. Enforces change budgets and includes an escalation protocol when the codebase is too messy for safe patching.
---

# Micro Editor

## TL;DR
**Phase:** Production / QA / Polish (never concept)  
**Use for:** 1-file surgical patch, minimal diff, no refactor  
**Budget:** MICRO (default) = 1 file, ≤ 80 lines changed (hard cap)  
**Output:** explicit diff summary + line count + why this is minimal  
**Stop:** if fix needs >80 lines, >1 file, or reveals structural debt → ESCALATE (do not patch around hacks)

---

## Objective
Apply the smallest possible change to achieve the requested outcome **without** introducing architectural drift.

Micro Editor exists to prevent:
- “agent becomes smart”
- “fix triggers refactor”
- “fix adds hacks”
- “fix touches many files”
- “fix changes design identity”

---

## When to Run
Run Micro Editor when:
- The user requests a small, localized change
- A bug/fix is likely resolvable with a tight patch
- You must respect strict scope and cost constraints
- Production code is already mostly stable

Do NOT run Micro Editor when:
- The request is a design/identity change → redirect to 18.5
- The request is a new section/component build → redirect to 05 or 19
- The system is messy and the fix would become “patch around hacks” → escalate

---

## Preconditions (must be true)
Before editing, you must have:

1) **Target file path** (exact)  
2) **Exact change request** (“what should be different”)  
3) **Current phase** is not concept exploration (INDEX governs)  
4) **Change budget declared** (default MICRO)

If any precondition is missing:
- stop and request only the missing item(s)
- do not guess

---

## Allowed Scope
Micro Editor may:
- Edit **one file only**
- Make minimal local changes:
  - tweak logic
  - adjust markup
  - adjust classes/styles in-file
  - fix typing/import in-file (only if required for the change)
- Add at most **one** small helper function inside the same file (if essential)
- Remove dead code inside the same file (only if directly related)

---

## Forbidden Scope (hard rules)
Micro Editor must NOT:
- Refactor structures “for cleanliness”
- Change file architecture
- Rename components widely
- Split files
- Create new components or folders
- Change design identity (radius system, surface language, typography system)
- Introduce new dependencies
- Touch global config (tailwind config, tsconfig, next config) unless explicitly requested
- Perform multi-file “cleanup”
- Add “temporary hacks” to bypass deeper issues

If tempted → stop and escalate.

---

## The No-Rescue Rule (critical)
Micro Editor is **not allowed** to patch around structural debt.

If the code shows signs of “emergency scaffolding”, you must not add more.

### Red flags (any one triggers escalation)
- 3+ “temporary” fixes already exist in the local area
- multiple contradictory conditions / duplicated logic
- unclear ownership of state/effects (e.g. chained useEffects)
- repeated “TODO/fix later”
- patch would require “just add one more if”
- you cannot explain the code path confidently
- fix requires >1 file or >80 lines to be safe

---

## Escalation Protocol (what to do instead of hacking)
If red flags appear, stop and choose the correct redirect:

### If it’s a bug with unclear cause
→ `15-web-debugger` (diagnose first)

### If the component/module is structurally broken
→ rebuild the module via:
- `05-component-architect` (single component rebuild)
or
- `19-section-prototyper` (section-level rebuild gate)

### If the issue is actually style/identity mismatch
→ `18.5-section-sandbox` (design lab)

Micro Editor must never “force it to work”.

---

## Change Budget (hard enforcement)
Default: **MICRO**
- 1 file
- ≤ 80 lines changed (add/remove/modify combined)

Optional (only if user explicitly upgrades budget):
- **SMALL:** ≤ 3 files, ≤ 200 lines total  
(If SMALL is requested, Micro Editor is still allowed to touch **only one file**; use another skill for multi-file changes.)

If the fix cannot fit MICRO:
- do not stretch
- escalate

---

## Execution Steps (must follow)
1) Restate the requested change in one sentence.
2) Identify the smallest edit point(s) in the file.
3) Apply the minimum patch.
4) Verify no unrelated formatting/rewrites occurred.
5) Produce a strict change report.

---

## Required Output Format (must be included in response)
After editing, Micro Editor must output:

- **File edited:** `<path>`
- **Change budget:** MICRO / SMALL
- **Line impact:** `+X / -Y / ~Z` (approx is OK, but must be honest)
- **What changed:** 3–6 bullets
- **What NOT changed:** 2–4 bullets (to prove scope control)
- **Risk note:** 1 short line (any side effects?)
- **Stop:** confirm completion and do not continue to other tasks

---

## Stop Conditions
Micro Editor must stop immediately when:
- requested change is done
- budget is reached
- escalation trigger occurs
- requirements are ambiguous

No follow-on improvements.
No “while I’m here”.

---

## Routing Notes (INDEX alignment)
- If user says “feels off” / wants new vibe → not Micro Editor → go 18.5
- If user wants new section or big component → not Micro Editor → go 05/19
- If there are errors/bugs and cause unknown → 15 first, then Micro Editor patch

---

## Core Principle
Micro Editor is a scalpel.

It wins by being:
- small
- precise
- boring
- controlled

If the fix requires creativity or structural redesign, Micro Editor must refuse and redirect.