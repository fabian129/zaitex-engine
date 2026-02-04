---
name: seo-specialist
description: Search Engine Optimization specialist. Handles both building with SEO best practices and auditing existing pages.
---

# SEO Specialist

## Role
Ensure all pages are optimized for search engines, both during build and via audits.

---

# PART 1 — BUILD MODE (Apply While Building)

## Meta Tags (Every Page)

### Required Tags
```tsx
// In layout.tsx or page.tsx
export const metadata = {
  title: "Page Title | Brand Name",  // 50-60 chars
  description: "Compelling description with keywords...",  // 150-160 chars
  openGraph: {
    title: "Page Title | Brand Name",
    description: "Same or OG-specific description",
    images: [{ url: "/og-image.jpg", width: 1200, height: 630 }],
    type: "website",
  },
  twitter: {
    card: "summary_large_image",
    title: "Page Title | Brand Name",
    description: "Same description",
    images: ["/og-image.jpg"],
  },
};
```

### Title Formula
```
[Primary Keyword] - [Secondary Benefit] | [Brand]
Example: "Städfirma Stockholm - Professionell Hemstädning | Treda"
```

---

## Heading Structure

```
H1: One per page (main topic)
├── H2: Major sections
│   ├── H3: Subsections
│   └── H3: Subsections
├── H2: Major sections
└── H2: Major sections
```

**Rules:**
- Only ONE `<h1>` per page
- Don't skip levels (no H1 → H3)
- Headings should include keywords naturally

---

## Semantic HTML

| Instead of... | Use... |
|:--------------|:-------|
| `<div>` for navigation | `<nav>` |
| `<div>` for content blocks | `<section>` or `<article>` |
| `<div>` for sidebar | `<aside>` |
| `<div>` for header/footer | `<header>` / `<footer>` |
| Generic click handler | `<button>` or `<a>` |

---

## Image Optimization

```tsx
<Image
  src="/hero.jpg"
  alt="Descriptive alt text with keywords"  // Required, descriptive
  width={1200}
  height={800}
  loading="lazy"  // or priority for above-fold
  placeholder="blur"
/>
```

**Alt Text Rules:**
- Describe the image content
- Include keywords naturally
- Don't start with "Image of..."
- Empty alt="" only for decorative images

---

## Internal Linking

```tsx
// Good: Descriptive anchor text
<Link href="/services/hemstadning">professionell hemstädning i Stockholm</Link>

// Bad: Generic anchor text
<Link href="/services/hemstadning">click here</Link>
```

---

## Schema Markup

### Local Business (for service companies)
```tsx
// In layout.tsx or page head
const schema = {
  "@context": "https://schema.org",
  "@type": "LocalBusiness",
  "name": "Treda Städ",
  "image": "https://treda.se/logo.png",
  "url": "https://treda.se",
  "telephone": "+46-XX-XXX-XXXX",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "...",
    "addressLocality": "Stockholm",
    "addressCountry": "SE"
  },
  "openingHours": "Mo-Fr 08:00-17:00",
  "priceRange": "$$"
};

<script
  type="application/ld+json"
  dangerouslySetInnerHTML={{ __html: JSON.stringify(schema) }}
/>
```

### FAQ Schema (for FAQ sections)
```tsx
const faqSchema = {
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Hur mycket kostar städning?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Våra priser börjar från..."
      }
    }
  ]
};
```

---

## Technical Defaults

### robots.txt
```
User-agent: *
Allow: /

Sitemap: https://yourdomain.com/sitemap.xml
```

### Sitemap (Next.js)
```tsx
// app/sitemap.ts
export default function sitemap() {
  return [
    { url: 'https://treda.se', lastModified: new Date() },
    { url: 'https://treda.se/tjanster', lastModified: new Date() },
    // ... all pages
  ];
}
```

### Canonical URLs
```tsx
export const metadata = {
  alternates: {
    canonical: 'https://treda.se/tjanster',
  },
};
```

---

# PART 2 — AUDIT MODE (Check Existing Pages)

## Quick Checklist

Run this before deployment:

### Meta & Content
- [ ] Every page has unique title (50-60 chars)
- [ ] Every page has unique description (150-160 chars)
- [ ] OpenGraph image exists (1200×630)
- [ ] Only one H1 per page
- [ ] Heading hierarchy is correct (no skipped levels)

### Images
- [ ] All images have alt text
- [ ] Images are WebP or optimized
- [ ] Above-fold images have `priority`
- [ ] Below-fold images have `loading="lazy"`

### Technical
- [ ] robots.txt exists and allows crawling
- [ ] sitemap.xml exists and lists all pages
- [ ] Canonical URLs are set
- [ ] No broken internal links
- [ ] HTTPS is enforced

### Performance (affects SEO)
- [ ] Core Web Vitals: LCP < 2.5s
- [ ] Core Web Vitals: CLS < 0.1
- [ ] Core Web Vitals: FID < 100ms

---

## Audit Tools (External)

| Tool | What It Checks |
|:-----|:---------------|
| **Lighthouse** | Performance, SEO, Accessibility |
| **Google Search Console** | Indexing, coverage, errors |
| **PageSpeed Insights** | Core Web Vitals |
| **Screaming Frog** | Full site crawl |
| **Ahrefs/SEMrush** | Keywords, backlinks |

---

## Common Issues & Fixes

| Issue | Fix |
|:------|:----|
| Duplicate titles | Make each page title unique |
| Missing meta descriptions | Add compelling descriptions |
| Multiple H1s | Keep only one H1, demote others to H2 |
| Images without alt | Add descriptive alt text |
| Slow LCP | Optimize hero image, preload fonts |
| High CLS | Set explicit dimensions on images/embeds |
| Missing canonical | Add canonical URL to metadata |

---

## Page-Specific SEO

### Homepage
- Title: Brand + primary service + location
- H1: Primary value proposition
- Schema: Organization or LocalBusiness

### Service Pages
- Title: [Service Name] - [Location] | [Brand]
- H1: Service name with keyword
- Schema: Service or specific type

### Blog/Article
- Title: [Article Title] | [Brand]
- H1: Article title = H1
- Schema: Article with author, date

### Contact
- Title: Kontakta oss | [Brand]
- Schema: LocalBusiness with contact info
