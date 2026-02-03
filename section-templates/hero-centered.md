# Section Template: Hero Centered

A full-width centered hero with focus on a single strong message.

## When to Use
- Single powerful message
- Minimal content, maximum impact
- When the message is more important than visuals

## Layout Pattern
```
[Centered Content]
  - Badge/Label
  - Headline
  - Subheadline
  - CTA Buttons

[Background: Full-screen image or gradient]
```

## Code Template

```tsx
"use client";

import { motion } from "framer-motion";
import Image from "next/image";
import { Button } from "@/components/ui/button";
import { ArrowRight, Sparkles } from "lucide-react";

interface HeroCenteredProps {
  badge?: string;
  headline: string;
  subheadline: string;
  primaryCta: { text: string; href: string };
  secondaryCta?: { text: string; href: string };
  backgroundImage?: string;
}

export function HeroCentered({
  badge,
  headline,
  subheadline,
  primaryCta,
  secondaryCta,
  backgroundImage,
}: HeroCenteredProps) {
  return (
    <section className="relative min-h-screen flex items-center justify-center px-6 py-20">
      {/* Background */}
      {backgroundImage && (
        <div className="absolute inset-0">
          <Image
            src={backgroundImage}
            alt=""
            fill
            sizes="100vw"
            className="object-cover"
            priority
          />
          <div className="absolute inset-0 bg-black/50" />
        </div>
      )}

      {/* Content */}
      <motion.div
        initial={{ opacity: 0, y: 30 }}
        animate={{ opacity: 1, y: 0 }}
        transition={{ duration: 0.6 }}
        className="relative z-10 text-center max-w-4xl mx-auto"
      >
        {badge && (
          <motion.div
            initial={{ opacity: 0, scale: 0.9 }}
            animate={{ opacity: 1, scale: 1 }}
            transition={{ delay: 0.2 }}
            className="inline-flex items-center gap-2 px-4 py-2 rounded-full bg-primary/10 text-primary text-sm font-medium mb-6"
          >
            <Sparkles className="w-4 h-4" />
            {badge}
          </motion.div>
        )}

        <h1 className="text-5xl md:text-6xl lg:text-7xl font-bold text-white leading-tight mb-6">
          {headline}
        </h1>

        <p className="text-xl md:text-2xl text-white/80 mb-10 max-w-2xl mx-auto leading-relaxed">
          {subheadline}
        </p>

        <div className="flex flex-col sm:flex-row gap-4 justify-center">
          <Button size="lg" asChild>
            <a href={primaryCta.href}>
              {primaryCta.text} <ArrowRight className="ml-2 w-5 h-5" />
            </a>
          </Button>
          {secondaryCta && (
            <Button size="lg" variant="outline" asChild>
              <a href={secondaryCta.href}>{secondaryCta.text}</a>
            </Button>
          )}
        </div>
      </motion.div>
    </section>
  );
}
```

## Usage Example

```tsx
<HeroCentered
  badge="Nyhet"
  headline="Professionell städning för alla"
  subheadline="Vi tar hand om ditt hem så att du kan fokusera på det som betyder mest."
  primaryCta={{ text: "Boka Nu", href: "/kontakt" }}
  secondaryCta={{ text: "Läs Mer", href: "#services" }}
  backgroundImage="/images/hero-bg.jpg"
/>
```

## Variations

### Without Background Image (Gradient)
```tsx
<section className="bg-gradient-to-br from-primary/5 via-background to-background">
  {/* content */}
</section>
```

### With Video Background
```tsx
<video 
  autoPlay 
  muted 
  loop 
  playsInline 
  className="absolute inset-0 w-full h-full object-cover"
>
  <source src="/videos/hero.mp4" type="video/mp4" />
</video>
```

### Dark Text (Light Background)
Change `text-white` to `text-foreground` and `text-white/80` to `text-secondary`.
