# Claude Code: SEO & Metadata Implementation Guide

## Pawgress Landing Page — Next.js (JavaScript, App Router)

> **For Claude Code:** Follow every step in order. Do not skip sections. All code is JavaScript — do not use TypeScript. Do not add type annotations. Confirm each file exists before editing. Ask before overwriting existing metadata.

---

## Before You Start

1. Confirm this project uses the **Next.js App Router** (`app/` directory exists).
2. Confirm `app/layout.js` exists. If not, check for `app/layout.jsx` — treat them the same.
3. Confirm `app/page.js` (or `.jsx`) exists. This is where JSON-LD goes.
4. Confirm `public/` directory exists. The OG image goes here.
5. Confirm `package.json` lists `next` as a dependency.

If any of these are missing, stop and report to the user before proceeding.

---

## Step 1 — Add `og-image.png` to Public Directory

Copy the OG image file (`og-image.png`) into the `public/` directory.

- Required dimensions: **1200 × 630px**
- File name must be exactly: `og-image.png`
- Path after copy: `public/og-image.png`
- This file will be served at `https://pawgress.io/og-image.png`

If the file already exists, ask the user before replacing it.
If the file doesn't exist, move to the next step.

---

## Step 2 — Add Metadata to `app/layout.js`

Open `app/layout.js`. Find the existing metadata export (if any). **Replace it entirely** with the block below, or add it if none exists.

The metadata export must be at the **top level** of the file, outside any component function.

```js
export const metadata = {
  metadataBase: new URL("https://pawgress.io"),

  title: "Pawgress — Client Management Software for Dog Trainers",
  description:
    "Manage clients, track session progress, and grow your dog training business — all in one place. Join the waitlist. 14-day free trial.",

  keywords: [
    "dog trainer software",
    "dog training client management",
    "dog trainer app",
    "dog trainer CRM",
    "dog training progress tracking",
    "dog training session notes",
    "client management for dog trainers",
  ],

  alternates: {
    canonical: "https://pawgress.io",
  },

  openGraph: {
    type: "website",
    url: "https://pawgress.io",
    siteName: "Pawgress",
    title: "Pawgress — Client Management Software for Dog Trainers",
    description:
      "Manage clients, track session progress, and grow your dog training business — all in one place.",
    images: [
      {
        url: "/og-image.png",
        width: 1200,
        height: 630,
        alt: "Pawgress — Dog Trainer Client Management Software",
      },
    ],
    locale: "en_US",
  },

  twitter: {
    card: "summary_large_image",
    site: "@getpawgress",
    creator: "@getpawgress",
    title: "Pawgress — Client Management Software for Dog Trainers",
    description:
      "Manage clients, track session progress, and grow your dog training business — all in one place.",
    images: ["/og-image.png"],
  },

  robots: {
    index: true,
    follow: true,
    googleBot: {
      index: true,
      follow: true,
      "max-image-preview": "large",
      "max-snippet": -1,
    },
  },
};
```

### Critical Notes for This Step

- `metadataBase` is **required**. Without it, Next.js cannot resolve `/og-image.png` to a full URL in Open Graph and Twitter tags. Social previews will be broken without it.
- Do NOT put the metadata export inside the default exported component function — it must be a separate named export.
- If the layout already imports `metadata` from somewhere else, consolidate into a single export. Do not have two `metadata` exports.

---

## Step 3 — Add JSON-LD Structured Data to `app/page.js`

Open `app/page.js`. Find the default exported component (usually `export default function Home()`).

Add the two JSON-LD `<script>` tags as the **first children** inside the returned JSX, before any other content. If the component returns a `<main>` or `<div>` wrapper, put the scripts inside it.

```js
export default function Home() {
  const softwareApplicationSchema = {
    "@context": "https://schema.org",
    "@type": "SoftwareApplication",
    name: "Pawgress",
    applicationCategory: "BusinessApplication",
    operatingSystem: "Web",
    url: "https://pawgress.io",
    description:
      "Client management software for professional dog trainers. Manage clients, dogs, sessions, progress tracking, training roadmaps, and homework — all in one place.",
    offers: [
      {
        "@type": "Offer",
        name: "Basic",
        price: "20.00",
        priceCurrency: "USD",
      },
      {
        "@type": "Offer",
        name: "Pro",
        price: "35.00",
        priceCurrency: "USD",
      },
      {
        "@type": "Offer",
        name: "Unlimited",
        price: "60.00",
        priceCurrency: "USD",
      },
    ],
    featureList: [
      "Client management",
      "Dog profiles",
      "Session tracking with scores",
      "Homework assignment",
      "Training roadmaps",
      "Goal tracking",
      "Google Calendar sync",
      "Payment overview",
    ],
    screenshot: "https://pawgress.io/og-image.png",
  };

  const organizationSchema = {
    "@context": "https://schema.org",
    "@type": "Organization",
    name: "Pawgress",
    url: "https://pawgress.io",
    logo: "https://pawgress.io/logo.png",
    sameAs: ["https://www.instagram.com/getpawgress"],
    description:
      "Pawgress builds client management software for professional dog trainers.",
  };

  return (
    <>
      <script
        type="application/ld+json"
        dangerouslySetInnerHTML={{
          __html: JSON.stringify(softwareApplicationSchema),
        }}
      />
      <script
        type="application/ld+json"
        dangerouslySetInnerHTML={{ __html: JSON.stringify(organizationSchema) }}
      />
      {/* existing page content goes here — do not remove or replace it */}
    </>
  );
}
```

### Critical Notes for This Step

- `app/page.js` must be a **Server Component** (no `'use client'` directive at the top). JSON-LD in a client component may not be rendered server-side and will be invisible to search crawlers. If `'use client'` is present on this file, move the JSON-LD into a new server component file (see Fallback below).
- Do not alter or remove any existing JSX content in this file. The JSON-LD scripts are purely additive.
- The `dangerouslySetInnerHTML` pattern is correct and safe here — the schema data is hardcoded, not user input.

#### Fallback: If `app/page.js` has `'use client'`

Create a new file `app/seo-schemas.js` (no `'use client'` directive):

```js
const softwareApplicationSchema = {
  "@context": "https://schema.org",
  "@type": "SoftwareApplication",
  name: "Pawgress",
  applicationCategory: "BusinessApplication",
  operatingSystem: "Web",
  url: "https://pawgress.io",
  description:
    "Client management software for professional dog trainers. Manage clients, dogs, sessions, progress tracking, training roadmaps, and homework — all in one place.",
  offers: [
    { "@type": "Offer", name: "Basic", price: "20.00", priceCurrency: "USD" },
    { "@type": "Offer", name: "Pro", price: "35.00", priceCurrency: "USD" },
    {
      "@type": "Offer",
      name: "Unlimited",
      price: "60.00",
      priceCurrency: "USD",
    },
  ],
  featureList: [
    "Client management",
    "Dog profiles",
    "Session tracking with scores",
    "Homework assignment",
    "Training roadmaps",
    "Goal tracking",
    "Google Calendar sync",
    "Payment overview",
  ],
  screenshot: "https://pawgress.io/og-image.png",
};

const organizationSchema = {
  "@context": "https://schema.org",
  "@type": "Organization",
  name: "Pawgress",
  url: "https://pawgress.io",
  logo: "https://pawgress.io/logo.png",
  sameAs: ["https://www.instagram.com/getpawgress"],
  description:
    "Pawgress builds client management software for professional dog trainers.",
};

export default function SeoSchemas() {
  return (
    <>
      <script
        type="application/ld+json"
        dangerouslySetInnerHTML={{
          __html: JSON.stringify(softwareApplicationSchema),
        }}
      />
      <script
        type="application/ld+json"
        dangerouslySetInnerHTML={{ __html: JSON.stringify(organizationSchema) }}
      />
    </>
  );
}
```

Then import and render `<SeoSchemas />` in `app/layout.js` (which is always a server component) before the `{children}` slot.

---

## Step 4 — Create `app/robots.js`

Check if `app/robots.js` already exists. If it does, read it first and confirm with the user before overwriting.

If it does not exist, create it:

```js
export default function robots() {
  return {
    rules: {
      userAgent: "*",
      allow: "/",
    },
    sitemap: "https://pawgress.io/sitemap.xml",
  };
}
```

No imports needed — Next.js handles this automatically.

---

## Step 5 — Create `app/sitemap.js`

Check if `app/sitemap.js` already exists. If it does, read it first and confirm with the user before overwriting.

If it does not exist, create it:

```js
export default function sitemap() {
  return [
    {
      url: "https://pawgress.io",
      lastModified: new Date(),
      changeFrequency: "monthly",
      priority: 1,
    },
  ];
}
```

As new pages are added to the site (e.g., `/pricing`, `/features`, `/blog`), add them to this array with appropriate `priority` values (0.1–1.0) and `changeFrequency` strings.

---

## Step 6 — Verify the H1 on the Landing Page

Open `app/page.js` and find the main `<h1>` tag. It should read exactly:

```
The Client Management App Built for Dog Trainers
```

If the H1 is missing, add it as the first visible heading in the page content. If it says something different, propose the change to the user — do not replace it without confirmation. The H1 must be unique on the page (only one `<h1>` per page).

---

## Step 7 — Verify `next/image` is Used for Above-the-Fold Images

In `app/page.js`, find any `<img>` tags that appear above the fold (hero section). Replace them with `next/image`:

```js
import Image from "next/image";

// Replace:
// <img src="/hero.png" alt="..." />

// With:
<Image
  src="/hero.png"
  alt="Pawgress dashboard — dog trainer client management"
  width={1200}
  height={800}
  priority
/>;
```

- The `priority` prop is required on above-fold images. It disables lazy loading and tells Next.js to preload the image, improving Largest Contentful Paint (LCP).
- Always include explicit `width` and `height` to prevent Cumulative Layout Shift (CLS).
- Alt text should be descriptive and naturally include the keyword "dog trainer" where appropriate.

---

## File Checklist

After completing all steps, confirm these files exist and are non-empty:

| File                  | Purpose                                                      | Required |
| --------------------- | ------------------------------------------------------------ | -------- |
| `app/layout.js`       | Metadata export (title, description, OG, Twitter, robots)    | Yes      |
| `app/page.js`         | JSON-LD structured data (SoftwareApplication + Organization) | Yes      |
| `app/robots.js`       | Crawl rules + sitemap reference                              | Yes      |
| `app/sitemap.js`      | URL list for Google indexing                                 | Yes      |
| `public/og-image.png` | Social share image (1200×630px)                              | Yes      |

---

## How to Test

Run these checks before marking implementation complete:

**1. Local metadata preview**

```bash
npm run build && npm run start
```

Open `http://localhost:3000` and view page source (`Ctrl+U`). Confirm:

- `<title>` tag matches exactly
- `<meta name="description">` is present
- `<meta property="og:image">` resolves to a full URL (not a relative path)
- Two `<script type="application/ld+json">` tags are present

**2. Robots and sitemap**

- Visit `http://localhost:3000/robots.txt` — should show allow rules and sitemap URL
- Visit `http://localhost:3000/sitemap.xml` — should show pawgress.io URL with lastmod date

**3. Structured data validation**

- Copy the JSON-LD content from page source
- Paste into [Google Rich Results Test](https://search.google.com/test/rich-results)
- Confirm `SoftwareApplication` and `Organization` entities are detected with no errors

**4. Open Graph preview**

- Use [opengraph.xyz](https://www.opengraph.xyz) with `https://pawgress.io` to verify OG image and text render correctly
- Twitter preview: use [cards-dev.twitter.com/validator](https://cards-dev.twitter.com/validator)

---

## Post-Launch: Google Search Console

Once the site is live at `https://pawgress.io`:

1. Add property in [Google Search Console](https://search.google.com/search-console)
2. Verify ownership via the HTML tag method (add to `<head>` in `app/layout.js` metadata under `verification.google`)
3. Submit sitemap: `https://pawgress.io/sitemap.xml`
4. Request indexing for the homepage URL

To add GSC verification to metadata:

```js
export const metadata = {
  // ... all existing fields ...
  verification: {
    google: "PASTE_YOUR_VERIFICATION_CODE_HERE",
  },
};
```

---

## What NOT to Do

- Do not use TypeScript (`.ts`, `.tsx`) — all files must be `.js` or `.jsx`
- Do not add `'use client'` to `app/layout.js` or `app/page.js` unless they already have it
- Do not put the `metadata` export inside a component function
- Do not use `<Head>` from `next/head` — that is the Pages Router pattern; this project uses App Router
- Do not keyword-stuff — the metadata values above are final; do not add more keywords to title or description
- Do not create a separate `_document.js` — App Router does not use this file
