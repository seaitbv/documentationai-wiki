---
title: "Technology stack"
description: "Complete technology stack and dependency overview for the ARMS application"
---

## Overview

ARMS is built as a modern full-stack web application using Next.js 16 with React 19, backed by Supabase for authentication, database, and file storage. The UI uses Tailwind CSS with custom components, and the application supports Dutch and French localization.

## Core framework

| Technology | Version | Purpose |
|-----------|---------|---------|
| Next.js | 16.1.6 | Full-stack React framework with App Router |
| React | 19.2.3 | UI library with Server Components and Server Actions |
| TypeScript | ^5 | Type-safe development |

## Backend services

| Technology | Version | Purpose |
|-----------|---------|---------|
| Supabase JS | ^2.98.0 | Database client, authentication, and storage |
| Supabase SSR | ^0.9.0 | Server-side Supabase client with cookie-based auth |
| PostgreSQL | (via Supabase) | Primary database |

## Frontend

| Technology | Version | Purpose |
|-----------|---------|---------|
| Tailwind CSS | ^4 | Utility-first CSS framework |
| Lucide React | ^0.576.0 | Icon library |
| next-intl | ^4.8.3 | Internationalization (i18n) |

## Utilities

| Technology | Version | Purpose |
|-----------|---------|---------|
| xlsx | ^0.18.5 | Excel file parsing for kilometer data imports |

## Development tools

| Technology | Version | Purpose |
|-----------|---------|---------|
| Vitest | ^4.0.18 | Test runner |
| Testing Library (React) | ^16.3.2 | Component testing utilities |
| Testing Library (jest-dom) | ^6.9.1 | DOM assertion matchers |
| Testing Library (user-event) | ^14.6.1 | User interaction simulation |
| jsdom | ^28.1.0 | DOM environment for tests |
| Vite React plugin | ^5.1.4 | React support for Vitest |
| ESLint | ^9 | Code linting |
| eslint-config-next | 16.1.6 | Next.js-specific lint rules |
| @tailwindcss/postcss | ^4 | Tailwind CSS PostCSS plugin |

## Key architectural decisions

### Why Next.js App Router

ARMS uses the Next.js App Router (not Pages Router) for:
- **React Server Components** -- Fetch data directly in components without API routes
- **Server Actions** -- Mutate data without building REST endpoints
- **Streaming** -- Progressive page loading for better perceived performance
- **Route groups** -- Organize routes with shared layouts using `(app)` convention

### Why Supabase

Supabase provides three services in one platform:
- **Authentication** -- Email/password auth with JWT tokens and cookie-based sessions
- **Database** -- PostgreSQL with Row Level Security for multi-tenant data isolation
- **Storage** -- File uploads with signed URLs for secure document management

### Why next-intl

ARMS supports Dutch (NL) and French (FR) locales. next-intl provides:
- Cookie-based locale detection
- Server-side message loading
- Formatted dates, numbers, and currencies (EUR)
- Type-safe translation keys

### Why no shadcn/ui

ARMS uses custom-built UI components rather than a component library. All components (data tables, dropdowns, form fields, modals) are in the `components/` directory, built with Tailwind CSS and Lucide icons. This provides full control over styling and behavior.

## Package scripts

```json
{
  "dev": "next dev",
  "build": "next build",
  "start": "next start",
  "lint": "eslint",
  "typecheck": "tsc --noEmit",
  "test": "vitest run",
  "test:watch": "vitest"
}
```

| Script | Description |
|--------|-------------|
| `dev` | Start the development server with hot reload |
| `build` | Create a production build |
| `start` | Start the production server |
| `lint` | Run ESLint checks |
| `typecheck` | Run TypeScript type checking without emitting files |
| `test` | Run all tests once |
| `test:watch` | Run tests in watch mode |
