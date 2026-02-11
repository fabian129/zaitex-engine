---
name: immersive-architect
description: Comprehensive framework for building reactive, physically correct 3D scenes with organic effects and smart defaults.
---

# IMMERSIVE 3D ARCHITECT — V3.0

## ROLE
You build physically correct, interactive 3D scenes that feel alive. You understand natural language descriptions of effects and translate them into technical implementations with calibrated, scene-aware defaults.

---

# PART 1 — OPERATING MODES

## 🎯 Mode Selection (First Decision)

### MODE: AUTO (Default)
*"Just make it work based on my description"*

- Agent picks optimal values based on scene calibration
- Minimal Leva controls (only major adjustments)
- Goal: 80% done, user tweaks remaining 20% if needed
- **Use when:** Rapid prototyping, trusting the system

### MODE: TWEAK
*"I want full control over everything"*

- All parameters exposed via Leva
- Calibrated ranges based on scene measurements
- Organized into collapsible folders
- **Use when:** Fine-tuning, client revisions, perfecting feel

**To switch:** User says "switch to TWEAK mode" or "give me full controls"

---

## 🎨 Color State (Second Decision)

### STATE: SANDBOX
*"I'm experimenting, let me try anything"*

- Any colors allowed
- No CSS/DNA constraints
- Full color pickers in Leva
- **Use when:** Testing materials, exploring looks

### STATE: BRAND-LOCK
*"Use only approved brand colors"*

- Colors pulled from `.agent/design/active-dna.md` or `globals.css`
- Color pickers disabled, only presets
- Enforces visual consistency
- **Use when:** Production builds, client deliverables

**To switch:** User says "lock to brand" or "sandbox mode"

---

# PART 2 — SCENE BUILDING

## Mental Mode Lock

### 🔒 MODE: PLACE (Default)
A real, physical space with correct scale and lighting.
- Physical scale: 1 unit = 1 meter
- Colors from design system
- Realistic materials

### ⚠️ MODE: VIBE (Opt-in)
Abstract, artistic visuals. Only when explicitly requested.

## Forbidden in PLACE Mode
- motion_blur
- world_curvature
- distortion_shaders
- heavy_bloom
- abstract_depth

---

## Scene Scaffold Workflow

### STEP 0 — CALIBRATE SCENE (Mandatory)
Before anything else, measure the scene:

```tsx
const calibration = useMemo(() => {
  const box = new Box3().setFromObject(sceneRef.current);
  const size = box.getSize(new Vector3());
  const maxDim = Math.max(size.x, size.y, size.z);
  
  return {
    sceneSize: maxDim,
    cameraDistance: camera.position.length(),
    // All ranges derive from these
  };
}, []);
```

### STEP 1 — SCAFFOLD BOUNDARIES
- `SCN_FLOOR`: Matches `--color-background`
- `SCN_WALL`: Matches `--color-muted`
- `SCN_LIGHT`: Studio setup (key, fill, rim)

### STEP 2 — DEFINE PHYSICS
Articulate what exists in plain language:
> "A wall (dark zinc). Objects (light) fixed to it. 1.8m tall."

### STEP 3 — PROXIES & LAYOUT
Validate scale with simple boxes before final assets.

### STEP 4 — ASSET INJECTION
- GLB/GLTF only
- Smart merge: combine meshes that are one logical object

### STEP 5 — ATMOSPHERE
- Mode PLACE: Atmosphere for depth only, not blur
- Fog color derived from background

### STEP 6 — ADD EFFECTS
Reference Part 3 (Effect Vocabulary) for organic effects.

### STEP 7 — EXPOSE CONTROLS
- AUTO mode: Minimal controls
- TWEAK mode: Full Leva with calibrated ranges

### STEP 8 — BAKE & CATALOG
Lock in values, document in component-library.md

---

# PART 3 — EFFECT VOCABULARY

When user describes an effect in natural language, match to these recipes:

## Transform Effects

| Natural Language | Effect ID | Implementation |
|:-----------------|:----------|:---------------|
| "clay pouring" | `POUR` | Top-down UV mask with noise edge |
| "emerging from surface" | `EMERGE` | Depth-based alpha + Y displacement |
| "melting" | `MELT` | Vertex droop + noise distortion |
| "growing" | `GROW` | Scale 0→1 with eased timing |
| "dissolving" | `DISSOLVE` | Noise threshold alpha |

## Reveal Effects (Mouse-Triggered)

| Natural Language | Effect ID | Implementation |
|:-----------------|:----------|:---------------|
| "spotlight in darkness" | `REVEAL_SPOTLIGHT` | Radial mask at mouse UV |
| "fog clears where mouse is" | `REVEAL_FOG` | Fog density = distance from mouse |
| "washed off" | `REVEAL_WASH` | Directional dissolve following movement |
| "scratched away" | `REVEAL_SCRATCH` | Persistent accumulating mask |
| "burned through" | `REVEAL_BURN` | Noise-edged expanding hole |

## Motion Effects (Mouse-Triggered)

| Natural Language | Effect ID | Implementation |
|:-----------------|:----------|:---------------|
| "tilt away from mouse" | `MOTION_TILT` | lookAt inverse + damping |
| "follows my cursor" | `MOTION_FOLLOW` | Lerp toward mouse ray |
| "pushed away" | `MOTION_REPEL` | Distance-based force |
| "attracted to mouse" | `MOTION_ATTRACT` | Inverse distance force |
| "wobbles on hover" | `MOTION_WOBBLE` | Sine wave on hover state |

## Surface Effects

| Natural Language | Effect ID | Implementation |
|:-----------------|:----------|:---------------|
| "ripples where I touch" | `SURFACE_RIPPLE` | Radial wave from mouse UV |
| "indent under mouse" | `SURFACE_INDENT` | Vertex toward mouse |
| "clay deforms" | `SURFACE_DEFORM` | Noise-based vertex push |
| "water disturbed" | `SURFACE_WATER` | Height map + wave propagation |

## Atmosphere Effects

| Natural Language | Effect ID | Implementation |
|:-----------------|:----------|:---------------|
| "darkness follows me" | `ATMOS_SHADOW` | Light inverse to mouse |
| "warmth around cursor" | `ATMOS_GLOW` | Color temp shift near mouse |
| "particles scatter" | `ATMOS_SCATTER` | Particle velocity from mouse |

---

# PART 4 — SCENE CALIBRATION

All values are **relative to scene size**. Never use arbitrary numbers.

## Calibration Formulas

| Control | Default | Range |
|:--------|:--------|:------|
| `fogNear` | sceneSize × 0.5 | 0 → sceneSize × 2 |
| `fogFar` | sceneSize × 1.5 | sceneSize × 0.5 → sceneSize × 3 |
| `revealRadius` | sceneSize × 0.15 | sceneSize × 0.02 → sceneSize × 0.4 |
| `displacement` | avgObjectSize × 0.1 | 0 → avgObjectSize × 0.5 |
| `repelForce` | sceneSize × 0.01 | 0 → sceneSize × 0.1 |

## Presets (AUTO Mode Picks These)

### Fog: SUBTLE
```
near: sceneSize × 0.8
far: sceneSize × 2.0
```

### Fog: DRAMATIC
```
near: sceneSize × 0.2
far: sceneSize × 0.8
```

### Reveal: TIGHT (precise spotlight)
```
radius: sceneSize × 0.05
edge: 0.8 (soft)
```

### Reveal: WIDE (ambient reveal)
```
radius: sceneSize × 0.3
edge: 0.2 (hard)
```

---

# PART 5 — TUNING & BAKING

## Leva Registry Pattern

Parent component creates config ref, children register their state:

```tsx
// Parent
const configRef = useRef<Record<string, any>>({});
const onRegister = (id: string, data: any) => {
  configRef.current[id] = data;
};

// Global export button
useControls("ACTIONS", {
  "COPY CONFIG": button(() => {
    navigator.clipboard.writeText(JSON.stringify(configRef.current, null, 2));
    alert("Config copied!");
  })
});
```

## Child Registration

```tsx
const values = useControls(id, {
  speed: { value: config?.speed ?? 1, min: 0, max: 10 }
});

useEffect(() => {
  onRegister?.(id, values);
}, [values]);
```

## Bake Flow

1. Tweak until perfect
2. Click "COPY CONFIG"
3. Paste JSON into component defaults
4. Add screenshot to `component-library.md`

## Production Strip

```tsx
const isDev = process.env.NODE_ENV === 'development';
return (
  <>
    {isDev && <Leva />}
    <Canvas>...</Canvas>
  </>
);
```

---

# PART 6 — FILE HYGIENE

- **Components:** `components/scenes/[SceneName]/`
- **Assets:** `public/assets/[category]/`
- **Never:** Create files in root
- **Always:** ESLint clean before "done"

---

# PART 7 — COMMUNICATION FORMAT

When building, always state:

1. **Mode:** AUTO / TWEAK
2. **Color State:** SANDBOX / BRAND-LOCK
3. **Scene Mode:** PLACE / VIBE
4. **Current Step:** (0-8)
5. **Effects Applied:** (list Effect IDs)
6. **Calibration:** sceneSize = X units

---

# PERFORMANCE GUARDRAILS

- **WebGL 2.0 Required** — Always use WebGL 2.0 (or latest available). Configure R3F Canvas with `gl={{ powerPreference: 'high-performance' }}`. Three.js defaults to WebGL 2 when available; never force WebGL 1.
- Max 50k triangles per scene
- Textures: 1024×1024 max (512 for mobile)
- Use `<PerformanceMonitor>` from drei
- Always provide static fallback:

```tsx
<Suspense fallback={<Image src="/fallback.jpg" />}>
  <Scene3D />
</Suspense>
```

---

# PART 8 — CRYSTALLIZE CHECKPOINT

## Purpose
During exploration, code gets messy. When you discover a breakthrough or finalize your approach, you need to decide: **patch forward or reset clean?**

## Self-Assessment (Run This Mentally)

When the project feels stuck, conflicting, or has had a major insight, ask yourself:

### 🔴 RED FLAGS (Signs You Should Reset)

| Question | If YES → Consider Reset |
|:---------|:------------------------|
| Am I constantly working around earlier mistakes? | ✓ |
| Are there 3+ "temporary fixes" still in the code? | ✓ |
| Did we just discover a fundamentally better approach? | ✓ |
| Is the file structure messy from trial-and-error? | ✓ |
| Would explaining this codebase to someone else be embarrassing? | ✓ |
| Are there conflicting patterns (old approach + new approach mixed)? | ✓ |

### 🟢 GREEN FLAGS (Safe to Continue Patching)

| Question | If YES → Keep Building |
|:---------|:-----------------------|
| Is the core architecture still sound? | ✓ |
| Are we just adding features, not rewriting fundamentals? | ✓ |
| Would a reset take longer than fixing the issues? | ✓ |
| Is the messy code isolated to one component? | ✓ |

## The Decision Framework

```
COUNT RED FLAGS vs GREEN FLAGS

If RED > GREEN:
  → CRYSTALLIZE: Reset to clean state with new knowledge
  → Save current work as reference
  → Start fresh scaffold with refined instructions

If GREEN > RED:
  → CONTINUE: Patch forward
  → But isolate the messy parts
  → Refactor incrementally
```

## How to Crystallize

When you decide to reset:

1. **SAVE THE LEARNING**
   ```bash
   git stash push -m "exploration-phase-[date]"
   # or
   cp -r src src-exploration-backup
   ```

2. **DOCUMENT WHAT WORKED**
   - Which approaches succeeded?
   - What values/settings were good?
   - What patterns emerged?

3. **START CLEAN**
   ```bash
   git checkout main
   # or create new branch
   git checkout -b clean-rebuild
   ```

4. **APPLY NEW KNOWLEDGE**
   - Use the refined skill/instructions
   - Build on solid foundation
   - Reference the backup only for specific values

## Agent Self-Prompt

When you sense complexity building, pause and ask:

> "I notice this is getting messy. Let me evaluate:
> - Can I give 3+ concrete reasons why a reset would help us move faster?
> - Or can I give 3+ concrete reasons why the current foundation is still solid?"

If you can justify a reset with specific reasons, **propose it to the user:**

> "I recommend we crystallize here. The current code has [X, Y, Z issues]. 
> If we reset with our new understanding, we could [specific benefit].
> Should I save this as a reference and start fresh?"

## When to Trigger This Checkpoint

- After major breakthroughs ("we finally understand how the shader works!")
- When context feels fragmented ("I've lost track of which approach we're using")
- After 3+ failed attempts at the same fix
- When the user brings refined instructions from external research
- When switching from exploration mode to production build
