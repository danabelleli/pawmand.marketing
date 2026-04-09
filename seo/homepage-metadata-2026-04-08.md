# Pawgress Homepage SEO & Metadata Report
**Date:** 2026-04-08
**Scope:** Landing page (pawgress.io) — Next.js App Router metadata implementation

---

## Summary

Pawgress is entering a niche (dog trainer business software) with low direct competition and strong commercial intent. The primary SEO opportunity right now is owning the keywords "dog trainer software" and "dog training client management" before launch — establishing domain authority early is critical since BarkBook currently holds the top positions for booking-related terms. The homepage metadata should clearly signal product category, audience specificity, and the waitlist CTA, while structured data helps Google classify Pawgress as a SoftwareApplication from day one.

---

## Keyword Strategy

### Primary Keywords (Homepage Targeting)

| Keyword | Est. Monthly Volume | Difficulty | Intent | Priority |
|---|---|---|---|---|
| dog trainer software | 1,000–2,000 | Low–Medium | Commercial | **Primary** |
| dog training client management | 200–500 | Low | Commercial | **Primary** |
| dog trainer app | 500–1,000 | Low–Medium | Commercial | **Primary** |
| client management for dog trainers | 100–300 | Low | Commercial | High |
| dog trainer CRM | 200–500 | Low | Commercial | High |

### Secondary Keywords (Support via copy)

| Keyword | Est. Monthly Volume | Difficulty | Intent |
|---|---|---|---|
| dog training business software | 100–300 | Low | Commercial |
| dog training management software | 100–200 | Low | Commercial |
| dog training session notes | 100–300 | Low | Informational |
| dog trainer business tools | 100–200 | Low | Commercial |
| dog training progress tracking | 200–500 | Low | Informational/Commercial |

> All volumes are estimated — verify with Ahrefs or Semrush before final prioritization.

### Competitor Gap: BarkBook
BarkBook ranks for scheduling/booking terms. They are weak on:
- "dog training progress tracking software"
- "dog trainer session notes"
- "dog training homework tracking"
- "training roadmap for dogs"

These are Pawgress differentiators — use them in copy and H2s.

---

## On-Page Metadata

### Title Tag
```
Pawgress — Client Management Software for Dog Trainers
```
- **Character count:** 55 (under 60 limit ✓)
- **Why:** Leads with brand, names the product category, immediately targets the audience. "Dog Trainers" as the final phrase reinforces audience specificity for Google.

### Meta Description
```
Manage clients, track session progress, and grow your dog training business — all in one place. Join the waitlist. 14-day free trial.
```
- **Character count:** 133 (under 155 limit ✓)
- **Why:** Uses primary keyword cluster naturally, addresses the core pain point (all in one place), and includes a clear CTA + trust signal (free trial).

### H1 Recommendation (landing page copy, not metadata)
```
The Client Management App Built for Dog Trainers
```
Complements the title tag without duplicating it.

---

## Next.js Implementation

### `app/layout.tsx` — Static Metadata Export

```typescript
import type { Metadata } from 'next';

export const metadata: Metadata = {
  metadataBase: new URL('https://pawgress.io'),

  title: 'Pawgress — Client Management Software for Dog Trainers',
  description:
    'Manage clients, track session progress, and grow your dog training business — all in one place. Join the waitlist. 14-day free trial.',

  keywords: [
    'dog trainer software',
    'dog training client management',
    'dog trainer app',
    'dog trainer CRM',
    'dog training progress tracking',
    'dog training session notes',
    'client management for dog trainers',
  ],

  alternates: {
    canonical: 'https://pawgress.io',
  },

  openGraph: {
    type: 'website',
    url: 'https://pawgress.io',
    siteName: 'Pawgress',
    title: 'Pawgress — Client Management Software for Dog Trainers',
    description:
      'Manage clients, track session progress, and grow your dog training business — all in one place.',
    images: [
      {
        url: '/og-image.png', // resolves to https://pawgress.io/og-image.png via metadataBase
        width: 1200,
        height: 630,
        alt: 'Pawgress — Dog Trainer Client Management Software',
      },
    ],
    locale: 'en_US',
  },

  twitter: {
    card: 'summary_large_image',
    site: '@getpawgress',
    creator: '@getpawgress',
    title: 'Pawgress — Client Management Software for Dog Trainers',
    description:
      'Manage clients, track session progress, and grow your dog training business — all in one place.',
    images: ['/og-image.png'], // resolves via metadataBase
  },

  robots: {
    index: true,
    follow: true,
    googleBot: {
      index: true,
      follow: true,
      'max-image-preview': 'large',
      'max-snippet': -1,
    },
  },
};
```

---

### JSON-LD Structured Data — `app/page.tsx`

Add this as a server component alongside your page content. Do NOT put it in a client component.

```tsx
// app/page.tsx (Server Component)

export default function HomePage() {
  const softwareApplicationSchema = {
    '@context': 'https://schema.org',
    '@type': 'SoftwareApplication',
    name: 'Pawgress',
    applicationCategory: 'BusinessApplication',
    operatingSystem: 'Web',
    url: 'https://pawgress.io',
    description:
      'Client management software for professional dog trainers. Manage clients, dogs, sessions, progress tracking, training roadmaps, and homework — all in one place.',
    offers: [
      {
        '@type': 'Offer',
        name: 'Basic',
        price: '20.00',
        priceCurrency: 'USD',
        priceSpecification: {
          '@type': 'UnitPriceSpecification',
          billingIncrement: 1,
          unitCode: 'MON',
          priceType: 'https://schema.org/RecurringChargeSpecification',
        },
      },
      {
        '@type': 'Offer',
        name: 'Pro',
        price: '35.00',
        priceCurrency: 'USD',
        priceSpecification: {
          '@type': 'UnitPriceSpecification',
          billingIncrement: 1,
          unitCode: 'MON',
          priceType: 'https://schema.org/RecurringChargeSpecification',
        },
      },
      {
        '@type': 'Offer',
        name: 'Unlimited',
        price: '60.00',
        priceCurrency: 'USD',
        priceSpecification: {
          '@type': 'UnitPriceSpecification',
          billingIncrement: 1,
          unitCode: 'MON',
          priceType: 'https://schema.org/RecurringChargeSpecification',
        },
      },
    ],
    featureList: [
      'Client management',
      'Dog profiles',
      'Session tracking with scores',
      'Homework assignment',
      'Training roadmaps',
      'Goal tracking',
      'Google Calendar sync',
      'Payment overview',
    ],
    screenshot: 'https://pawgress.io/og-image.png',
  };

  const organizationSchema = {
    '@context': 'https://schema.org',
    '@type': 'Organization',
    name: 'Pawgress',
    url: 'https://pawgress.io',
    logo: 'https://pawgress.io/logo.png',
    sameAs: ['https://www.instagram.com/getpawgress'],
    description:
      'Pawgress builds client management software for professional dog trainers.',
  };

  return (
    <>
      <script
        type="application/ld+json"
        dangerouslySetInnerHTML={{ __html: JSON.stringify(softwareApplicationSchema) }}
      />
      <script
        type="application/ld+json"
        dangerouslySetInnerHTML={{ __html: JSON.stringify(organizationSchema) }}
      />
      {/* rest of your page JSX */}
    </>
  );
}
```

---

### `app/robots.ts`

```typescript
import type { MetadataRoute } from 'next';

export default function robots(): MetadataRoute.Robots {
  return {
    rules: {
      userAgent: '*',
      allow: '/',
    },
    sitemap: 'https://pawgress.io/sitemap.xml',
  };
}
```

### `app/sitemap.ts`

```typescript
import type { MetadataRoute } from 'next';

export default function sitemap(): MetadataRoute.Sitemap {
  return [
    {
      url: 'https://pawgress.io',
      lastModified: new Date(),
      changeFrequency: 'monthly',
      priority: 1,
    },
  ];
}
```

---

## OG Image Spec

Create `/public/og-image.png` at **1200 × 630px** with:
- Pawgress logo + tagline ("Train. Track. Grow.")
- A clean product screenshot or abstract visual
- Brand colors (warm, professional palette per brand style guide)
- No text smaller than 24px (must be readable in link previews)

Test with: [Facebook Sharing Debugger](https://developers.facebook.com/tools/debug/) and [Twitter Card Validator](https://cards-dev.twitter.com/validator)

---

## Quick Wins (Under 1 Hour Each)

1. **Add `metadataBase`** — required for Next.js to resolve relative OG image URLs. Without it, social previews break.
2. **Create `og-image.png`** — single highest-ROI visual asset for social sharing and link previews.
3. **Add `app/robots.ts`** — one file, tells crawlers to index everything, submits sitemap reference.
4. **Add `app/sitemap.ts`** — submittable to Google Search Console immediately for faster indexing.
5. **Submit sitemap to Google Search Console** — free, takes 5 minutes, accelerates initial indexing.

---

## Implementation Notes

- `metadataBase: new URL('https://pawgress.io')` is **required** in the root layout for Next.js to correctly resolve `/og-image.png` to an absolute URL in all metadata fields.
- JSON-LD `<script>` tags must live in **Server Components** only — do not add them inside `'use client'` components or they may not be rendered server-side and will be invisible to crawlers.
- The `keywords` metadata field has minimal direct ranking value in 2026 but is harmless and useful for internal reference — keep the list tight and relevant.
- Prices in `SoftwareApplication` schema reflect the annual billing rate (lowest price) — update these if pricing changes.
- `logo.png` referenced in Organization schema needs to exist at `public/logo.png`.

---

## What to Verify in Code

These recommendations assume standard Next.js App Router setup. Confirm before implementing:
- [ ] App Router is in use (`app/` directory, not `pages/`)
- [ ] Root `layout.tsx` exists and accepts metadata exports
- [ ] `public/` directory is served at the root URL
- [ ] No existing `metadata` export conflicts with the one above
