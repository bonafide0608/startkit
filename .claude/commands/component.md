---
name: component
description: Generate a new shadcn/ui component with TypeScript types and imports
trigger: /component <component-name>
---

# Component Generator

Generates a new shadcn/ui component with TypeScript support and Tailwind CSS styling.

## Usage

```
/component Button
/component Card
/component Dialog
```

## What it does

1. Downloads the component from shadcn/ui registry
2. Creates TypeScript type definitions
3. Generates component file with proper imports
4. Adds to lib/components or components/ directory
5. Creates a re-export in components/index.ts

## Requirements

- shadcn/ui must be installed
- Project must have components.json configured

## Example Output

Creates `components/button.tsx` with:
- Proper TypeScript types
- Tailwind CSS classes
- Radix UI integration
- Component props documentation
