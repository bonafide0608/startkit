# Next.js 16 Project Setup

## Tech Stack
- **Framework**: Next.js 16.2.4 (App Router, not Pages Router)
- **Runtime**: React 19.2.4 with Server Components by default
- **Language**: TypeScript 5 (strict mode enabled)
- **Styling**: Tailwind CSS 4 with @tailwindcss/postcss plugin
- **Components**: shadcn/ui + Radix UI (radix-ui v1.4.3)
- **Icons**: Lucide React 1.11.0
- **Utilities**: clsx, tailwind-merge, tw-animate-css

## Project Structure
- Path alias configured: `@/*` → root directory
- App Router only (no Pages Router)
- TypeScript strict mode enabled
- ESLint configured (eslint-config-next)

## Development Commands
- `npm run dev` — Start dev server (port 3000)
- `npm run build` — Production build
- `npm run start` — Start production server
- `npm run lint` — Run ESLint

## Key Development Guidelines

### React 19 & Next.js 16 Breaking Changes
- Server Components are default; use `'use client'` sparingly
- Form handling: use native HTML forms or `next/form`
- React 19 changed lifecycle hooks; check Next.js docs if unsure
- Heed deprecation warnings in error messages

### Component Development
- Use shadcn/ui components as building blocks
- Import from `@/components/ui/*` path alias
- Follow camelCase for functions, PascalCase for components
- 4-space indentation (enforced by eslint-config-next)

### Styling with Tailwind v4
- Use native Tailwind utilities (no arbitrary values for common patterns)
- Merge class conflicts with `clsx()` or `tailwind-merge`
- PostCSS plugin handles CSS generation automatically
- No custom CSS needed for most cases

### TypeScript Safety
- Strict mode enabled — fix type errors before committing
- Use explicit types for component props and functions
- Avoid `any` type; use `unknown` for truly unknown values

## Skill Recommendations
- `/component` — scaffold shadcn/ui components with types
- `/route` — generate App Router pages/API routes
- `/validate` — run lint + type check before pushing
- `/code-review` — detailed code analysis (set effort level as needed)
- `/verify` — test UI changes in browser

## Sub-agents Available
- **code-reviewer**: Review TypeScript safety, Next.js patterns, performance
- **debugger**: Fix runtime bugs, type errors, render issues

## Common Patterns

### Creating a New Component
```bash
npm run component
```
This scaffolds a `.tsx` file with TypeScript types and proper imports.

### Adding a New Route
```bash
npm run route
```
Generates App Router pages/API routes with boilerplate.

### Testing Before Commit
```bash
npm run validate
```
Runs eslint + TypeScript check locally.

## Performance Optimization Guide

### Image Optimization
- Use `next/image` component (automatic optimization)
- Add `sizes` prop for responsive images: `sizes="(max-width: 768px) 50px, 100px"`
- Use `priority` for above-the-fold images (LCP improvement)
- Add `placeholder="blur"` with `blurDataURL` for better perceived performance
```tsx
<Image
  src="/logo.svg"
  alt="Logo"
  width={100}
  height={20}
  priority
  sizes="(max-width: 768px) 50px, 100px"
/>
```

### Font Optimization
- Add `display: "swap"` to prevent FOUT (Flash of Unstyled Text)
- Load only required font weights to reduce bundle size
```tsx
const geistSans = Geist({
  variable: "--font-geist-sans",
  subsets: ["latin"],
  display: "swap", // Improves LCP
  weight: ["400", "500", "600"], // Only needed weights
});
```

### Server Components Strategy
- Keep components as Server Components by default (reduces JS bundle)
- Use `'use client'` only for interactive elements
- Data fetching happens on server automatically
```tsx
// ✅ Good: Server Component
export default function Home() {
  // Can access environment variables, databases, etc.
  return <div>...</div>;
}

// ❌ Only when needed: Client Component
"use client";
import { useState } from "react";
export function Counter() {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(count + 1)}>{count}</button>;
}
```

### Code Splitting & Dynamic Imports
- Load heavy components dynamically to reduce initial bundle:
```tsx
import dynamic from "next/dynamic";

const HeavyComponent = dynamic(() => import("@/components/heavy"), {
  loading: () => <div>Loading...</div>,
  ssr: false, // Only if client-side rendering needed
});
```

### Lucide React Optimization
- Import icons individually (auto tree-shaking)
```tsx
// ✅ Good
import { Menu, X, ArrowRight } from "lucide-react";

// ❌ Avoid
import * as Icons from "lucide-react";
```

### Metadata & SEO
- Add comprehensive metadata for better SEO:
```tsx
export const metadata: Metadata = {
  title: "App Title",
  description: "App description",
  openGraph: {
    title: "App Title",
    description: "App description",
    images: [{url: "/og-image.png", width: 1200, height: 630}],
  },
  icons: {icon: "/favicon.ico", apple: "/apple-touch-icon.png"},
};
```

### Static/ISR Optimization
- Use revalidate for static generation with periodic refresh:
```tsx
export const revalidate = 3600; // Refresh every 1 hour (ISR)
// or
export const dynamic = "force-static"; // Complete static generation
```

### Tailwind CSS v4
- Use native utilities (avoid arbitrary values for common patterns)
- Leverage CSS variables for consistent theming
- Keep class strings concise and readable (use spreading if needed)

### Caching Strategy
- Leverage Next.js automatic caching for static assets
- Set appropriate Cache-Control headers via middleware
- Use CDN for image delivery (Vercel Image Optimization)

### Performance Monitoring
- Add Web Vitals tracking (LCP, FID, CLS):
```tsx
import { Analytics } from "@vercel/analytics/react";
// In layout.tsx <body>
<Analytics /> // Automatic Core Web Vitals monitoring
```

### Bundle Analysis
- Run `npm run build` and check `.next/` output for bundle size
- Use Next.js built-in bundle analysis when needed

## Debugging
- Check `.next/` build output if you hit build errors
- Use `npm run lint` to catch TypeScript and ESLint issues early
- Browser DevTools: React DevTools extension helpful for component debugging
- See node_modules/next/dist/docs/ for latest Next.js docs when unsure

@AGENTS.md
