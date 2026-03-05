---
title: "Parameter server actions"
description: "Server actions for reading and updating application configuration parameters"
---

## Overview

The parameter server actions in `lib/actions/parameters.ts` provide admin-only management of system-wide configuration values stored in the `parameter` table. These parameters control application behavior such as non-driving day thresholds, email recipients, and invoice numbering.

## Authorization

All write operations require the `admin` role, enforced by the `requireAdmin()` helper. Read operations use authenticated access.

## Functions

### getAllParameters

Fetches all parameters ordered by key name.

| Property | Value |
|----------|-------|
| Signature | `getAllParameters()` |
| Auth | Authenticated |
| Returns | `{ data: ParameterRow[] \| null; error: string \| null }` |

```typescript
interface ParameterRow {
  param_key: string;
  param_value: string;
  param_type: ParamType;
  description_nl: string | null;
  description_fr: string | null;
}
```

### updateParameter

Updates a parameter value after validating it against the parameter's declared type.

| Property | Value |
|----------|-------|
| Signature | `updateParameter(paramKey: string, paramValue: string)` |
| Auth | `requireAdmin()` |
| Returns | `{ error: string \| null }` |
| Revalidates | `/parameters` layout |

## Type validation

Each parameter has a declared type that is validated before saving:

| Type | Validation rule | Example |
|------|----------------|---------|
| `integer` | Must parse to a whole number | `"30"` |
| `decimal` | Must parse to a valid number | `"0.21"` |
| `boolean` | Must be `"true"` or `"false"` | `"true"` |
| `text` | Any string (no validation) | `"Hello"` |
| `email_list` | Comma-separated valid email addresses | `"a@b.com,c@d.com"` |

## Parameter library (`lib/parameters.ts`)

The parameter server actions work alongside the `lib/parameters.ts` library, which provides cached read access for use in server-side business logic.

### getParameter

Returns a typed parameter value with 5-minute caching via `unstable_cache`.

```typescript
async function getParameter(key: string): Promise<ParameterValue | null>
```

The return type depends on the parameter's `param_type`:
- `integer` returns `number`
- `decimal` returns `number`
- `boolean` returns `boolean`
- `text` returns `string`
- `email_list` returns `string[]`

### getParameterRaw

Returns the raw `ParameterRow` without type casting.

```typescript
async function getParameterRaw(key: string): Promise<ParameterRow | null>
```

### castParameterValue

Converts a string parameter value to its typed representation based on the parameter type.

```typescript
function castParameterValue(value: string, type: ParamType): ParameterValue
```

> [!info]
> Parameters are cached for 5 minutes using Next.js `unstable_cache` with the `"parameters"` cache tag. The cache is invalidated when `revalidatePath("/parameters")` is called after an update.
