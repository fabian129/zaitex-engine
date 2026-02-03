# Zaitex Engine

> A design system for building the best websites in the world.

## 🎯 What is This?

The Zaitex Engine is a **universal AI-powered website building system** containing:

- **12 Sequential Skills** — From design research to deployment
- **Section Templates** — Reusable Hero, Features, Pricing blueprints
- **DNA Templates** — Starter style configs for different industries
- **Visual Reference Library** — 100+ screenshots and URLs for prompting AI

---

## 📁 Structure

```
.agent/core/
├── 00-philosophy.md           # Core mindset & standards
├── 01-core-stack.md           # Required dependencies
│
├── skills/                    # The 12-skill pipeline
│   ├── 01-design-director.md
│   ├── 02-page-planner.md
│   ├── 03-layout-architect.md
│   ├── 04-component-selector.md
│   ├── 05-component-architect.md
│   ├── 06-motion-choreographer.md
│   ├── 07-copywriter.md
│   ├── 08-performance-guardian.md
│   ├── 09-style-propagator.md
│   ├── 10-accessibility-auditor.md
│   ├── 11-browser-validator.md
│   └── 12-deployment-packager.md
│
├── section-templates/         # Reusable section blueprints
│   ├── hero-split.md
│   ├── hero-centered.md
│   └── features-grid.md
│
├── design-templates/          # Starter DNA configs
│   ├── service-business.json
│   ├── premium-agency.json
│   └── minimal-saas.json
│
├── references/                # Visual prompting library
│   ├── component-examples/    # Cards, CTAs, Buttons, etc.
│   └── inspiration-sites/     # Minimal, Tech, Company styles
│
└── workflows/                 # Automation scripts
    └── setup-project.md
```

---

## 🚀 Usage

### Option 1: Git Submodule (Recommended)
```bash
# Add to a new project
git submodule add https://github.com/fabian129/zaitex-engine.git .agent/core

# Update to latest
git submodule update --remote
```

### Option 2: Copy
Just copy the contents into your project's `.agent/core/` folder.

---

## 🎨 DNA Lock Workflow

1. **ITERATE** — Build Hero + section, tweak `design_dna.json`
2. **LOCK** — Run `npm run dna:lock`
3. **EXTEND** — Build rest of site
4. **UNLOCK** — Edit JSON, re-run hydrate

---

## 📚 Skills Pipeline

| # | Skill | Purpose |
|:--|:------|:--------|
| 01 | Design Director | Research & extract DNA from references |
| 02 | Page Planner | Plan sections from client brief |
| 03 | Layout Architect | Decide grid layouts |
| 04 | Component Selector | Pick the right components |
| 05 | Component Architect | Build custom components |
| 06 | Motion Choreographer | Add animations |
| 07 | Copywriter | Write content |
| 08 | Performance Guardian | Optimize images & code |
| 09 | Style Propagator | Ensure consistency |
| 10 | Accessibility Auditor | WCAG compliance |
| 11 | Browser Validator | Visual QA |
| 12 | Deployment Packager | Deploy to Vercel |

---

## 🖼️ Visual Reference Library

The `references/` folder contains 100+ screenshots and URLs organized by:
- **Component type** (Cards, CTAs, Buttons, Footers, etc.)
- **Style** (Minimal, Tech, Company)

Use these images to **prompt the AI** instead of describing layouts in words:
> "Build a hero section like the one in `references/inspiration-sites/Minimal.md`"

---

## 📄 License

Private. For internal use only.
