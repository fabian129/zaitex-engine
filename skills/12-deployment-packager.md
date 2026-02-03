name: deployment-packager
description: Production Launch Specialist. Prepares sites for deployment with environment setup, analytics integration, and deployment instructions.
---

# Deployment Packager Logic

## 1. Objective
You are a **DevOps Specialist**. Your job is to prepare a Next.js site for production deployment by:
- Creating environment variable templates
- Adding analytics tracking (GA4, Plausible, etc.)
- Setting up error monitoring (Sentry)
- Generating deployment instructions for Vercel/Netlify
- Creating a pre-launch checklist

## 2. Deliverables

### A. Environment Variables (`.env.example`)
```bash
# Site Configuration
NEXT_PUBLIC_SITE_URL=https://yourdomain.com
NEXT_PUBLIC_SITE_NAME="Your Site Name"

# Analytics
NEXT_PUBLIC_GA4_ID=G-XXXXXXXXXX
NEXT_PUBLIC_PLAUSIBLE_DOMAIN=yourdomain.com

# Error Tracking
NEXT_PUBLIC_SENTRY_DSN=https://xxx@xxx.ingest.sentry.io/xxx
SENTRY_AUTH_TOKEN=your_sentry_auth_token

# Contact Form (if using)
RESEND_API_KEY=re_xxxxxxxxxxxx
CONTACT_EMAIL=hello@yourdomain.com

# CMS (if using)
SANITY_PROJECT_ID=your_project_id
SANITY_DATASET=production
SANITY_API_TOKEN=your_api_token
```

### B. Google Analytics 4 Integration
**File:** `lib/analytics.ts`
```typescript
export const GA_TRACKING_ID = process.env.NEXT_PUBLIC_GA4_ID;

export const pageview = (url: string) => {
  if (typeof window.gtag !== 'undefined') {
    window.gtag('config', GA_TRACKING_ID!, {
      page_path: url,
    });
  }
};

export const event = ({ action, category, label, value }: {
  action: string;
  category: string;
  label: string;
  value?: number;
}) => {
  if (typeof window.gtag !== 'undefined') {
    window.gtag('event', action, {
      event_category: category,
      event_label: label,
      value: value,
    });
  }
};
```

**Add to `app/layout.tsx`:**
```tsx
import Script from 'next/script';

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <head>
        {process.env.NEXT_PUBLIC_GA4_ID && (
          <>
            <Script
              src={`https://www.googletagmanager.com/gtag/js?id=${process.env.NEXT_PUBLIC_GA4_ID}`}
              strategy="afterInteractive"
            />
            <Script id="google-analytics" strategy="afterInteractive">
              {`
                window.dataLayer = window.dataLayer || [];
                function gtag(){dataLayer.push(arguments);}
                gtag('js', new Date());
                gtag('config', '${process.env.NEXT_PUBLIC_GA4_ID}');
              `}
            </Script>
          </>
        )}
      </head>
      <body>{children}</body>
    </html>
  );
}
```

### C. Sentry Error Tracking
**Install:**
```bash
npm install @sentry/nextjs
```

**File:** `sentry.client.config.ts`
```typescript
import * as Sentry from "@sentry/nextjs";

Sentry.init({
  dsn: process.env.NEXT_PUBLIC_SENTRY_DSN,
  tracesSampleRate: 1.0,
  environment: process.env.NODE_ENV,
});
```

**File:** `sentry.server.config.ts`
```typescript
import * as Sentry from "@sentry/nextjs";

Sentry.init({
  dsn: process.env.NEXT_PUBLIC_SENTRY_DSN,
  tracesSampleRate: 1.0,
  environment: process.env.NODE_ENV,
});
```

### D. Deployment Instructions (`DEPLOYMENT.md`)
```markdown
# Deployment Guide

## Vercel Deployment (Recommended)

### 1. Prerequisites
- GitHub repository with code pushed
- Vercel account (free tier works)

### 2. Deploy Steps
1. Go to [vercel.com](https://vercel.com)
2. Click "Import Project"
3. Select your GitHub repository
4. Configure environment variables (see below)
5. Click "Deploy"

### 3. Environment Variables
Add these in Vercel Dashboard → Settings → Environment Variables:

| Variable | Value | Notes |
|----------|-------|-------|
| `NEXT_PUBLIC_SITE_URL` | `https://yourdomain.com` | Your production URL |
| `NEXT_PUBLIC_GA4_ID` | `G-XXXXXXXXXX` | From Google Analytics |
| `NEXT_PUBLIC_SENTRY_DSN` | `https://xxx@xxx.ingest.sentry.io/xxx` | From Sentry dashboard |

### 4. Custom Domain
1. Go to Vercel Dashboard → Settings → Domains
2. Add your domain (e.g., `yourdomain.com`)
3. Update DNS records as instructed
4. Wait for SSL certificate (automatic)

### 5. Post-Deployment
- [ ] Test site at Vercel URL
- [ ] Verify analytics tracking
- [ ] Check error monitoring in Sentry
- [ ] Submit sitemap to Google Search Console
- [ ] Test on mobile devices

## Netlify Deployment (Alternative)

### 1. Deploy Steps
1. Go to [netlify.com](https://netlify.com)
2. Click "Add new site" → "Import an existing project"
3. Connect GitHub repository
4. Build settings:
   - Build command: `npm run build`
   - Publish directory: `.next`
5. Add environment variables
6. Click "Deploy"

### 2. Environment Variables
Same as Vercel (see above)

## Manual Deployment (VPS/Server)

### 1. Build Production Bundle
```bash
npm run build
npm start
```

### 2. Process Manager (PM2)
```bash
npm install -g pm2
pm2 start npm --name "yoursite" -- start
pm2 save
pm2 startup
```

### 3. Nginx Reverse Proxy
```nginx
server {
    listen 80;
    server_name yourdomain.com;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```
```

## 3. Pre-Launch Checklist

Generate `PRE_LAUNCH_CHECKLIST.md`:

```markdown
# Pre-Launch Checklist

## Technical
- [ ] Production build succeeds (`npm run build`)
- [ ] All environment variables set
- [ ] SSL certificate active (HTTPS)
- [ ] Custom domain configured
- [ ] Sitemap submitted to Google Search Console
- [ ] robots.txt configured correctly
- [ ] 404 page exists and styled
- [ ] Favicon and app icons added

## Performance
- [ ] Lighthouse score > 90
- [ ] Images optimized (WebP format)
- [ ] Core Web Vitals passing (LCP < 2.5s, FID < 100ms, CLS < 0.1)
- [ ] No console errors in production

## SEO
- [ ] Meta tags on all pages
- [ ] Open Graph images created (1200x630px)
- [ ] Structured data validated (Google Rich Results Test)
- [ ] Alt text on all images
- [ ] Canonical URLs set

## Accessibility
- [ ] WCAG 2.1 AA compliance verified
- [ ] Keyboard navigation tested
- [ ] Screen reader tested (NVDA or JAWS)
- [ ] Color contrast ratios pass (4.5:1 minimum)

## Analytics & Monitoring
- [ ] Google Analytics 4 tracking verified
- [ ] Sentry error tracking active
- [ ] Conversion goals configured (if applicable)
- [ ] Uptime monitoring set up (e.g., UptimeRobot)

## Legal & Compliance
- [ ] Privacy policy page added
- [ ] Cookie consent banner (if GDPR required)
- [ ] Terms of service page (if applicable)
- [ ] Contact information accurate

## Content
- [ ] All placeholder text replaced
- [ ] All images have proper alt text
- [ ] Contact form tested and working
- [ ] Social media links correct
- [ ] Copyright year current

## Testing
- [ ] Tested on Chrome, Safari, Firefox, Edge
- [ ] Tested on mobile (iOS and Android)
- [ ] Tested on tablet
- [ ] All links work (no 404s)
- [ ] Forms submit correctly
- [ ] Email notifications working (if applicable)

## Backup & Security
- [ ] Database backup configured (if applicable)
- [ ] Environment variables secured (not in Git)
- [ ] API keys rotated (if needed)
- [ ] Rate limiting configured (if applicable)

## Client Handoff
- [ ] Admin credentials provided (if CMS)
- [ ] Analytics access granted
- [ ] DNS management instructions provided
- [ ] Maintenance plan discussed
```

## 4. Integration with Existing Skills

### A. SEO Optimizer
- **Input:** SEO Optimizer generates sitemap and meta tags
- **Output:** Deployment Packager ensures they're deployed correctly

### B. Accessibility Validator
- **Input:** Validator confirms WCAG compliance
- **Output:** Deployment Packager adds it to pre-launch checklist

### C. Brief Interpreter
- **Input:** Client brief specifies required integrations (GA4, HubSpot)
- **Output:** Deployment Packager adds them to environment variables

## 5. Output Files

When run, Deployment Packager creates:
1. `.env.example` - Environment variable template
2. `lib/analytics.ts` - Analytics helper functions
3. `DEPLOYMENT.md` - Step-by-step deployment guide
4. `PRE_LAUNCH_CHECKLIST.md` - Comprehensive launch checklist
5. `sentry.client.config.ts` - Error tracking setup
6. `sentry.server.config.ts` - Server-side error tracking

## 6. Example Usage

**User Request:**
> "Prepare this site for deployment to Vercel with Google Analytics"

**Deployment Packager Output:**
1. Creates `.env.example` with GA4 variable
2. Adds analytics code to `layout.tsx`
3. Generates `DEPLOYMENT.md` with Vercel instructions
4. Creates `PRE_LAUNCH_CHECKLIST.md`

**Result:** Site is deployment-ready in 5 minutes
