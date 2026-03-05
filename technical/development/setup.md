---
title: "Development setup"
description: "Step-by-step guide to set up a local ARMS development environment"
---

## Prerequisites

Before you begin, make sure you have the following installed:

- **Node.js** 20 or later
- **pnpm** (recommended) or npm
- **Git**
- A **Supabase** project (local or cloud)

## Setup steps

### Step 1: Clone the repository

```bash
    git clone <repository-url> atrac
    cd atrac
    ```

### Step 2: Install dependencies

```bash
    pnpm install
    ```

    Or with npm:

    ```bash
    npm install
    ```

### Step 3: Configure environment variables

Copy the example environment file and fill in your values:

    ```bash
    cp .env.example .env.local
    ```

    See [[technical/development/env-variables|Environment variables]] for the full list of required and optional variables.

    At minimum, you need:

    ```
    NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
    NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY=eyJ...
    SUPABASE_SERVICE_ROLE_KEY=eyJ...
    NEXT_PUBLIC_APP_URL=http://localhost:3000
    ```

### Step 4: Set up Supabase

**Option A: Supabase Cloud**

    1. Create a project at [supabase.com](https://supabase.com)
    2. Copy the project URL and keys from the project settings
    3. Run migrations against the cloud database (see next step)

    **Option B: Supabase Local (recommended for development)**

    1. Install the Supabase CLI
    2. Start the local Supabase instance:

    ```bash
    supabase start
    ```

    3. Use the local URL and keys printed by the CLI

### Step 5: Run database migrations

Apply all 18 migration files in order:

    ```bash
    supabase db push
    ```

    Or if using the Supabase CLI with a local instance:

    ```bash
    supabase migration up
    ```

    This creates all tables, seed data, RLS policies, and storage buckets. See [[technical/database/migrations|Database migrations]] for details on each migration.

### Step 6: Start the development server

```bash
    pnpm dev
    ```

    The application starts at `http://localhost:3000`.

    > [!success]
> If everything is configured correctly, you should see the login page. Use the credentials set up in your Supabase project to log in.


## Verifying your setup

After starting the dev server, verify each layer:

| Check | Command / URL | Expected result |
|-------|--------------|-----------------|
| App loads | `http://localhost:3000` | Login page renders |
| Auth works | Log in with test credentials | Redirect to dashboard |
| Database connected | Navigate to Fleet page | Trailer list loads (may be empty) |
| Types are valid | `pnpm typecheck` | No errors |
| Tests pass | `pnpm test` | All tests green |
| Lint passes | `pnpm lint` | No errors |

## Common scripts

```bash
# Development server with hot reload
pnpm dev

# Type checking
pnpm typecheck

# Linting
pnpm lint

# Run all tests
pnpm test

# Run tests in watch mode
pnpm test:watch

# Production build
pnpm build

# Start production server
pnpm start
```

## Troubleshooting

> [!info]- Supabase connection errors
> - Verify `NEXT_PUBLIC_SUPABASE_URL` and `NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY` are correct
>     - For local Supabase, ensure `supabase start` has completed
>     - Check that your IP is not blocked by Supabase network restrictions (cloud only)


  > [!info]- Migration errors
> - Migrations must run in order (they are numbered sequentially)
>     - If a migration fails, check the SQL error and fix the issue before retrying
>     - For a fresh start, drop all tables and re-run migrations


  > [!info]- Authentication not working
> - Ensure the `SUPABASE_SERVICE_ROLE_KEY` is set (needed for admin operations)
>     - Verify that at least one user exists in the Supabase auth system
>     - Check that the `user_profile` table has a matching entry for the auth user
