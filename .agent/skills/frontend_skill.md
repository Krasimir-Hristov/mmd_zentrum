---
name: Frontend Engineering Skill
description: Expert guidance on Next.js 16+, Tailwind CSS, Shadcn/UI, and State Management.
---

# Frontend Engineering Skill

## Core Principles

1.  **Atomic Design**: functionality first, then atomic breakdown.
2.  **Server Components**: Use React Server Components (RSC) by default. Only add 'use client' when interactivity is strictly needed.
3.  **Strict Types**: No `any`. Zod validation for all inputs.

## Tech Stack Guide

### Next.js 16+ (App Router)

- Use standard `page.tsx` for routes and `layout.tsx` for shared UI.
- Use `loading.tsx` for Suspense boundaries.
- **Data Fetching**: Prefer server-side fetching in Server Components. For client-side updates, use TanStack Query.

### Tailwind CSS & Shadcn/ui

- **Path**: `@/components/ui` for shadcn primitives.
- **Customization**: properties in `tailwind.config.ts`.
- **Classes**: Use `cn()` helper for conditional classes.

### State Management

- **Global**: `zustand` (stores in `@/stores`).
- **Server Cache**: `tanstack/react-query` (providers in `@/components/providers`).

## Best Practices

- **Optimistic UI**: Use `useMutation` with `onMutate` to update cache instantly.
- **Forms**: Use `react-hook-form` + `zod` schema.
