# Section Template: Hero Split

A two-column hero with text on one side and visual on the other.

## When to Use
- Need balance between text content and visual
- Homepage or landing pages
- When you have a strong hero image or 3D element

## Layout Pattern
```
Desktop: [Text 50%] | [Visual 50%]
Mobile:  [Visual] → [Text] (stacked)
```

## Code Template

```tsx
"use client";

import { motion } from "framer-motion";
import Image from "next/image";
import { Button } from "@/components/ui/button";
import { ArrowRight } from "lucide-react";

interface HeroSplitProps {
  headline: string;
  subheadline: string;
  ctaText: string;
  ctaHref: string;
  imageSrc: string;
  imageAlt: string;
}

export function HeroSplit({
  headline,
  subheadline,
  ctaText,
  ctaHref,
  imageSrc,
  imageAlt,
}: HeroSplitProps) {
  return (
    <section className="min-h-screen grid lg:grid-cols-2 gap-12 items-center px-6 py-20">
      {/* Text Side */}
      <motion.div
        initial={{ opacity: 0, x: -30 }}
        animate={{ opacity: 1, x: 0 }}
        transition={{ duration: 0.6 }}
        className="max-w-xl"
      >
        <h1 className="text-5xl md:text-6xl lg:text-7xl font-bold text-foreground leading-tight mb-6">
          {headline}
        </h1>
        <p className="text-xl text-secondary mb-8 leading-relaxed">
          {subheadline}
        </p>
        <Button size="lg" asChild>
          <a href={ctaHref}>
            {ctaText} <ArrowRight className="ml-2 w-5 h-5" />
          </a>
        </Button>
      </motion.div>

      {/* Visual Side */}
      <motion.div
        initial={{ opacity: 0, x: 30 }}
        animate={{ opacity: 1, x: 0 }}
        transition={{ duration: 0.6, delay: 0.2 }}
        className="relative h-[500px] lg:h-[600px] rounded-3xl overflow-hidden"
      >
        <Image
          src={imageSrc}
          alt={imageAlt}
          fill
          sizes="(max-width: 1024px) 100vw, 50vw"
          className="object-cover"
          priority
        />
      </motion.div>
    </section>
  );
}
```

## Usage Example

```tsx
<HeroSplit
  headline="Vi skapar rent och trivsamt"
  subheadline="Professionell städning för hem och företag i Malmö."
  ctaText="Boka Städning"
  ctaHref="/kontakt"
  imageSrc="/images/hero.jpg"
  imageAlt="Clean modern living room"
/>
```

## Customization Points

| Prop | Type | Notes |
|:-----|:-----|:------|
| `headline` | string | Main attention grabber |
| `subheadline` | string | Supporting benefit |
| `ctaText` | string | Action verb (e.g., "Get Started") |
| `ctaHref` | string | Link destination |
| `imageSrc` | string | Path to hero image |
| `imageAlt` | string | Descriptive alt text |

## Background Variations

```tsx
// With gradient overlay
<div className="absolute inset-0 bg-gradient-to-r from-background via-background/80 to-transparent" />

// With pattern
<GridPattern className="absolute inset-0 opacity-10" />

// With blobs
<OrganicBlob className="absolute -top-32 -left-32" variant="primary" />
```
