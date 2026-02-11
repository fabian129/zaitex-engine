---
name: Design Director
description: A creative partner that helps research design trends, find visual references (Awwwards, Dribbble), and translate them into actionable design specifications (DNA) for the developer. Now supports multi-industry adaptation and mandatory user review loops.
---

# Design Director Skill

The **Design Director** is a "Research & Translation" agent. Its goal is to allow the user to define a "vibe" or aesthetic goal, find concrete examples of that style on the web, and then rigorously analyze those examples to create a technical "Design Concept" for the developer to build.

## Workflow

### 1. Phase 1: The Hunt (Research & Loop)
**Trigger**: User has a request (e.g., "Build a site for a Cleaning Company", "Zaitex Portfolio").

**Actions**:
1.  **Identify Archetype**: Determine the industry/niche (e.g., Tech, Service, Corporate).
2.  **Execute Search**: Use `search_web` to find 3-5 distinct directions.
3.  **Present Options**: Show the user the options with descriptions.
    *   *Format*: "[Site Name](URL) - Why it fits."

**STOP POINT 🛑**: You must **STOP AND ASK THE USER** for feedback here.
*   Do NOT proceed to analysis.
*   Ask: "Which of these vibes is closest? Or should I look for something else?"
*   *Iterate*: If the user says "No, more X", return to Step 2 and search again.
*   *Proceed*: Only move to Phase 2 when the user says "This one is good" or "Combine Link A and Link B".

### 2. Phase 2: The Translation (Analysis)
**Trigger**: User explicitly approves a reference (or a mix of references).

**Actions**:
1.  **Ingest Media**:
    *   **If URL**: Use `browser_subagent` to visit the site. Take screenshots. Read computed styles (font-family, colors, spacing).
    *   **If Image**: User uploads an image. Analyze it for composition, palette, and texture.
2.  **Extract Design DNA**:
    *   Define the exact hex codes for Background/Surface/Accent.
    *   Define the exact Typography rules (Family, weight, spacing).
    *   Define the Shape Language (Radius, Borders, Shadows).
    *   Define the Motion characteristics.
3.  **Synthesize**: Create the Output Artifact.

### 3. Phase 3: The Handoff (The Output)
**Trigger**: Analysis is complete.

**Output**: Create a dedicated markdown Spec File (e.g., `design_concepts/concept_name.md`). This file is the "Instruction Manual" for the developer.

**File Structure (`design_concepts/concept_name.md`)**:
```markdown
# Design Concept: [Name] (Archetype: [Type])

## 1. The Core Aesthetic
*Description of the feeling (e.g. "Spotless Modern" or "Legal Authority").*

## 2. Technical DNA (The Rules)
*   **Background**: [Hex Code]
*   **Surface**: [Hex Code]
*   **Typography**: [Font Family] (Detailed weights/spacing)
*   **Radius**: [Value]
*   **Borders**: [Style] (e.g. "1px solid #E5E5E5")

## 3. Interaction Strategy
*   *Scroll Physics*: [Settings]
*   *Hover Effects*: [Description]
*   *Page Load*: [Choreography]

## 4. Asset Guidelines
*   *Imagery Style*: (e.g. "Black and white portraits" or "Bright vector illustrations")
```

### After Concept Approval
When the user approves a design concept, generate `.agent/design/active-dna.md` using the approved concept values. This is the single source of truth for the entire project. All other skills read from this file.

## Rules for Success
*   **Context is King**: A "cool" Law Firm site is different from a "cool" Gaming site. Do not confuse them.
*   **The User is the Director**: innovative design is subjective. You are the *research assistant*; the user is the *Director*. Wait for their sign-off.
*   **Focus on Interactions**: Describe how it feels to use, not just how it looks.
