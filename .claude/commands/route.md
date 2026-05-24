---
name: route
description: Generate Next.js App Router page or API route with scaffolding
trigger: /route <path> [--type=page|api]
---

# Route Generator

Creates a new page or API route with proper folder structure and TypeScript templates.

## Usage

```
/route app/dashboard
/route app/users/[id]
/route api/users --type=api
/route api/auth/login --type=api
```

## What it does

### For Pages (`--type=page` or default)

1. Creates folder structure: `app/<path>/`
2. Generates `page.tsx` with:
   - React Server Component setup
   - TypeScript types
   - Basic layout structure
   - Metadata configuration

3. Creates `layout.tsx` if needed
4. Sets up Tailwind CSS styling

### For API Routes (`--type=api`)

1. Creates folder structure: `app/api/<path>/`
2. Generates `route.ts` with:
   - HTTP method handlers (GET, POST, PUT, DELETE)
   - TypeScript request/response types
   - Error handling
   - CORS headers (if needed)

3. Includes JSDoc documentation

## Examples

**Page Route:**
```
/route app/dashboard
```
Creates: `app/dashboard/page.tsx` with Server Component setup

**Dynamic Route:**
```
/route app/users/[id]
```
Creates: `app/users/[id]/page.tsx` with dynamic params

**API Route:**
```
/route api/users --type=api
```
Creates: `app/api/users/route.ts` with GET/POST handlers

## Output Structure

For `/route app/dashboard`:
```
app/
  dashboard/
    page.tsx (Server Component)
    layout.tsx (optional)
```

For `/route api/users --type=api`:
```
app/
  api/
    users/
      route.ts (API handlers)
```

## Features

- TypeScript support
- Tailwind CSS integration
- Proper imports setup
- Error handling templates
- Type-safe request/response
