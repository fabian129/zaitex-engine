---
name: brand-moodboard
description: >
  Concepting skill. Generates a stunning, interactive HTML brand moodboard by synthesizing
  scattered visual references, Aura templates, typography preferences, and brand input into
  a unified visual and verbal direction. Triggers on: moodboard requests, brand identity work,
  visual direction, color palette creation, design system starting points — or when someone
  dumps a pile of references and says "help me find the direction." Also triggers when
  describing a company and asking how it should look, feel, or communicate. Works in two
  modes: solo (fast execution, trust the designer's taste) and client session (guide the
  client through decisions they can't articulate).
---

## TL;DR
**Skill:** 18 — Brand Moodboard  
**Phase:** Concept  
**Purpose:** Establish visual direction inspiration  
**Change Budget:** None (exploratory)  
**Stop:** After direction candidate selected  
**Redirects:** → 18.5

# Brand Moodboard Generator

Produces a single, self-contained HTML file that IS the moodboard — animated, interactive,
beautiful. Not a document about a brand. A visual experience of it.

This is an internal agency tool. It has two operating contexts:

### Solo Mode (you working alone)
You already have taste. You might dump 25 Aura templates, 10 component screenshots, typography
references, site URLs, and a mood like "mörkt, premium, men inte corporate-kallt." The system
should be a fast, opinionated execution partner that matches your level. No hand-holding, no
"what's your target audience?" — you know that already. Move fast. Trust your taste.

### Client Session Mode (you with a client)
You're in a meeting, maybe screen-sharing. The client can't articulate what they want. The system
becomes your co-pilot — it asks the smart questions you would ask, but in a way that makes the
client feel comfortable and guided. The moodboard becomes a live conversation tool: generate it,
they react, you iterate. The client never touches the system directly — you're driving.

Read the conversation. Figure out which mode you're in and adapt everything accordingly.

---

## Phase 1 — Read the Room & Gather Input

This skill accepts ANY combination of input. The more you feed it, the smarter the synthesis.

### What can be provided as input

- **Aura templates** — full HTML files, screenshots, or descriptions ("I like the hero from
  this one, the footer from that one")
- **Component references** — screenshots, URLs, or descriptions of components you like from
  any site
- **Typography** — font names, screenshots of type you like, or vague descriptions ("something
  editorial", "tech but warm")
- **Reference sites/URLs** — sites you admire for tone, layout, motion, anything
- **Existing brand assets** — a logo, existing colors, a business card, brand guidelines
- **Mood/feeling** — adjectives, vibes, comparisons ("Apple meets a Swedish craft brewery")
- **Business context** — what the company does, who the customer is, what the site should achieve
- **Text input** — just a name and a feeling, that's enough too

### The intake decision tree

**Heavy reference input (5+ references, templates, assets):**
→ Go to **Reference Synthesis Mode** (below)

**Light input (brand name + description + maybe a mood):**
→ Go to **Quick Start Mode** (below)

**If it's ambiguous** — check which mode you're in:
- Solo mode → assume you have enough, move fast
- Client session → ask ONE smart question to orient

---

### Reference Synthesis Mode

When you receive a pile of scattered references, don't just pick one and run with it.
Synthesize. Find the throughline.

**Step 1 — Map patterns across all inputs**

For every reference, silently extract:
- Layout patterns (grid? asymmetric? horizontal scroll? bento?)
- Color temperature (warm/cool/neutral) and palette logic (monochrome? split? accent-heavy?)
- Typography energy (serif = editorial, grotesk = modern, mono = technical, mixed = bold)
- Motion character (smooth and slow? sharp and snappy? playful? minimal?)
- Spacing rhythm (generous and breathable? tight and dense?)
- Overall mood (premium? accessible? bold? quiet?)

Don't describe each reference individually. Look across ALL of them for clusters.

**Step 2 — Find the throughline**

What connects the scattered inputs? Identify:
- **The common thread** — what 60%+ of the references share
- **The outliers** — references that contradict the majority (these are interesting — they
  might be the thing that makes the brand *unique*)
- **The tensions** — where references pull in opposite directions

**Step 3 — Surface tensions to the user**

Present what you found. Not a list of each reference — a synthesis:

**Solo mode:** Be concise. State the throughline and the main tension in 2–3 sentences:
"Tråden genom allt du valt är [X]. Men du har en spänning mellan [A] och [B] — jag lutar
åt [resolution]. Stämmer det?"

**Client session mode:** Use comparisons they can react to:
"Av era referenser ser jag två spår — ett mer [adjektiv] och ett mer [adjektiv]. Vilket
känns närmare er?"
Clarify what the 'adjectives' mean if the client seems unsure. For example, if they say
'modern', ask what that means to them. Does it mean minimalist? Tech-forward? Clean?

**Step 4 — Propose 2–3 directions**

Not full moodboards. Quick, named directions with one sentence each:
- **Direction A:** "Mörkt + serif + generöst — luxury editorial"
- **Direction B:** "Mörkt + grotesk + tight grid — tech-forward"
- **Direction C:** "Split — serif headers on dark, grotesk body on light"

In solo mode: pick the strongest one yourself and state why. User can override.
In client session: present all and let them react.

**Step 5 — Generate the full moodboard from the chosen direction**

Proceed to Phase 2 with the chosen direction locked in. The synthesis work you did
now informs every decision — palette, typography, motion, voice.

---

### Quick Start Mode

For lighter input (brand name + a feeling, or a brief description).

**Extract silently from context:**
- Brand name
- What the company does
- Who their customer is
- Any mentioned colors, references, or aesthetic words

**Decision tree:**
- If you have enough to make strong creative decisions → go straight to Phase 2, briefly
  stating what assumptions you're making
- If something critical is missing → ask ONE smart question (see below)
- If they say "kör bara" or seem impatient → make bold decisions and go, no questions asked

### The one smart question rule

Never ask more than one question at a time. Pick the most important gap and ask it in a way
that helps the user think, not just fill in a form.

**Bad:** "Kan du berätta mer om era färger, typsnitt, målgrupp och vad ni vill förmedla?"

**Good (solo):** "Mörkt eller ljust som bas?"

**Good (client session):** "En fråga innan jag kör — är känslan ni vill ha mer åt det mörka
och premium-hållet, eller ljust och tillgängligt?"

For clients who seem completely lost, use comparison questions — they're easier to answer
than open-ended ones:

**Good for clients:** "Tänk på ett varumärke ni tycker ser bra ut — det kan vara vad som
helst, ett klädesbolag, en app, en bil. Vad är det som tilltalar er med det?"

---

## Phase 2 — Brand Analysis (think before you build)

Before writing a single line of code, reason through the brand out loud in 4–6 sentences.
This is not optional — it creates alignment with the user before you commit to a direction.

Structure your reasoning like this:

**"Baserat på [vad du vet] läser jag det här varumärket som [positionering]. Det pekar mot
[mörkt/ljust/neutralt] som bas, med [accent] för att [varför]. För typsnitt tänker jag
[display font] + [body font] eftersom [ett konkret skäl]. Stämmer det med hur ni tänker?"**

Keep it to 3–5 sentences. Not a monologue. The goal is: user nods and says "ja kör" or
corrects you before you've built the wrong thing.

**If they correct you:** Update your analysis, confirm the new direction in one sentence, then build.

**If they say "ja kör" or don't respond:** Build.

### What to decide in this phase

1. **Positioning axis** — Pick one or two:
   - Premium ↔ Accessible
   - Technical ↔ Human
   - Bold ↔ Quiet
   - Young ↔ Established
   - Global ↔ Local

2. **Palette logic**
   - Base: Dark (#0A–#1A range), Light (#F0–#F8 range), or split
   - Accent: Should feel like a decision, not a default. Ask yourself: what color surprises
     you slightly but still fits? That's usually the right one.
   - Never pick safe colors for premium brands. Safe = forgettable.
   - Colors need personality names, not function names:
     - ✓ "Void", "Volt", "Cream", "Signal", "Dusk", "Chalk", "Ember"
     - ✗ "Primary", "Secondary", "Background", "Text"

3. **Typography**
   - Display font: must have character. If you could use it for any brand, don't use it.
   - Body font: must be readable at 14–16px, slightly distinctive, not clinical.
   - Never use: Inter, Roboto, Arial, system-ui, sans-serif as a standalone choice.
   - Good display: Syne, Playfair Display, Cormorant, Fraunces, Cabinet Grotesk, Bebas Neue,
     DM Serif, Clash Display
   - Good body: DM Sans, Instrument Sans, Plus Jakarta Sans, Figtree, Lora, Literata

4. **Voice & Verbal Identity** — This is about HOW the brand communicates, not just what it looks like.

   **Solo mode** — you already have a tone figured out, or can infer it from the references:
   - Extract voice from the conversation, any documents, or reference sites.
   - State your read concisely: "Rösten jag läser ut ur det här är [X]."
   - Move on. Don't deliberate.

   **Client session mode** — the client hasn't thought about voice:
   - Guide them with comparison questions, not theory.
   - **Good:** "Om ert företag var en person — pratar den som en coach, en kompis, en professor, eller en chef?"
   - **Good:** "Tänk på ert senaste Instagram-inlägg eller mail till en kund. Var det formellt eller avslappnat?"
   - Pick an archetype for them based on what you know. State it. Let them correct you.

   **Decide:**
   - **Personality archetype** — one word: Mentor, Challenger, Guide, Friend, Expert, Rebel, Craftsman
   - **Tone position** — where on the spectrum: Formell ↔ Avslappnad, Direkt ↔ Diplomatisk, Varm ↔ Saklig
   - **Vocabulary DNA** — 5–6 words the brand uses vs. 5–6 it avoids
   - **Communication principles** — 2–3 rules (e.g. "Alltid direkt, aldrig passiv", "Visa resultat, inte process")
   - **Voice ✓/✗** — 3 things the brand DOES say + 3 it NEVER says (specific, not generic)
     - ✗ "Vi är innovativa" (every brand says this)
     - ✓ "Vi förklarar inte — vi visar"

5. **Motion character**
   - Soft and organic (slow eases, breathing gradients)
   - Sharp and precise (quick transitions, clean snaps)
   - Playful (spring physics, bouncy easing)
   - Elegant (slow reveals, minimal motion)

6. **Mood words** — 7–9 words. 3 are "active" (the core), rest are supporting texture.

---

## Phase 3 — Generate the HTML

Write a complete, self-contained HTML file. All CSS and JS inline. No external dependencies
except Google Fonts (loaded via link tag).

### Layout: Bento Grid

12-column CSS grid, 80px base row unit, 12px gap.

```css
.grid {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  grid-auto-rows: 80px;
  gap: 12px;
}
```

Define span classes: c-2x2, c-3x2, c-3x3, c-4x2, c-4x3, c-4x4, c-6x2, c-6x3, c-6x4,
c-8x3, c-12x2. Mix sizes — no uniform grid.

### Required cards

**1. Brand Statement** — Large, light bg, dark text. One bold headline, one accent-colored
word. Display font, 800 weight, tight leading. This is the emotional anchor of the moodboard.

**2. Color Palette** — Wide card. Swatches flex side by side. Hover → swatch expands
(flex: 1.6). Each swatch: name + hex code. Mix-blend-mode: difference on text so it's
always readable regardless of swatch color.

**3. Atmosphere** — Dark card, radial gradient bg using brand colors at low opacity (0.08–0.15).
No body text. Just a label and 2–3 descriptor words (e.g. "Dark · Organic · Premium").
This card should *feel* like the brand's emotional space.

**4. Accent Card** — Solid accent color. 3 core brand adjectives in large display font. Black text.
Simple, confident.

**5. Typography Display** — Shows "Aa" + brand name in display font at large size. Font name as label.

**6. Typography Body** — Shows body font in a real, brand-specific sentence (not lorem ipsum).
Shows font pairing reference below.

**7. Voice & Tone** — 3 ✓ (accent color) and 3 ✗ (accent2, strikethrough). Specific to THIS brand.

**8. Motion Principles** — 4–5 motion behaviors. Each with a pulsing animated dot (staggered
animation-delay). These should describe the actual motion character decided in Phase 2.

**9. Mood Words** — Wide card, words at varied sizes and opacities. 3 active (full opacity),
rest at 0.12. On card hover: rest fade to 0.06, actives stay at 1. Creates a reveal effect.

**10. Border Beam Demo** — Rotating conic-gradient border (3s linear infinite). Shows brand
accent color in motion. Label: "Detail · Border Beam".

**11. Micro Animation Demo** — At minimum:
- A circle element that scales + rotates on hover (cubic-bezier spring)
- A progress bar that loops (scaleX 0→1)
Both should use brand accent color.

**12. CTA / Button Preview** — Primary button (accent bg, dark text) + ghost button (transparent,
border). Both have hover states. Label: "Hover för att se states".

**13. Dark / Light Split** — Card split 50/50. Left: dark bg, right: light bg. Each labeled with
which sections of the site use that tone. Separated by a subtle vertical line.

**14. Tagline** — Full-width card. Brand tagline in italic body font. Brand name + year
right-aligned. This is the last thing you see — it should land.

**15. Brand Voice Profile** — Medium-to-wide card. Shows the verbal identity at a glance:
- **Top:** Personality archetype in display font, large (e.g. "Mentor")
- **Middle:** Tone spectrum as a visual slider — a horizontal line with a marker showing
  position between two poles (e.g. "Formell ●———————— Avslappnad"). Use CSS for the
  marker, accent color.
- **Bottom left:** "Vocabulary DNA" — two columns, left: 5 words the brand uses (accent
  colored), right: 5 words it avoids (muted, strikethrough)
- **Bottom right:** 2–3 communication principles in small body font
- **Below the card:** A comparison block — the same message written two ways:
  - ✓ "In-brand" version (accent border-left, full opacity)
  - ✗ "Generic" version (muted, faded, strikethrough)
  This is the most powerful part — it makes the voice *tangible* for people who
  don't think in design abstractions.

### Card rules

- Every card has a `label` (10px, 500 weight, 0.12–0.15em letter-spacing, uppercase, muted)
- Cards lift on hover: `transform: translateY(-4px)`, subtle border-color brightening
- Base card: dark bg (#111), border `rgba(255,255,255,0.08)`, border-radius 12px
- Padding: `20px 24px`
- Hover transition: `cubic-bezier(0.34, 1.56, 0.64, 1)` — spring feel

### CSS architecture

```css
:root {
  --black: /* darkest bg, never pure #000 */;
  --white: /* lightest surface, slightly warm, never pure #FFF */;
  --accent: /* primary accent — bold, confident */;
  --accent2: /* secondary, used for ✗ marks and signal moments */;
  --mid: /* muted labels and secondary text */;
  --border: rgba(255,255,255,0.08);
  --display-font: 'FontName', sans-serif;
  --body-font: 'FontName', sans-serif;
}
```

### Required animations

- **Border beam**: conic-gradient rotation, 3s linear infinite
- **Motion dots**: pulse (scale + opacity), staggered animation-delay per dot
- **Micro circle**: hover → scale(1.2) rotate(10deg), spring cubic-bezier
- **Progress bar**: scaleX(0→1) loop, transform-origin: left
- **Swatch expand**: flex transition on hover
- **Card lift**: translateY(-4px) on hover, spring easing

### Header

```
[BRAND NAME] — Brand Moodboard          v0.1 · [Month Year]
─────────────────────────────────────────────────────────
```

Brand name in display font, small, slightly muted. Right side: version + date. Thin border-bottom.

---

## Phase 4 — After Delivery

After presenting the file, say one short sentence: what the core creative decision was and why.

Example: "Jag gick med en kall, mörk bas och elektrisk grön accent för att spegla att ni är
tekniskt duktiga men med en edge — öppna filen i Chrome för att se animationerna."

Then stop. Don't over-explain. Let the moodboard do the work.

### If they say "inte riktigt" or "gillar det inte"

Don't regenerate immediately. Ask one diagnostic question to understand what's off:

**"Vad är det som inte stämmer — är det färgerna, typografin, känslan i stort, eller något
specifikt kort?"**

Based on their answer:
- **Färgerna** → Ask: "För varmt, för kallt, eller fel accentfärg?" Then regenerate palette.
- **Typografin** → Ask: "Vill ni ha något skarpare/modernare eller mjukare/mer klassiskt?"
- **Känslan i stort** → Means the positioning was wrong. Re-read Phase 2, correct the axis,
  regenerate.
- **Specifikt kort** → Fix just that card. Don't rebuild everything.

### If they say "nästan, men..."

This is the best case. They're oriented. Extract what works, fix what doesn't. Confirm in
one sentence what you're keeping and what you're changing before you do it.

### For clients who don't know what to change (client session mode)

If the client seems unsure how to give feedback, help them with this:

**"Tänk på känslan när du öppnar moodboarden — första tre sekunder. Är den rätt, för
aggressiv, för lugn, eller något annat?"**

First impressions are more honest than considered opinions for people unfamiliar with
design feedback.

---

## Phase 5 — DNA Bridge (Handoff to Pipeline)

When the user approves the moodboard and wants to build a website from it, extract the
creative decisions into the Zaitex pipeline:

### What to extract into `active-dna.md`:

| Moodboard Element          | DNA Section                  |
|:---------------------------|:-----------------------------|
| Color palette swatches      | 🎨 Color Palette             |
| Display + body fonts        | 📝 Typography                |
| Motion character            | 🎬 Motion DNA                |
| Mood words (active 3)       | 🎯 Design Principles         |
| Voice & tone (✓/✗)          | 🔑 Signatures                |
| Brand Voice Profile         | → `07-copywriter` skill brief |
| Personality archetype       | → `07-copywriter` skill brief |
| Tone spectrum position      | → `07-copywriter` skill brief |
| Vocabulary DNA              | → `07-copywriter` skill brief |
| Communication principles    | → `07-copywriter` skill brief |
| Dark/light split            | 🔑 Signatures → Layout       |
| Accent card adjectives      | 🎯 Design Principles         |

### Handoff steps:

1. **Fill `active-dna.md`** — Map all approved moodboard values into the DNA template
2. **Generate copywriter brief** — Write a `copy-voice.md` file in `.agent/project/` containing
   the personality archetype, tone position, vocabulary DNA, communication principles, and the
   example comparison sentence. This becomes the source of truth for `07-copywriter`.
3. **Hand off to `01-design-director`** — to confirm/refine and extend the DNA with
   component-level decisions (card styles, button shapes, hover behaviors)
4. **If `00-brief-architect` hasn't run yet** — run it first to gather business context,
   THEN apply the moodboard's visual decisions on top

### The bridge sentence:

When handing off, tell the user:

**"Moodboarden är godkänd. Jag har extraherat färger, typsnitt och motion-karaktär till
active-dna.md. Nästa steg: Design Director förfinar det till komponentnivå, sen börjar vi
bygga."**

---

## Quality Checklist (run before every output)

- [ ] Fonts are NOT Inter / Roboto / Arial / system-ui
- [ ] Colors have personality names, not function names
- [ ] Accent color is bold — not the safe choice
- [ ] Voice/tone items are brand-specific, not generic virtues
- [ ] Mood words are varied in size AND opacity — not a uniform list
- [ ] Grid has genuinely mixed card sizes
- [ ] All animations are CSS-only
- [ ] The brand statement actually sounds like THIS brand
- [ ] The atmosphere card feels like the right emotional space
- [ ] Typography body card uses a real sentence, not placeholder text
- [ ] Voice profile has a real personality archetype, not a generic one
- [ ] Tone spectrum position is specific (not centered/neutral by default)
- [ ] Vocabulary DNA words are specific to THIS brand's industry and culture
- [ ] The comparison sentence makes the voice difference immediately obvious

---

## Output

Save the moodboard HTML file to the project root as `[brandname]_moodboard.html`.

Tell the user: "Öppna filen i Chrome så ser du den live med animationer."

Then ask: "Vill ni bygga en sajt från det här? Då extraherar jag allt till active-dna.md
och vi kör igång med pipelinen."

---

## The Underlying Philosophy

This is not a template machine. It's a creative synthesis engine.

Its core job is taking scattered aesthetic intuition — 25 templates, a feeling you can't
name, a typography screenshot from last Tuesday — and finding the throughline. The moment
when the system says "tråden genom allt du valt är X" and you go "ja, det är det" —
that's the whole point.

For clients, the moodboard is often the first time they see their brand as a visual reality.
That moment matters. Make it count.

For you as the designer, this is about speed and clarity. You know more than you can
articulate in text. The system's job is to read your taste from your choices and help you
see the pattern in what you've already decided.

When in doubt: be bolder. Safe is forgettable. A moodboard that sparks a reaction —
even a "hmm, not quite" — is more valuable than one that gets a polite nod.
