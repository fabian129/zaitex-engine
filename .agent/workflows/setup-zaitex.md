---
description: Set up a new Zaitex project automatically with the Base DNA and Production-Ready Core Stack
---

# Zaitex Project Setup Workflow

This workflow bootstraps a new Next.js project with the Zaitex branding, visual effects, and strict type safety settings.

## 1. Initialize Next.js Project
Run the standard Next.js setup with TypeScript, Tailwind, and App Router.
```bash
npx create-next-app@latest . --typescript --tailwind --eslint
```

## 2. Install Zaitex Core Stack
// turbo
Install the mandatory dependencies for visual effects and animations.
```bash
npm install framer-motion lenis lucide-react class-variance-authority clsx tailwind-merge three @react-three/fiber @react-three/drei gsap @gsap/react
npm install -D @types/three
```

## 3. Configure Design System
Set up the Active DNA in `app/globals.css` and `tailwind.config.ts`.
*(Refer to `.agent/design/active-dna.md` for tokens)*

## 4. Verify Build Environment
Ensure the environment is strict-mode compliant (checking for null canvas refs, etc).
```bash
npm run build
```
