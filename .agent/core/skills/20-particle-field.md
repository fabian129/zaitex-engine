---
name: particle-field
description: >
  GPU-powered particle field system for interactive text, borders, logos, and UI elements.
  Particles live on any source shape (text, SVG, image edge) and react to cursor gravity.
  Built on Regl (WebGL) for near-zero CPU cost. Leva controls optional for fine-tuning
  without agent involvement. One component, infinite visual variations.
---

## TL;DR
**Skill:** 20 — Particle Field  
**Phase:** Production (specialized)  
**Purpose:** GPU particle effects (isolated modules only)  
**Change Budget:** MEDIUM (isolated to scene/text modules)  
**Stop:** After performance verified  
**Redirects:** If performance risk → 08

# Particle Field — Skill 20

## What This Is

A reusable WebGL particle system where particles are placed on any **source texture**
(rendered text, SVG, border, logo) and respond to cursor gravity — fleeing on approach
and elastically returning home. The same GLSL shader engine powers every variant.

Reference implementation: basement.studio's Vercel Ship hero (2024)
Key insight: It's NOT a Three.js effect. It's 2D WebGL with custom GLSL — lighter and
faster than any 3D approach.

---

## Position in Pipeline

```
Section Prototyper (19)  → decides WHERE particle effects live
                         ↓
★ PARTICLE FIELD (20)   ← YOU ARE HERE
  → Build ParticleField.tsx (core engine)
  → Choose preset (TEXT, BORDER, LOGO, DIVIDER, EDGE)
  → Wire to hero / section / button
  → Optional: Leva controls for user fine-tuning
```

---

## Core Architecture

### The Control Texture (`baseFbo`)

Every particle field is driven by a single **RGB texture** that encodes behavior rules.
Paint this texture in code (canvas 2D API) or in Figma and export as PNG.

| Channel | Encodes | Example |
|:--------|:--------|:--------|
| **Red** | Source shape — where particles appear, white = lit | The letter forms of "ZAITEX" |
| **Green** | Movement permission — 1.0 = moves freely, 0.0 = locked | Button center = 0, letter edges = 1 |
| **Blue** | Bridge zones — allows effect to flow between separate elements | Gap between Z and A gets a blue bridge |

### The Flow Shader (Cursor Gravity)

A second shader samples mouse position each frame and stores:
- **Red + Green**: Direction vector from pixel → cursor, with fade/falloff
- **Blue**: Magnitude — how far particles should travel

Momentum is built in: **moving particles change direction slower than static ones.**
This makes the physics feel organic, not mechanical.

### Particle Lifecycle

```
IDLE:    particle sits at source position → renders as shape texture
FLEEING: cursor enters repel radius → velocity accumulates away from cursor
DRIFTING: cursor moves away → particle overshoots, oscillates back
SETTLED: return spring pulls particle home → snaps back to source position
```

---

## Dependencies

```bash
npm install regl
npm install @types/regl --save-dev
# Leva (optional, only for TWEAK mode)
npm install leva
```

`regl` is ~30KB minified. Do NOT use Three.js for this — it's overkill and 10× heavier.

---

## Operating Modes

### MODE: BAKED (Production Default)
All parameter values hardcoded from approved config. No Leva. Zero overhead.
Use when the effect is finalized and approved.

### MODE: TWEAK (Development / Iteration)
Leva panel exposed with calibrated sliders. User can adjust in browser without
touching code or burning agent tokens. Once happy, click "COPY CONFIG" and paste
into component defaults.

```tsx
// Activate TWEAK mode
<ParticleField text="ZAITEX" tweakMode={process.env.NODE_ENV === 'development'} />
```

---

## The Component API

```tsx
<ParticleField
  // Source
  text="ZAITEX"              // Text string (uses Bebas Neue by default)
  svgPath=""                 // OR: SVG path string for logos/icons
  preset="TEXT"              // TEXT | BORDER | LOGO | DIVIDER | EDGE

  // Visual
  particleColor="#c6f91f"    // Default: brand accent
  particleSize={1.5}         // px — 0.5 (dust) → 4 (chunks)
  density={2}                // Particles per pixel — 1 (sparse) → 4 (dense)

  // Physics
  repelForce={0.8}           // 0 (gentle) → 2 (explosive)
  repelRadius={80}           // px — cursor influence range
  returnSpeed={0.05}         // 0.01 (syrupy) → 0.3 (elastic snap)
  momentum={0.92}            // 0.8 (snappy) → 0.98 (floaty)

  // Fallback
  fallbackSvg={<ZaitexSvg />} // Shown while WebGL compiles

  // Leva controls
  tweakMode={false}          // Set true in dev to expose sliders
/>
```

---

## Presets

Each preset is a pre-tuned config object. Pass `preset="TEXT"` and the component
loads sensible defaults. Override any individual property.

### TEXT
Large headline text that shatters on cursor approach.
```ts
{ density: 2, particleSize: 1.5, repelForce: 0.9, returnSpeed: 0.05, momentum: 0.94 }
```

### BORDER
Thin particle outline of a card or button. Shimmers / scatters on hover.
```ts
{ density: 1, particleSize: 0.8, repelForce: 0.4, returnSpeed: 0.08, momentum: 0.88 }
```

### LOGO
Logo mark built from particles. Dense, high-fidelity, reassembles quickly.
```ts
{ density: 3, particleSize: 1.2, repelForce: 0.7, returnSpeed: 0.07, momentum: 0.92 }
```

### DIVIDER
Horizontal 1px line that splashes when cursor crosses it.
```ts
{ density: 1, particleSize: 0.6, repelForce: 1.2, returnSpeed: 0.04, momentum: 0.96 }
```

### EDGE
Image edge detection — particles trace the contours of a photograph.
```ts
{ density: 1.5, particleSize: 1.0, repelForce: 0.6, returnSpeed: 0.06, momentum: 0.91 }
```

---

## Building the Control Texture (Code Method)

No Figma needed. Generate `baseFbo` programmatically with Canvas 2D:

```ts
function createBaseFbo(text: string, font: string, canvas: HTMLCanvasElement) {
  const ctx = canvas.getContext('2d')!;
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  // RED channel: render text in white → becomes particle source shape
  ctx.fillStyle = 'white';
  ctx.font = `400 ${fontSize}px ${font}`;
  ctx.textAlign = 'center';
  ctx.textBaseline = 'middle';
  ctx.fillText(text, canvas.width / 2, canvas.height / 2);

  const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);

  // GREEN channel: copy red → full movement permission (can zero out specific zones)
  for (let i = 0; i < imageData.data.length; i += 4) {
    imageData.data[i + 1] = imageData.data[i]; // G = R
  }

  // BLUE channel: add bridges between letter gaps if needed
  // (advanced: flood-fill connected zones with blue)

  ctx.putImageData(imageData, 0, 0);
}
```

---

## Flow Shader (GLSL)

```glsl
// Fragment shader — stores direction + magnitude of cursor influence
precision mediump float;

uniform vec2 uMouse;      // Normalized mouse position [0..1]
uniform vec2 uResolution;
uniform sampler2D uPrev;  // Previous frame (enables momentum/fade)
uniform float uDelta;     // Time delta

void main() {
  vec2 uv = gl_FragCoord.xy / uResolution;
  vec2 pixelToMouse = uMouse - uv;
  float dist = length(pixelToMouse);

  // Fade influence with distance
  float influence = smoothstep(0.3, 0.0, dist);

  // Red + Green: direction toward cursor, faded by distance
  vec2 dir = normalize(pixelToMouse) * influence;

  // Blue: magnitude of displacement
  float magnitude = influence;

  // Read previous frame → momentum (particles already moving change direction slowly)
  vec4 prev = texture2D(uPrev, uv);
  vec3 current = vec3(dir * 0.5 + 0.5, magnitude);

  // Blend: mix current influence with previous state (momentum)
  gl_FragColor = vec4(mix(prev.rgb, current, 0.15), 1.0);
}
```

---

## SVG Fallback + Swap Pattern

Prevents blank screen during WebGL compilation:

```tsx
const [shaderReady, setShaderReady] = useState(false);

// Show SVG until WebGL canvas is compiled and first frame rendered
return (
  <div style={{ position: 'relative' }}>
    {/* SVG fallback — same font, same size, animates in */}
    <svg
      style={{ opacity: shaderReady ? 0 : 1, transition: 'opacity 0.3s' }}
    >
      <text fontFamily="Bebas Neue" fontSize={fontSize}>{text}</text>
    </svg>

    {/* WebGL canvas */}
    <canvas
      ref={canvasRef}
      style={{ opacity: shaderReady ? 1 : 0, position: 'absolute', top: 0, left: 0 }}
    />
  </div>
);
```

Apply antialiasing to the canvas text render so the swap is seamless even at zoom.

---

## Leva Controls (TWEAK Mode)

When `tweakMode={true}`, expose sliders so the user can tune live without agent:

```tsx
import { useControls, button } from 'leva';

const {
  repelForce,
  repelRadius,
  returnSpeed,
  momentum,
  particleSize,
  density,
} = useControls('Particle Field', {
  repelForce:  { value: 0.8, min: 0, max: 2, step: 0.05 },
  repelRadius: { value: 80,  min: 20, max: 200, step: 5 },
  returnSpeed: { value: 0.05, min: 0.01, max: 0.3, step: 0.005 },
  momentum:    { value: 0.92, min: 0.8, max: 0.99, step: 0.01 },
  particleSize: { value: 1.5, min: 0.5, max: 4, step: 0.1 },
  density:     { value: 2, min: 0.5, max: 4, step: 0.25 },
  'COPY CONFIG': button(() => {
    const config = { repelForce, repelRadius, returnSpeed, momentum, particleSize, density };
    navigator.clipboard.writeText(JSON.stringify(config, null, 2));
    alert('Config copied to clipboard! Paste into component defaults.');
  }),
});
```

**Workflow:**
1. Run in dev mode
2. Tune sliders in browser until the effect feels perfect
3. Click "COPY CONFIG"
4. Paste JSON into `<ParticleField defaultConfig={...} />`
5. Set `tweakMode={false}` for production

---

## Performance Guardrails

| Rule | Limit |
|:-----|:------|
| Max particle count | 150,000 (at density=2, covers 1920×80px strip) |
| Canvas size | Match element size, not viewport — never full-screen for borders |
| Mobile | Halve density, increase returnSpeed, disable on `prefers-reduced-motion` |
| Fallback | Always provide SVG. No exceptions. |
| WebGL context loss | Use `canvas.addEventListener('webglcontextlost')` to switch to SVG |

```tsx
// Always check reduced motion
const prefersReduced = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
if (prefersReduced) return <StaticText>{text}</StaticText>;
```

---

## File Structure

```
src/
  app/
    components/
      particle-field/
        ParticleField.tsx       ← Main component with API
        particleField.vert.glsl ← Vertex shader
        particleField.frag.glsl ← Fragment shader
        flowField.frag.glsl     ← Cursor gravity shader
        presets.ts              ← Preset configurations
        createBaseFbo.ts        ← Control texture generation
        useParticleField.ts     ← Regl setup hook
```

---

## Building Instructions for Agent

When a user asks to apply a particle field effect:

1. **Install regl** (and leva if tweakMode requested)
2. **Ask**: text / SVG / border mode? Which preset?
3. **Generate `baseFbo`** for the source shape
4. **Build `ParticleField.tsx`** with the regl canvas + flow shader
5. **Add SVG fallback** — always, no exceptions
6. **Wire into component** — replace static text/border with `<ParticleField />`
7. **Test**: verify particle count < 150k, check mobile behavior
8. **If tweakMode**: expose Leva, let user tune, then bake final config

Do NOT use Three.js for this effect. Regl only.

---

## Catalog of Approved Builds

Track every approved particle field here so it can be reused:

| Project | Preset | Text/Shape | Config snapshot |
|:--------|:-------|:-----------|:----------------|
| ZAITEX Hero | TEXT | "ZAITEX" | TBD after build |
