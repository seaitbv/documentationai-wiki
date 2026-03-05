---
title: "Supabase Auth"
description: "Supabase Auth configuration, user profile management, session handling, and automatic logout behavior in ARMS."
---

## Overview

ARMS uses Supabase Auth as its primary authentication provider. Supabase manages the `auth.users` table, issues JWT tokens, and handles session persistence through HTTP-only cookies. The application extends this with a `user_profile` table for role assignment and user management.

## User profile table

The `user_profile` table extends Supabase's `auth.users` with application-specific data. It is linked via a foreign key on `user_id` referencing `auth.users(id)`.

| Column | Type | Required | Description |
|--------|------|----------|-------------|
| `user_id` | uuid (PK, FK) | Yes | References `auth.users(id)`, cascades on delete |
| `full_name` | text | Yes | User's display name |
| `role` | user_role (enum) | Yes | One of: `admin`, `commercial`, `accounting`, `fleet_manager`, `read_only` |
| `is_active` | boolean | Yes | Whether the user can access the system (default: `true`) |
| `created_on` | timestamptz | Yes | Record creation timestamp |
| `created_by` | uuid (FK) | No | User who created the record |
| `updated_on` | timestamptz | Yes | Last update timestamp |
| `updated_by` | uuid (FK) | No | User who last updated the record |

```sql
create type user_role as enum (
  'admin', 'commercial', 'accounting', 'fleet_manager', 'read_only'
);

create table user_profile (
  user_id    uuid        primary key references auth.users(id) on delete cascade,
  full_name  text        not null,
  role       user_role   not null default 'read_only',
  is_active  boolean     not null default true,
  created_on timestamptz not null default now(),
  created_by uuid        references auth.users(id),
  updated_on timestamptz not null default now(),
  updated_by uuid        references auth.users(id)
);
```

## Automatic user profile creation

A database trigger automatically creates a `user_profile` row when a new user signs up through Supabase Auth. The profile is initialized with the `read_only` role and the user's full name (falling back to their email address if no name is provided).

```sql
create or replace function handle_new_user()
returns trigger as $$
begin
  insert into public.user_profile (user_id, full_name)
  values (
    new.id,
    coalesce(new.raw_user_meta_data ->> 'full_name', new.email)
  );
  return new;
end;
$$ language plpgsql security definer;

create trigger on_auth_user_created
  after insert on auth.users
  for each row execute function handle_new_user();
```

> [!info]
> New users always start with the `read_only` role. An administrator must manually upgrade the user's role through the user management interface.


## Session management

### Middleware authentication check

The Next.js middleware validates the user session on every request using the Supabase server client. The client reads session cookies and verifies the JWT token.

```typescript middleware.ts
import { createServerClient } from "@supabase/ssr";
import { NextResponse, type NextRequest } from "next/server";

export async function middleware(request: NextRequest) {
  const response = NextResponse.next({ request });

  const supabase = createServerClient(
    process.env.NEXT_PUBLIC_SUPABASE_URL!,
    process.env.NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY!,
    {
      cookies: {
        getAll() {
          return request.cookies.getAll();
        },
        setAll(cookiesToSet) {
          cookiesToSet.forEach(({ name, value }) =>
            request.cookies.set(name, value)
          );
          cookiesToSet.forEach(({ name, value, options }) =>
            response.cookies.set(name, value, options)
          );
        },
      },
    }
  );

  const { data: { user } } = await supabase.auth.getUser();

  // Routing logic based on auth state
  if (!user && !isLoginPage) {
    return NextResponse.redirect(loginUrl);
  }
  if (user && isLoginPage) {
    return NextResponse.redirect(homeUrl);
  }

  return response;
}
```

### Route matcher

The middleware runs on all routes except static assets:

```typescript
export const config = {
  matcher: [
    "/((?!_next/static|_next/image|favicon.ico|.*\\.(?:svg|png|jpg|jpeg|gif|webp)$).*)",
  ],
};
```

### Automatic logout

The application supports a configurable automatic logout timeout stored in the `parameter` table with key `auto_logout_minutes` and type `integer`. When the timeout period elapses without user activity, the session is terminated.

> [!tip]
> The automatic logout timeout is managed through the Parameters admin page. Only users with the `admin` role can modify this value.


## User deactivation

Setting `is_active = false` on a `user_profile` record immediately revokes all data access. The `get_user_role()` function returns `NULL` for inactive users, which causes all RLS policies to deny access.

This means deactivation takes effect on the user's next database query -- no session invalidation is required.

## Environment variables

| Variable | Required | Description |
|----------|----------|-------------|
| `NEXT_PUBLIC_SUPABASE_URL` | Yes | Supabase project URL |
| `NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY` | Yes | Supabase anonymous (publishable) API key |

> [!danger]
> Never use the Supabase service role key in client-side code. The publishable key combined with RLS policies provides secure access without exposing administrative credentials.


## Related pages

- **[[technical/auth/overview|Authentication overview]]** — Full authentication architecture and flow diagrams.

  - **[[technical/auth/rbac|RBAC]]** — Role definitions and the application-level access matrix.

  - **[[technical/database/rls-policies|RLS policies]]** — Database-level security policies powered by get_user_role().
