---
title: "Environment variables"
description: "All environment variables required and optional for running ARMS"
---

## Overview

ARMS uses environment variables for configuration. Variables prefixed with `NEXT_PUBLIC_` are exposed to the browser; all others are server-only.

## Required variables

| Variable | Server/Client | Description | Example |
|----------|--------------|-------------|---------|
| `NEXT_PUBLIC_SUPABASE_URL` | Client | Supabase project URL | `https://abc123.supabase.co` |
| `NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY` | Client | Supabase anonymous/public key | `eyJhbGciOi...` |
| `SUPABASE_SERVICE_ROLE_KEY` | Server | Supabase service role key (full access, bypasses RLS) | `eyJhbGciOi...` |

> [!danger]
> Never expose `SUPABASE_SERVICE_ROLE_KEY` to the client. This key bypasses Row Level Security and has full database access. It should only be used in server-side code.


## Optional variables

### Application

| Variable | Server/Client | Description | Default |
|----------|--------------|-------------|---------|
| `NEXT_PUBLIC_APP_URL` | Client | Base URL of the application | `http://localhost:3000` |

### Microsoft Graph (email integration)

These variables are required only if you need the email draft feature (sending offers/contracts via Outlook).

| Variable | Server/Client | Description | Example |
|----------|--------------|-------------|---------|
| `MICROSOFT_CLIENT_ID` | Server | Azure AD application client ID | `a1b2c3d4-...` |
| `MICROSOFT_CLIENT_SECRET` | Server | Azure AD application client secret | `secret~value` |
| `MICROSOFT_TENANT_ID` | Server | Azure AD tenant ID | `common` or `a1b2c3d4-...` |

> [!info]
> If `MICROSOFT_CLIENT_ID` and `MICROSOFT_CLIENT_SECRET` are not set, the email integration will throw an error when invoked. The rest of the application functions normally without these variables.


## Environment file setup

Create a `.env.local` file in the project root:

```bash
# Supabase (required)
NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
SUPABASE_SERVICE_ROLE_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...

# Application
NEXT_PUBLIC_APP_URL=http://localhost:3000

# Microsoft Graph (optional - for email feature)
MICROSOFT_CLIENT_ID=your-client-id
MICROSOFT_CLIENT_SECRET=your-client-secret
MICROSOFT_TENANT_ID=common
```

## Variable usage in code

### Client-side (browser)

Variables prefixed with `NEXT_PUBLIC_` are available in both server and client code:

```typescript
// Available everywhere
const url = process.env.NEXT_PUBLIC_SUPABASE_URL!;
```

### Server-side only

Variables without the prefix are only available in server-side code (Server Components, Server Actions, API routes):

```typescript
// Only available in server-side code
const serviceKey = process.env.SUPABASE_SERVICE_ROLE_KEY!;
```

### Supabase client usage

The Supabase client factories use the environment variables:

```typescript
// lib/supabase/server.ts - Server client (uses cookies for auth)
const supabase = createServerClient(
  process.env.NEXT_PUBLIC_SUPABASE_URL!,
  process.env.NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY!,
  { cookies: { ... } }
);

// lib/supabase/client.ts - Browser client
const supabase = createBrowserClient(
  process.env.NEXT_PUBLIC_SUPABASE_URL!,
  process.env.NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY!,
);
```

## Local Supabase values

When running Supabase locally with `supabase start`, use the values printed by the CLI:

```bash
# Typical local Supabase values
NEXT_PUBLIC_SUPABASE_URL=http://127.0.0.1:54321
NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZS1kZW1vIiwicm9sZSI6ImFub24i...
SUPABASE_SERVICE_ROLE_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZS1kZW1vIiwicm9sZSI6InNlcnZpY2Vfcm9sZSI...
```
