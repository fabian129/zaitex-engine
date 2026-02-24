---
name: brief-architect
description: Project intake and strategic planning skill. Takes raw client data (meetings, documents, playbooks, existing sites, templates) and produces a complete project blueprint with downstream briefs for every skill in the pipeline. Also generates client-facing brand documentation. Use this skill at the START of every new project, when onboarding a new client, when receiving client documents/playbooks, when the user says "new project", "new client", "plan this", "brief this", or provides meeting notes and client materials. This skill runs BEFORE everything else in the pipeline.
---

## TL;DR
**Skill:** 00 — Brief Architect  
**Phase:** Phase 0 (Intake & Routing)  
**Purpose:** Define project scope, constraints, and MODE (AURA / LITE / ENGINE)  
**Change Budget:** None (read-only planning)  
**Output:** Structured brief + explicit MODE decision  
**Stop:** After MODE is declared and constraints are clear  
**Redirects:** → INDEX (Phase 1)

# Brief Architect

## Objective
Transform raw client chaos into structured, actionable project documentation. This skill is the bridge between "the client sent us a bunch of stuff" and "the agent knows exactly what to build."

## Philosophy
**Not:** "Let me start coding based on these meeting notes."
**Instead:** "Let me understand the client's world first, then create a blueprint that every skill can execute on."

Clients rarely have their brand documented. Meeting notes are messy. Playbooks are long. The Brief Architect reads everything, asks the right questions, and produces two things:
1. **Internal briefs** that the agent pipeline consumes
2. **Client-facing documentation** that the client can keep, share, and use beyond this project

---

## When to Run
- Start of every new project
- When onboarding a new client
- When receiving a batch of client documents
- When pivoting an existing project based on new information
- When creating a demo/pitch site for a prospect

---

## Inputs (What You Might Receive)

The skill must handle any combination of these. Sometimes all of them, sometimes just one.

| Input Type | Examples | What to Extract |
|:-----------|:---------|:----------------|
| **Meeting notes** | Fathom summaries, call transcripts, action items | Goals, decisions, tone of voice, priorities |
| **Client documents** | Playbooks, ICPs, pricing docs, audit frameworks | Service structure, target audience, terminology, value proposition |
| **Existing site** | URL or screenshot of current/draft site | What works, what's missing, current positioning |
| **Aura template** | HTML file from Aura.build | Existing sections, visual direction, gaps to fill |
| **Reference sites** | URLs or screenshots the client likes | Aesthetic preferences, layout patterns, feature expectations |
| **Verbal brief** | "Build a site for an event agency" | Starting point — requires more questions |
| **Brand assets** | Logos, color preferences, font preferences | Visual constraints |

### Handling Sparse Input
If you receive very little (just a verbal brief or a single document):
1. Make reasonable assumptions based on industry and business type
2. Mark every assumption clearly: `[ASSUMPTION — verify with client]`
3. Present assumptions in the brief for approval before proceeding
4. Don't ask 20 questions upfront — assume smartly, verify later

### Handling Dense Input
If you receive a lot (10+ documents, long meeting notes, multiple playbooks):
1. Read everything before producing anything
2. Don't summarize each document separately — synthesize across all of them
3. Look for contradictions between documents and flag them
4. Identify what's relevant to the website vs what's internal business documentation

---

## Phase 1: Ingest & Understand

### Step 1: Read Everything
Consume all provided materials. Don't start producing output yet. Build a mental model of:
- What does this business do?
- Who do they sell to?
- What's their unique positioning?
- What language do they use? (Their words, not generic marketing speak)
- What are they trying to achieve with this website?
- What exists already?

### Step 2: Identify the Project Type

| Type | Characteristics | Approach |
|:-----|:----------------|:---------|
| **Full build from scratch** | No existing site, client has documents/brief | Full blueprint, design direction needed |
| **Template-based build** | Aura template or reference site as starting point | Gap analysis: what template has vs what client needs |
| **Rebuild/redesign** | Existing site that needs improvement | Audit existing, preserve what works, fix what doesn't |
| **Demo/pitch site** | Building to sell to a prospect, not a signed client | Fast, impressive, use Sandbox Mode, less documentation |
| **Expansion** | Adding pages/sections to existing project | Read existing DNA, plan additions only |

### Step 3: Extract Core Elements

From all the input, extract these:

**Business Identity**
```
Company:        [Name]
Industry:       [Specific niche, not just "consulting"]
Positioning:    [How they describe themselves — use THEIR words]
USP:            [What makes them different from competitors]
```

**Target Audience**
```
Primary:        [Who they mainly sell to — be specific]
Secondary:      [If applicable]
Pain Points:    [What problems the audience has]
Language:       [How the audience talks about their problems]
```

**Offerings / Services**
```
Tier 1:         [Entry level — name, price if known, description]
Tier 2:         [Mid level]
Tier 3:         [Premium level]
...
```

**Conversion Goals**
```
Primary:        [The #1 thing a visitor should do — book call, buy, sign up]
Secondary:      [Secondary action — download, subscribe, explore]
Funnel:         [How they get from visitor → customer]
```

**Voice & Tone**
```
Personality:    [ex. "Authoritative but approachable", "Bold and direct"]
Keywords:       [Words they use repeatedly — "Executive Architecture", "EBITDA-skydd"]
Avoid:          [Words/tone they'd never use]
Register:       [Formal / Professional / Casual / Technical]
```

**Existing Assets**
```
Logo:           [Yes/No, format]
Colors:         [If specified]
Fonts:          [If specified]
Photography:    [Style preference, existing images]
Content:        [Blog posts, case studies, testimonials available?]
```

**Technical Requirements**
```
Functionality:  [Forms, calculators, booking, e-commerce, audit tools]
Integrations:   [CRM, email marketing, payment, analytics]
CMS:            [Does client need to edit content?]
Hosting:        [Preference — Vercel, existing host]
```

---

## Phase 2: Produce the Blueprint

### The Project Brief (`project-brief.md`)

This is the master document. Everything else derives from it.

**STOP POINT 🛑**: Present this to the user for approval before proceeding to Phase 3.

```markdown
# Project Brief: [Client Name]

## 1. Client Summary
[2-3 sentences: who they are, what they do, who they serve]

## 2. Project Type
[Full build / Template-based / Rebuild / Demo / Expansion]

## 3. Business Identity
Company:     [Name]
Industry:    [Niche]
Positioning: [Their words]
USP:         [Differentiator]

## 4. Target Audience
Primary: [Description]
- Pain: [What hurts]
- Want: [What they're looking for]
- Language: [How they describe it]

Secondary: [If applicable]

## 5. Offerings
[List tiers/services with descriptions]

## 6. Conversion Strategy
Primary Goal: [Action]
Secondary Goal: [Action]
Funnel: [Path from visitor → customer]

## 7. Voice & Tone
Personality: [Description]
Key Terms: [Words to use]
Avoid: [Words to never use]
Register: [Formal/Casual/etc]

## 8. Site Structure

### Pages Needed
1. [Page] — [Purpose]
2. [Page] — [Purpose]
...

### Section Flow: [Main Page]
| # | Section | Goal | Key Content |
|:--|:--------|:-----|:------------|
| 1 | Hero | [Goal] | [Content summary] |
| 2 | [Name] | [Goal] | [Content summary] |
| ... | | | |

### Section Flow: [Additional Pages]
[Repeat per page if multi-page site]

## 9. Recommended Additions
[Sections/features the client didn't mention but should have]
| Suggestion | Why | Priority |
|:-----------|:----|:---------|
| [Section/Feature] | [Business reason] | High/Medium/Low |

## 10. Design Direction
Vibe: [Description]
References: [Sites/templates that match]
Template: [If Aura template, which one and what to modify]
[ASSUMPTION] markers if guessing

## 11. Technical Requirements
[Functionality, integrations, CMS needs]

## 12. Existing Assets
[What the client has provided: logos, copy, images, documents]

## 13. Open Questions
[Anything that couldn't be determined from the input]

## 14. Assumptions
[Everything marked as assumption, collected here for easy review]
```

---

## Phase 3: Break Down to Skill Briefs

After the user approves the Project Brief, generate these files:

### File Structure
```
.agent/
├── design/
│   └── active-dna.md              ← Generated after Design Director runs
└── project/
    ├── project-brief.md           ← The master document (Phase 2)
    ├── design-direction.md        ← For Design Director
    ├── page-plan.md               ← For Page Planner
    ├── copy-brief.md              ← For Copywriter
    ├── tech-spec.md               ← For Component Architect
    ├── section-suggestions.md     ← Recommended additions
    └── brand-bible.md             ← Client-facing deliverable
```

### design-direction.md (→ Design Director)

```markdown
# Design Direction: [Client Name]

## Vibe
[Description of the feeling the site should evoke]

## Industry Archetype
[ex. "Premium B2B Consulting" / "Creative Agency" / "Service Business"]

## Suggested References
1. [URL/description] — Why: [what to take from it]
2. [URL/description] — Why: [what to take from it]
3. [URL/description] — Why: [what to take from it]

## Starting Point
[If Aura template: which one and what modifications needed]
[If from scratch: suggested aesthetic direction]

## Client Preferences
[Any explicit preferences from meetings/documents]

## Constraints
[Colors they want, colors to avoid, any visual requirements]
```

### page-plan.md (→ Page Planner)

```markdown
# Page Plan: [Client Name]

## Business Goal
[Primary conversion from brief]

## Target Audience
[From brief — keep short]

## Pages

### Page: [Main Landing Page]

| # | Section | Goal | Content | CTA |
|:--|:--------|:-----|:--------|:----|
| 1 | Hero | [Goal] | [Content] | [CTA text] |
| 2 | [Name] | [Goal] | [Content] | [CTA if applicable] |
| ... | | | | |

### Page: [Additional Page]
[Repeat]

## Section Suggestions (Not in Original Brief)
[From section-suggestions.md — included here for context]
```

### copy-brief.md (→ Copywriter)

```markdown
# Copy Brief: [Client Name]

## Voice & Tone
Personality: [From brief]
Register: [Formal/Casual/etc]

## Key Terms (USE THESE)
- [Term 1] — [Context for when to use it]
- [Term 2] — [Context]
...

## Avoid (NEVER USE)
- [Word/phrase]
- [Word/phrase]

## Audience Language
[How the target audience describes their problems — write copy that mirrors this]

## Copy Needed Per Section

### Hero
- Headline direction: [Concept, not final copy]
- Subtext direction: [What to communicate]
- CTA: [Specific action, not "Learn More"]

### [Section 2]
- Headline direction: [Concept]
- Key message: [What this section must communicate]
- Proof points: [Data, testimonials, specifics to include]

### [Continue for all sections]

## SEO Considerations
Primary keyword: [If known]
Secondary keywords: [If known]
Location: [If local business]
```

### tech-spec.md (→ Component Architect)

```markdown
# Technical Spec: [Client Name]

## Functionality Required

### [Feature 1: ex. Digital Audit Tool]
- Description: [What it does]
- User flow: [Step by step]
- Input: [What user provides]
- Output: [What user receives]
- Integration: [External services needed]
- Priority: [Must-have / Nice-to-have]

### [Feature 2: ex. Booking Integration]
- Description: [What it does]
- Service: [Calendly / Cal.com / custom]
- Priority: [Must-have / Nice-to-have]

## Forms
[List all forms needed with fields]

## Third-Party Integrations
[Analytics, CRM, email, payment, etc.]

## CMS Requirements
[Does client need to edit content? What content?]

## Performance Requirements
[Any specific needs — fast mobile, heavy animation OK, etc.]
```

### section-suggestions.md

```markdown
# Section Suggestions: [Client Name]

These sections were not mentioned by the client but are recommended based on their business type, audience, and conversion goals.

| Section | Why It's Needed | Where to Place | Priority |
|:--------|:----------------|:---------------|:---------|
| Social Proof / Logos | [Business reason] | After Hero or after Features | High |
| FAQ | [Business reason] | Before Contact | Medium |
| Case Studies | [Business reason] | After Services | High |
| Process / How It Works | [Business reason] | After Hero | Medium |
| ... | | | |

## For Each Suggestion

### [Section Name]
**Why:** [Specific business reason, not generic]
**Content needed:** [What goes in it]
**Example reference:** [URL or description of a good version of this section]
**Can skip if:** [Condition under which this isn't needed]
```

---

## Phase 4: Brand Bible (Client-Facing)

This is the deliverable the client keeps. It's written for humans, not agents. Professional tone, clean formatting, no internal jargon.

Generate this AFTER Design Director has run and `active-dna.md` is populated.

### brand-bible.md (→ Client delivery)

```markdown
# Brand Bible: [Client Name]

## Brand Identity

### Who We Are
[2-3 sentences — positioning statement]

### Who We Serve
[Target audience description in human language]

### Our Voice
[How we speak — with examples]
- We say: "[example phrase]"
- We don't say: "[example phrase]"

### Our Promise
[Value proposition in one sentence]

---

## Visual Identity

### Color Palette
[Colors with hex codes, shown with purpose]
- Primary: #___ — Used for CTAs, key actions
- Secondary: #___ — Used for accents, highlights
- Background: #___ — Page backgrounds
- Text: #___ — Body text

### Typography
- Headings: [Font Name] — [Where it's used]
- Body: [Font Name] — [Where it's used]

### Visual Style
- [Description of visual signatures — sharp corners, specific shadow style, etc.]
- [Photography style if applicable]
- [Icon style if applicable]

---

## Messaging Framework

### Headline Templates
- Hero: [Pattern — ex. "[Action verb] + [Outcome] + [For whom]"]
- Section: [Pattern]

### Key Messages
1. [Message 1 — the #1 thing people should remember]
2. [Message 2]
3. [Message 3]

### Elevator Pitch
[30-second description of the business]

---

## Digital Presence

### Website Structure
[Pages and their purpose — simple overview]

### Social Media Tone
[If applicable — how brand voice adapts to social]

### Content Themes
[What topics the brand should talk about]

---

## Usage Guidelines

### Logo Usage
[Minimum size, clear space, what not to do]

### Color Usage
[When to use which color, contrast requirements]

### Photography
[Style guidelines — dark/light, people/abstract, filters]

---

*Generated by Zaitex Engine • [Date]*
```

---

## Phase 5: Handoff to Pipeline

After all briefs are generated and approved:

1. **If design direction is clear** → Skip Design Director, go straight to Page Planner with `page-plan.md`
2. **If design direction needs exploration** → Design Director reads `design-direction.md` and proposes options
3. **Copywriter** reads `copy-brief.md` and produces copy BEFORE layout begins
4. **Component Architect** reads `tech-spec.md` for any functional requirements
5. **All skills** reference `project-brief.md` as the source of truth for client context

### Integration with Existing Pipeline

```
Brief Architect (NEW — runs first)
    ↓ produces briefs
Design Director ← reads design-direction.md
    ↓
Page Planner ← reads page-plan.md
    ↓
Copywriter ← reads copy-brief.md
    ↓
[Rest of pipeline as normal]
```

### Integration with Aura Migration

If starting from an Aura template:
1. Brief Architect produces the blueprint
2. Aura Migration converts the template
3. Brief Architect's `section-suggestions.md` identifies gaps
4. Agent adds missing sections using the normal pipeline
5. Copywriter replaces template copy with client-specific copy from `copy-brief.md`

---

## Industry-Specific Section Libraries

When suggesting sections, reference these common patterns:

### B2B Consulting / Professional Services
- Hero with authority positioning
- Problem/Gap statement ("The problem we solve")
- Methodology / Framework visualization
- Case Studies / Results
- Value Ladder / Pricing tiers
- Trust Signals (logos, certifications, press)
- About / Team
- FAQ
- Booking CTA

### Creative Agency / Portfolio
- Hero with featured work
- Portfolio Grid / Case Studies
- Services overview
- Process visualization
- Team
- Testimonials
- Contact with personality

### Service Business (Local)
- Hero with clear service + location
- Services grid
- Before/After or Results
- Reviews / Testimonials
- Service area map
- Pricing (if applicable)
- FAQ
- Contact with form + phone

### E-commerce / Product
- Hero with flagship product
- Product categories
- Featured products
- Social proof / Reviews
- How it works (if applicable)
- Trust badges (shipping, returns, security)
- Newsletter signup

### SaaS / Tech
- Hero with product demo/screenshot
- Feature grid (bento)
- How it works (3 steps)
- Pricing table
- Integrations
- Testimonials / Case studies
- FAQ
- CTA banner

### Personal Brand / Thought Leader
- Hero with personal positioning
- Methodology / Framework
- Content / Resources (books, podcasts, articles)
- Speaking / Events
- Testimonials
- Media / Press
- Newsletter signup
- Contact / Booking

---

## Cross-Skill References

| When... | Hand off to... |
|:--------|:---------------|
| Design direction needs exploration | **Design Director** with `design-direction.md` |
| Page structure is defined | **Page Planner** with `page-plan.md` |
| Copy needs writing | **Copywriter** with `copy-brief.md` |
| Technical features identified | **Component Architect** with `tech-spec.md` |
| Aura template is starting point | **Aura Migration** + section suggestions |
| Brand Bible needs visual data | Wait for **Design Director** to populate `active-dna.md` first |

---

## Key Principles

1. **Read everything before producing anything.** Don't start writing the brief after reading the first document.
2. **Use the client's language.** If they say "EBITDA-skydd", you write "EBITDA-skydd", not "financial protection."
3. **Suggest what they missed.** Clients don't know what sections a website needs. You do.
4. **Mark assumptions clearly.** If you're guessing, say so. Let the user verify.
5. **One approval gate.** The Project Brief is the single checkpoint. After that, the pipeline runs.
6. **The Brand Bible is a deliverable.** It's not internal documentation — it's something the client pays for and keeps.
