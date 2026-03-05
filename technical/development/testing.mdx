---
title: "Testing"
description: "Test infrastructure, patterns, and coverage areas in the ARMS codebase"
---

## Overview

ARMS uses Vitest as the test runner with Testing Library for component tests. Tests follow a co-location pattern where test files sit alongside the code they test.

## Test infrastructure

| Tool | Purpose |
|------|---------|
| Vitest 4.x | Test runner and assertion library |
| @testing-library/react | React component rendering and querying |
| @testing-library/jest-dom | DOM-specific assertion matchers |
| @testing-library/user-event | User interaction simulation |
| jsdom | Browser environment simulation |

## Running tests

```bash
# Run all tests once
pnpm test

# Run tests in watch mode (re-runs on file changes)
pnpm test:watch
```

## Test file conventions

Test files use the `*.test.ts` or `*.test.tsx` pattern and are co-located with their source files:

```
lib/
  exactonline.ts
  exactonline.test.ts          # Tests for exactonline.ts
  vies.ts
  vies.test.ts                 # Tests for vies.ts
  actions/
    trailers.ts
    trailers.test.ts           # Tests for trailer actions
app/(app)/
  invoices/
    invoicing-utils.ts
    invoicing-utils.test.ts    # Tests for invoicing utilities
components/
  data-table.tsx
  data-table.test.tsx          # Tests for DataTable component
```

## Test coverage areas

### Business logic tests (`lib/`)

| Test file | What it covers |
|-----------|---------------|
| `exactonline.test.ts` | VAT code mapping, invoice serialization, export validation |
| `vies.test.ts` | VAT number parsing, address parsing, VIES API responses |
| `microsoft-graph.test.ts` | Authorization URL building, token exchange, draft creation |
| `parameters.test.ts` | Parameter type casting, value validation |
| `rbac.test.ts` | Role-based access control checks |
| `offer-status-transitions.test.ts` | Offer state machine transition validation |
| `contract-status-transitions.test.ts` | Contract state machine transition validation |
| `invoice-status-transitions.test.ts` | Invoice state machine transition validation (via `status-transitions.test.ts`) |
| `activity-utils.test.ts` | Activity stream formatting |
| `dashboard-utils.test.ts` | Dashboard statistic calculations |
| `notification-utils.test.ts` | Notification formatting and filtering |
| `offer-email-utils.test.ts` | Offer email content generation |
| `contract-email-utils.test.ts` | Contract email content generation |
| `i18n.test.ts` | Internationalization utilities |

### Server action tests (`lib/actions/`)

| Test file | What it covers |
|-----------|---------------|
| `trailers.test.ts` | Trailer CRUD validation, uniqueness checks |
| `documents.test.ts` | Upload validation, MIME type checking, file size limits |
| `parameters.test.ts` | Parameter type validation, admin authorization |
| `dropdown-values.test.ts` | Dropdown value fetching and filtering |
| `contracts-auto-invoice.test.ts` | Auto-invoice creation on contract acceptance |

### Domain utility tests (`app/(app)/`)

| Test file | What it covers |
|-----------|---------------|
| `invoicing-utils.test.ts` | Day/month calculation, proposal status, advance offsets |
| `fleet-utils.test.ts` | Fleet list filtering and sorting |
| `trailer-form-utils.test.ts` | Trailer form validation |
| `trailer-properties-utils.test.ts` | Technical property validation |
| `document-utils.test.ts` | Document list utilities |
| `inspection-utils.test.ts` | Inspection record utilities |
| `km-registration-utils.test.ts` | Kilometer registration calculations |
| `km-import-utils.test.ts` | Excel import parsing |
| `non-productive-period-utils.test.ts` | Non-productive period calculations |
| `offer-form-utils.test.ts` | Offer form validation |
| `offer-utils.test.ts` | Offer list utilities |
| `contract-form-utils.test.ts` | Contract form validation |
| `contract-utils.test.ts` | Contract list utilities |
| `damage-control-utils.test.ts` | Damage assessment validation |
| `non-driving-days-utils.test.ts` | Non-driving day calculations |
| `planning-utils.test.ts` | Planning calendar utilities |
| `parameters-utils.test.ts` | Parameter admin utilities |
| `email-template-utils.test.ts` | Email template variable resolution |
| `template-utils.test.ts` | Document template utilities |

### Component tests (`components/`)

| Test file | What it covers |
|-----------|---------------|
| `data-table.test.tsx` | Table rendering, sorting, pagination |
| `dropdown.test.tsx` | Dropdown selection, options rendering |
| `smart-dropdown.test.tsx` | Async search, debouncing |
| `form-field.test.tsx` | Label, error display, required indicator |
| `form-layout.test.tsx` | Grid layout rendering |
| `checkbox.test.tsx` | Checked/unchecked states |
| `confirm-dialog.test.tsx` | Modal open/close, confirm/cancel actions |
| `date-picker.test.tsx` | Date selection, format display |
| `number-input.test.tsx` | Numeric input validation |
| `text-input.test.tsx` | Text input rendering |
| `text-area.test.tsx` | Textarea rendering |
| `pagination.test.tsx` | Page navigation |
| `status-badge.test.tsx` | Status color mapping |
| `toast.test.tsx` | Toast appearance and dismissal |
| `sidebar.test.tsx` | Navigation rendering |
| `header.test.tsx` | Header rendering |
| `header-card.test.tsx` | Card header rendering |
| `empty-state.test.tsx` | Empty state messaging |
| `filter-bar.test.tsx` | Filter controls |
| `export-button.test.tsx` | Export trigger |
| `lookup.test.tsx` | Async lookup field |
| `new-button.test.tsx` | New item button |
| `tab-nav.test.tsx` | Tab navigation |
| `table-skeleton.test.tsx` | Loading skeleton |

### Integration tests

| Test file | What it covers |
|-----------|---------------|
| `app/(app)/page.test.tsx` | Dashboard page rendering |
| `middleware.test.ts` | Auth middleware redirect logic |
| `hooks/use-parameter.test.ts` | Parameter hook behavior |

## Testing patterns

### Mocking Supabase

Server action tests mock the Supabase client to test business logic without a database connection:

```typescript
vi.mock("@/lib/supabase/server", () => ({
  createClient: vi.fn(() => ({
    from: vi.fn(() => ({
      select: vi.fn().mockReturnThis(),
      insert: vi.fn().mockReturnThis(),
      // ...chain methods
    })),
    auth: { getUser: vi.fn() },
  })),
}));
```

### Testing state machines

State transition tests verify allowed and blocked transitions:

```typescript
it("allows transition from Aangemaakt to Verstuurd", () => {
  expect(isOfferTransitionAllowed("Aangemaakt", "Verstuurd")).toBe(true);
});

it("blocks transition from Geannuleerd to Aangemaakt", () => {
  expect(isOfferTransitionAllowed("Geannuleerd", "Aangemaakt")).toBe(false);
});
```
