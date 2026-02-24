---
name: immersive-architect
description: >
  Comprehensive framework for building reactive, physically correct 3D scenes with organic effects
  and smart defaults — now module-first to prevent monolithic files and token burn.
---

## TL;DR
**Skill:** 13 — Immersive Architect  
**Phase:** Concept / Production (3D projects only)  
**Purpose:** Build 3D scenes or immersive modules  
**Change Budget:** LARGE (isolated to scene modules)  
**Stop:** After scene is stable and performant  
**Redirects:** If messy → rebuild module cleanly

# IMMERSIVE 3D ARCHITECT — V3.1 (MODULE-FIRST)

## ROLE
You build physically correct, interactive 3D scenes that feel alive. You translate natural language
effects into calibrated technical implementations with scene-aware defaults — while keeping the
codebase modular, patchable, and cheap to iterate.

---

# PART 0 — NON-NEGOTIABLES (TOKEN & SCOPE CONTROL)

## ✅ Module-First Rule (Hard)
Immersive work MUST be split into small files. Never ship a single giant Scene file.

### Required module layout
- `components/immersive/[SceneName]/Scene.tsx`        → Canvas + composition only
- `components/immersive/[SceneName]/Camera.tsx`       → camera rig + calibration hooks
- `components/immersive/[SceneName]/Lights.tsx`       → key/fill/rim, env, shadows
- `components/immersive/[SceneName]/Models.tsx`       → GLTF loads + mesh grouping
- `components/immersive/[SceneName]/Materials.ts`     → materials factory/helpers
- `components/immersive/[SceneName]/Effects.tsx`      → postprocessing + atmos
- `components/immersive/[SceneName]/Interactions.tsx` → mouse/raycast/forces
- `components/immersive/[SceneName]/constants.ts`     → preset values + brand hooks
- `components/immersive/[SceneName]/types.ts`         → config types (optional)
- `components/immersive/index.ts`                     → exports

**Never** create immersive files in root. Keep everything under `components/immersive/`.

## ✅ Line Budget (Hard)
- No immersive module may exceed **300 lines**.
- Target: **80–200 lines** per module.
If a module is getting large, split again (e.g., `Effects/Fog.tsx`, `Effects/Bloom.tsx`).

## ✅ One-Module Patch Policy (Hard)
During iteration, edits must target **one module per round** unless user explicitly requests a refactor.
State which file you will touch before editing.

Example:
> "Patch target: `Effects.tsx` only. No other changes."

## ✅ One Feature per Iteration (Hard)
In immersive mode, do not add 3 features at once. Add exactly one:
- add bloom OR add fog OR add reveal mask OR add wobble
Then show + iterate.

---

# PART 1 — OPERATING MODES

## 🎯 Mode Selection (First Decision)

### MODE: AUTO (Default)
"Just make it work based on my description"
- Picks optimal values from calibration
- Minimal Leva controls (only major adjustments)
- Goal: 80% done, user tweaks remaining 20% if needed
- Use when: Rapid prototyping, trusting the system

### MODE: TWEAK
"I want full control over everything"
- All parameters exposed via Leva
- Calibrated ranges based on scene measurements
- Organized into collapsible folders
- Use when: Fine-tuning, client revisions, perfecting feel

To switch: user says "switch to TWEAK" / "give me full controls"

---

## 🎨 Color State (Second Decision)

### STATE: SANDBOX
"I'm experimenting"
- Any colors allowed
- No CSS/DNA constraints
- Full color pickers in Leva

### STATE: BRAND-LOCK
"Use only approved brand colors"
- Colors pulled from `.agent/design/active-dna.md` or `globals.css`
- Color pickers disabled, only presets
- Enforces visual consistency

To switch: user says "lock to brand" / "sandbox mode"

---

# PART 2 — SCENE BUILDING

## Mental Mode Lock

### 🔒 MODE: PLACE (Default)
A real, physical space with correct scale and lighting.
- 1 unit = 1 meter
- Colors from design system
- Realistic materials

### ⚠️ MODE: VIBE (Opt-in)
Abstract, artistic visuals. Only when explicitly requested.

### Forbidden in PLACE Mode
- motion_blur
- world_curvature
- distortion_shaders
- heavy_bloom
- abstract_depth

---

## Scene Scaffold Workflow (Module-first)

### STEP 0 — CALIBRATE SCENE (Mandatory)
Calibration belongs in `Camera.tsx` (or a shared hook). All ranges derive from it.

```tsx
// Camera.tsx
export function useSceneCalibration(sceneRef, camera) {
  return useMemo(() => {
    const box = new Box3().setFromObject(sceneRef.current);
    const size = box.getSize(new Vector3());
    const maxDim = Math.max(size.x, size.y, size.z);
    return { sceneSize: maxDim, cameraDistance: camera.position.length() };
  }, []);
}
STEP 1 — SCAFFOLD BOUNDARIES

SCN_FLOOR matches --color-background

SCN_WALL matches --color-muted

SCN_LIGHT studio setup (key, fill, rim)
Implementation lives in Lights.tsx + Scene.tsx composition.

STEP 2 — DEFINE PHYSICS (Plain Language)

Describe what exists:

"A wall (dark zinc). Objects (light) fixed to it. 1.8m tall."

This maps to:

Models.tsx (objects)

Materials.ts (surface)

Lights.tsx (lighting)

STEP 3 — PROXIES & LAYOUT

Validate scale with simple primitives FIRST:

Proxies go in Models.tsx (temporary) behind a DEBUG_PROXIES flag.

STEP 4 — ASSET INJECTION

GLB/GLTF only

Smart merge: combine meshes that are one logical object
All loads & grouping in Models.tsx.

STEP 5 — ATMOSPHERE

PLACE: atmosphere for depth only, not blur

Fog color derived from background
Lives in Effects.tsx (or Effects/Fog.tsx).

STEP 6 — ADD EFFECTS

Use Part 3 vocabulary. Effects implemented inside Effects.tsx + Interactions.tsx.
Never embed effect logic directly in Scene.tsx.

STEP 7 — EXPOSE CONTROLS

AUTO: minimal controls

TWEAK: full Leva with calibrated ranges
Leva wiring belongs in Scene.tsx (registry host) but each module registers its folder.

STEP 8 — BAKE & CATALOG

Lock values, document in component-library.md.
Production strips Leva.

PART 3 — EFFECT VOCABULARY (UNCHANGED)

When user describes an effect in natural language, match to these recipes:

Transform Effects
Natural Language	Effect ID	Implementation
"clay pouring"	POUR	Top-down UV mask with noise edge
"emerging from surface"	EMERGE	Depth-based alpha + Y displacement
"melting"	MELT	Vertex droop + noise distortion
"growing"	GROW	Scale 0→1 with eased timing
"dissolving"	DISSOLVE	Noise threshold alpha
Reveal Effects (Mouse-Triggered)
Natural Language	Effect ID	Implementation
"spotlight in darkness"	REVEAL_SPOTLIGHT	Radial mask at mouse UV
"fog clears where mouse is"	REVEAL_FOG	Fog density = distance from mouse
"washed off"	REVEAL_WASH	Directional dissolve following movement
"scratched away"	REVEAL_SCRATCH	Persistent accumulating mask
"burned through"	REVEAL_BURN	Noise-edged expanding hole
Motion Effects (Mouse-Triggered)
Natural Language	Effect ID	Implementation
"tilt away from mouse"	MOTION_TILT	lookAt inverse + damping
"follows my cursor"	MOTION_FOLLOW	Lerp toward mouse ray
"pushed away"	MOTION_REPEL	Distance-based force
"attracted to mouse"	MOTION_ATTRACT	Inverse distance force
"wobbles on hover"	MOTION_WOBBLE	Sine wave on hover state
Surface Effects
Natural Language	Effect ID	Implementation
"ripples where I touch"	SURFACE_RIPPLE	Radial wave from mouse UV
"indent under mouse"	SURFACE_INDENT	Vertex toward mouse
"clay deforms"	SURFACE_DEFORM	Noise-based vertex push
"water disturbed"	SURFACE_WATER	Height map + wave propagation
Atmosphere Effects
Natural Language	Effect ID	Implementation
"darkness follows me"	ATMOS_SHADOW	Light inverse to mouse
"warmth around cursor"	ATMOS_GLOW	Color temp shift near mouse
"particles scatter"	ATMOS_SCATTER	Particle velocity from mouse
PART 4 — SCENE CALIBRATION (UNCHANGED)

All values are relative to scene size. Never use arbitrary numbers.

(Keep your formulas + presets here.)

PART 5 — TUNING & BAKING (MODULE-AWARE)
Leva Registry Pattern (Scene host + module registration)

Scene.tsx hosts registry and export button.

Each module registers its own folder values via onRegister(id, values).

Rule: each module controls only its own folder (Lights/Effects/etc).

(Keep your existing registry + bake flow.)

PART 6 — FILE HYGIENE (UPDATED)

Components: components/immersive/[SceneName]/... (module layout above)

Assets: public/assets/[category]/

Never: create or edit immersive code in app/ pages directly (import modules instead)

Always: ESLint clean before "done"

Always: keep each file under line budget

PART 7 — COMMUNICATION FORMAT (UPDATED)

When building, always state:

Mode: AUTO / TWEAK

Color State: SANDBOX / BRAND-LOCK

Scene Mode: PLACE / VIBE

Current Step: (0–8)

Patch Target: (single module path)

Effects Applied: (Effect IDs)

Calibration: sceneSize = X units

PERFORMANCE GUARDRAILS (UNCHANGED)

(Keep your WebGL2, tri budget, texture limits, PerformanceMonitor, static fallback.)

PART 8 — CRYSTALLIZE CHECKPOINT (UNCHANGED)

(Keep your reset-vs-patch framework.)