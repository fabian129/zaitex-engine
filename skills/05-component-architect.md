name: component-architect
description: Senior React Architect. Identifies complex UI patterns and extracts them into reusable, logic-separated components.
---

# Component Architect Logic

## 1. Objective
Prevent "Spaghetti Code" in page sections. When a UI element has complex state (`useState`, `useEffect`), intricate data mapping, or is reused across sections, you extract it into a dedicated "Zaitex Tool".

## 2. Trigger Conditions
Run this skill when `Section Builder` encounters:
- **Interactive Forms:** Multi-step wizards, calculators, complex inputs.
- **Data Collections:** Sortable tables, filtering grids, search bars.
- **Complex UI:** Carousels, Tabs, Accordions, Video Players with custom controls.
- **Repeated Patterns:** A specific card style used >3 times.

## 3. Architecture Rules (The "Zaitex Standard")

### A. Separation of Concerns
- **Layout (The Shell):** The `Section` component handles *positioning* (margin, padding, grid).
- **Logic (The Core):** The `Component` handles *internal state* and *rendering*.

### B. Props Interface
- Components must be "dumb" content receivers where possible.
- Use explicit TypeScript interfaces.
- Allow `className` override (merged via `cn()`).

### C. File Structure
- Simple UI atoms -> `components/ui/` (shadcn).
- Complex Zaitex Tools -> `components/zaitex/` (e.g., `components/zaitex/roi-calculator.tsx`).
- Sections -> `components/sections/` (e.g., `components/sections/pricing-calculator.tsx`).

## 4. Execution Protocol
1. **Identify**: "This Pricing Card has a 'Yearly/Monthly' toggle and logic."
2. **Extract**: Create `components/zaitex/pricing-toggle.tsx`.
3. **Refactor**: Update the original section to simply import `<PricingToggle />`.

## 5. Output Format
Output the standalone component file.

```tsx
// Example: components/zaitex/roi-calculator.tsx
"use client";
import { useState } from "react";
import { Slider } from "@/components/ui/slider";
import { Card } from "@/components/ui/card";

interface RoiCalculatorProps {
  baseRate: number;
}

export function RoiCalculator({ baseRate }: RoiCalculatorProps) {
  const [leads, setLeads] = useState(10);
  const total = leads * baseRate;

  return (
    <Card className="p-6 border-primary/20 bg-background/50">
      <h3 className="text-lg font-bold uppercase mb-4">Projected Revenue</h3>
      <div className="mb-8">
        <div className="text-4xl font-black tabular-nums">${total.toLocaleString()}</div>
        <div className="text-xs text-muted-foreground uppercase tracking-widest">Monthly Potential</div>
      </div>
      <Slider 
        value={[leads]} 
        onValueChange={(v) => setLeads(v[0])} 
        max={100} 
        step={1} 
        className="[&>.range]:bg-primary"
      />
      <div className="mt-2 text-xs font-medium text-right">{leads} Leads / Month</div>
    </Card>
  );
}
```
