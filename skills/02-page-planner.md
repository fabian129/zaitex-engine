---
name: page-planner
description: Strategic planning skill - creates sitemap and section flow from client brief
---

# Page Planner

## Objective
Transform client brief into a strategic page structure that achieves business goals.

## Process

### Step 1: Extract Requirements from Brief
**Input:** Client brief, brand guidelines, business goals  
**Extract:**
- **Business Goal:** What's the primary conversion? (book consultation, buy product, sign up)
- **Target Audience:** Who are they? (B2B, B2C, technical, non-technical)
- **Brand Constraints:** Required colors, fonts, prohibited elements
- **Compliance:** Accessibility level (WCAG AA/AAA), legal requirements
- **Voice/Tone:** Professional, casual, bold, clinical

**Output Structure:**
```markdown
## Client Requirements
- **Goal:** Get consultation bookings
- **Audience:** Law firm clients (B2C, non-technical)
- **Brand Colors:** Navy blue (#003366) primary
- **Compliance:** WCAG AA, no auto-play video
- **Tone:** Professional, trustworthy, conservative
```

### Step 2: Understand the Goal
Ask yourself:
- What action should the visitor take? (Buy, contact, sign up, learn)
- What does the client do? (Product, service, agency)
- Who is the target audience? (B2B, B2C, technical, non-technical)

### Step 3: Map the Journey
Visitor psychology follows this pattern:
1. **Grab attention** (Hero - 3 seconds to hook)
2. **Build trust** (Social proof, logos, testimonials)
3. **Explain value** (Features, benefits, how it works)
4. **Overcome objections** (FAQ, guarantees, comparisons)
5. **Drive action** (Pricing, CTA, contact)

### 3. Create Section Flow
Use this template:

```markdown
# [Site Name] - Page Plan

## Business Goal
[Primary conversion goal]

## Target Audience
[Who we're targeting]

## Section Flow

### 1. Hero
- **Goal:** [Grab attention + communicate value]
- **Content:** [Headline concept, key message]
- **CTA:** [Primary action]

### 2. [Next Section]
- **Goal:** [Why this section exists]
- **Content:** [What goes here]
- **CTA:** [If applicable]

[Continue for all sections]

## Validation
✓ Does the hero immediately communicate what we do?
✓ Is the conversion path clear?
✓ Are we addressing the main visitor objections?
✓ Is the primary CTA visible without scrolling?
```

## Output Format
Save as `docs/page-plan.md` with clear section goals.

## Example

**Brief:** "Design agency wants to show portfolio and get consultation bookings"

**Output:**
```markdown
# Agency Portfolio - Page Plan

## Business Goal
Get qualified consultation bookings

## Section Flow

### 1. Hero
- **Goal:** Communicate we're premium + different
- **Content:** Bold headline about unforgettable brands
- **CTA:** "See Our Work" (scroll to portfolio)

### 2. Portfolio Grid
- **Goal:** Prove our quality
- **Content:** 6-9 best case studies
- **CTA:** "View Case Study" on each

### 3. Process
- **Goal:** Demystify how we work (build trust)
- **Content:** 3-step process visualization

### 4. Testimonials
- **Goal:** Social proof
- **Content:** 3 client quotes with photos

### 5. Contact
- **Goal:** Convert to booking
- **Content:** Calendar integration
- **CTA:** "Book Free Consultation"
```

## Key Principle
**Every section must have a clear "why"** - if you can't explain why it exists, cut it.
