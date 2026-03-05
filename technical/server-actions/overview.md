---
title: "Server actions overview"
description: "How ARMS uses Next.js server actions for data mutations and queries with Supabase"
---

## What are server actions

Server actions are asynchronous functions that run on the server in Next.js. ARMS uses them as the primary mechanism for all data mutations and many data queries. Each server action file begins with the `"use server"` directive, which tells Next.js to execute the function on the server rather than in the browser.

Server actions replace traditional API routes for most operations in ARMS. They can be called directly from React Server Components or from client components using form actions or event handlers.

## Common pattern

Every server action in ARMS follows a consistent pattern:

### Step 1: Authenticate the user

Call `requireAuth()` (or a role-specific variant like `requireAdmin()` or `requireFleetManager()`) to verify the user is logged in and has the correct permissions.

    ```typescript
    async function requireAuth() {
      const supabase = await createClient();
      const { data: { user } } = await supabase.auth.getUser();

      if (!user) {
        return { error: "Not authenticated", supabase: null, userId: null };
      }

      return { error: null, supabase, userId: user.id };
    }
    ```

### Step 2: Validate input

Check required fields and business rules before touching the database. Return early with a descriptive error string if validation fails.

    ```typescript
    if (!input.plate_number.trim())
      return { data: null, error: "plate_number is required" };
    ```

### Step 3: Query or mutate data

Use the Supabase client to perform the database operation (select, insert, update, or delete).

    ```typescript
    const { data, error } = await supabase
      .from("trailer")
      .insert({ ...fields, created_by: userId, updated_by: userId })
      .select("plate_number")
      .single();
    ```

### Step 4: Revalidate the cache

Call `revalidatePath()` to invalidate the Next.js cache so that affected pages re-fetch fresh data.

    ```typescript
    revalidatePath("/fleet", "layout");
    ```

### Step 5: Return a typed result

Every action returns a `Promise` with a consistent shape: `{ data, error }` for queries, or `{ error }` for mutations.

    ```typescript
    return { data: { plate_number: data.plate_number }, error: null };
    ```


## Return type conventions

All server actions follow one of two return patterns:

| Pattern | Used for | Shape |
|---------|----------|-------|
| Query result | Fetching data | `{ data: T \| null; error: string \| null }` |
| Mutation result | Create/update/delete | `{ error: string \| null }` |
| Create result | Creating records | `{ data: { id: number } \| null; error: string \| null }` |

## Error handling

Errors are returned as plain strings rather than thrown exceptions. This makes them easy to display in the UI. Common error patterns include:

- **Validation errors**: `"plate_number is required"`
- **Duplicate checks**: `"DUPLICATE_PLATE"`, `"DUPLICATE_VAT"`, `"DUPLICATE_REF"`
- **Auth errors**: `"Not authenticated"`, `"Only admin can manage parameters"`
- **Transition errors**: `"TRANSITION_NOT_ALLOWED"`
- **Database errors**: The raw Supabase error message is forwarded

## Authentication variants

Different action files use different authentication helpers based on the required access level:

| Helper | Required role | Used in |
|--------|--------------|---------|
| `requireAuth()` | Any authenticated user | trailers, customers, offers, contracts, invoicing |
| `requireAdmin()` | `admin` role | parameters |
| `requireFleetManager()` | `admin` or `fleet_manager` | documents |

## Server action files

ARMS organizes server actions into domain-specific files under `lib/actions/`:

| File | Domain | Key operations |
|------|--------|---------------|
| [[technical/server-actions/trailers|trailers.ts]] | Fleet management | CRUD for trailers and trailer properties |
| [[technical/server-actions/customers|customers.ts]] | Customer management | CRUD for customers and contacts, VIES integration |
| [[technical/server-actions/offers|offers.ts]] | Commercial | CRUD for offers, status transitions, contract conversion |
| [[technical/server-actions/contracts|contracts.ts]] | Commercial | CRUD for contracts, status transitions, auto-invoicing |
| [[technical/server-actions/invoicing|invoicing.ts]] | Billing | Proposal generation, invoice creation, Exact Online export |
| [[technical/server-actions/documents|documents.ts]] | File management | Upload, download, delete via Supabase Storage |
| [[technical/server-actions/parameters|parameters.ts]] | System config | Read and update application parameters |
| activity.ts | Activity stream | Log and retrieve user activity |
| dashboard.ts | Dashboard | Aggregate dashboard statistics |
| dropdown-values.ts | Dropdowns | Fetch dropdown categories and values |
| inspections.ts | Fleet | Trailer inspection records |
| km-registrations.ts | Fleet | Kilometer registration entries |
| non-driving-days.ts | Contracts | Non-driving day management |
| non-productive-periods.ts | Fleet | Non-productive period tracking |
| notifications.ts | Notifications | User notification management |
| offer-email.ts | Email | Offer email draft creation |
| contract-email.ts | Email | Contract email draft creation |
| templates.ts | Templates | Document template management |
| trailer-status.ts | Fleet | Trailer status changes |

## Audit trail

All create and update operations set `created_by` and `updated_by` fields with the authenticated user's ID. This provides a built-in audit trail for every record in the system.

```typescript
const { data, error } = await supabase
  .from("trailer")
  .insert({
    ...fields,
    created_by: userId,   // Set on creation
    updated_by: userId,   // Set on every update
  })
```
