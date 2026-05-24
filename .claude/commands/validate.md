---
name: validate
description: Run code quality checks (lint, type check, build) before deployment
trigger: /validate
---

# Validate Command

Runs comprehensive code quality checks to ensure your code is production-ready.

## Usage

```
/validate
```

## What it runs

1. **ESLint** — Linting and code style checks
   - Fixes auto-fixable issues automatically
   - Reports remaining issues

2. **TypeScript** — Type checking
   - Catches type errors
   - Validates type safety across the project

3. **Next.js Build** — Production build validation
   - Ensures no build errors
   - Checks for unresolved imports
   - Validates Next.js specific rules

## Output

Provides a summary report:
- ✓ ESLint results
- ✓ TypeScript check results
- ✓ Build status
- ✓ Any warnings or errors to fix

## When to use

- Before committing code
- Before pushing to remote
- Before deploying to production
- During development to catch issues early

## Exit codes

- 0: All checks passed
- 1: One or more checks failed
