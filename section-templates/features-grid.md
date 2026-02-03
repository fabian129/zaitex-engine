# Section Template: Features Grid

A responsive grid displaying multiple features/services with icons.

## When to Use
- Showcasing 3-6 features or services
- When each item has equal importance
- Explaining what you offer

## Layout Pattern
```
Desktop: 3 columns
Tablet:  2 columns
Mobile:  1 column
```

## Code Template

```tsx
"use client";

import { motion } from "framer-motion";
import { LucideIcon } from "lucide-react";
import { cn } from "@/lib/utils";

interface Feature {
  icon: LucideIcon;
  title: string;
  description: string;
}

interface FeaturesGridProps {
  headline?: string;
  subheadline?: string;
  features: Feature[];
  columns?: 2 | 3 | 4;
}

export function FeaturesGrid({
  headline,
  subheadline,
  features,
  columns = 3,
}: FeaturesGridProps) {
  const gridCols = {
    2: "md:grid-cols-2",
    3: "md:grid-cols-2 lg:grid-cols-3",
    4: "md:grid-cols-2 lg:grid-cols-4",
  };

  return (
    <section className="py-24 px-6 bg-background">
      <div className="max-w-6xl mx-auto">
        {/* Header */}
        {(headline || subheadline) && (
          <div className="text-center mb-16">
            {headline && (
              <h2 className="text-4xl md:text-5xl font-bold text-foreground mb-4">
                {headline}
              </h2>
            )}
            {subheadline && (
              <p className="text-xl text-secondary max-w-2xl mx-auto">
                {subheadline}
              </p>
            )}
          </div>
        )}

        {/* Grid */}
        <div className={cn("grid gap-8", gridCols[columns])}>
          {features.map((feature, index) => (
            <motion.div
              key={feature.title}
              initial={{ opacity: 0, y: 20 }}
              whileInView={{ opacity: 1, y: 0 }}
              viewport={{ once: true }}
              transition={{ delay: index * 0.1, duration: 0.5 }}
              className="group p-8 rounded-3xl bg-white border border-border/50 
                        hover:shadow-xl hover:shadow-primary/5 hover:-translate-y-1 
                        transition-all duration-300"
            >
              <div className="w-14 h-14 rounded-2xl bg-primary/10 flex items-center justify-center mb-6 
                            group-hover:bg-primary group-hover:text-white transition-colors">
                <feature.icon className="w-7 h-7 text-primary group-hover:text-white" />
              </div>
              <h3 className="text-xl font-bold text-foreground mb-3">
                {feature.title}
              </h3>
              <p className="text-secondary leading-relaxed">
                {feature.description}
              </p>
            </motion.div>
          ))}
        </div>
      </div>
    </section>
  );
}
```

## Usage Example

```tsx
import { Sparkles, Shield, Clock, CheckCircle } from "lucide-react";

<FeaturesGrid
  headline="Varför välja oss?"
  subheadline="Vi levererar kvalitet och trygghet i varje städning."
  features={[
    {
      icon: Sparkles,
      title: "Professionell Personal",
      description: "Utbildad och erfaren personal som tar hand om ditt hem.",
    },
    {
      icon: Shield,
      title: "Försäkrade & Certifierade",
      description: "Full försäkring och RUT-avdrag på alla våra tjänster.",
    },
    {
      icon: Clock,
      title: "Flexibla Tider",
      description: "Vi anpassar oss efter ditt schema, även helger.",
    },
    {
      icon: CheckCircle,
      title: "Nöjd-kund-garanti",
      description: "Inte nöjd? Vi kommer tillbaka och fixar det kostnadsfritt.",
    },
  ]}
/>
```

## Variations

### Minimal (No Cards)
```tsx
<div className="p-6 text-center">
  <feature.icon className="w-12 h-12 text-primary mx-auto mb-4" />
  <h3 className="font-bold mb-2">{feature.title}</h3>
  <p className="text-secondary text-sm">{feature.description}</p>
</div>
```

### With Background Pattern
```tsx
<section className="relative">
  <GridPattern className="absolute inset-0 opacity-5" />
  {/* content */}
</section>
```
