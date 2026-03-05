---
title: "Project structure"
description: "Directory layout and organization of the ARMS codebase"
---

## Overview

ARMS follows Next.js App Router conventions with a clear separation between routing (app directory), business logic (lib directory), and UI components (components directory).

## Top-level directory tree

```
atrac/
  app/
    (app)/                    # Main authenticated app route group
    login/                    # Login page (outside route group)
    api/                      # API routes (Microsoft OAuth callback)
    layout.tsx                # Root layout
  components/                 # Shared UI components
  hooks/                      # Custom React hooks
  i18n/                       # Internationalization config
  lib/                        # Business logic and utilities
    actions/                  # Server actions (data mutations)
    supabase/                 # Supabase client factories
  messages/                   # Translation files (nl.json, fr.json)
  supabase/
    migrations/               # Database migration files
  middleware.ts               # Auth middleware
  next.config.ts              # Next.js configuration
  package.json                # Dependencies and scripts
```

## App directory

The `app/(app)/` route group contains all authenticated pages. The parentheses in `(app)` create a route group that shares a layout without adding a URL segment.

```
app/(app)/
  layout.tsx                  # Sidebar navigation, auth check
  page.tsx                    # Dashboard (home page)
  dashboard-client.tsx        # Dashboard client component
  activity-stream.tsx         # Activity feed widget
  notification-panel.tsx      # Notification dropdown
  fleet/                      # Trailer management pages
  customers/                  # Customer management pages
  contacts/                   # Contact directory pages
  offers/                     # Offer management pages
  contracts/                  # Contract management pages
  invoices/                   # Invoicing workflow pages
  planning/                   # Planning calendar page
  parameters/                 # System parameter admin
  templates/                  # Document template management
```

Each domain directory typically contains:
- `page.tsx` -- List/overview page (Server Component)
- `[id]/page.tsx` -- Detail/edit page with dynamic route
- `new/page.tsx` -- Creation form page
- `*-utils.ts` -- Client-side utility functions
- `*-utils.test.ts` -- Tests for utilities

## Lib directory

The `lib/` directory contains all business logic, separated from the UI:

```
lib/
  actions/                    # Server actions (see Server Actions docs)
    trailers.ts
    customers.ts
    offers.ts
    contracts.ts
    invoicing.ts
    documents.ts
    parameters.ts
    ...
  supabase/
    client.ts                 # Browser Supabase client
    server.ts                 # Server Supabase client (cookie-based)
  parameters.ts               # Cached parameter access
  microsoft-graph.ts          # Microsoft Graph API integration
  exactonline.ts              # Exact Online export serialization
  vies.ts                     # EU VIES VAT validation
  rbac.ts                     # Role-based access control utilities
  offer-status-transitions.ts # Offer state machine
  contract-status-transitions.ts # Contract state machine
  invoice-status-transitions.ts  # Invoice state machine
  ...
```

## Components directory

Custom UI components built with Tailwind CSS and Lucide icons:

```
components/
  checkbox.tsx                # Checkbox input
  confirm-dialog.tsx          # Confirmation modal
  data-table.tsx              # Sortable, paginated data table
  date-picker.tsx             # Date input with calendar
  dropdown.tsx                # Standard dropdown select
  smart-dropdown.tsx          # Searchable dropdown with async loading
  empty-state.tsx             # Empty state placeholder
  export-button.tsx           # Data export button
  filter-bar.tsx              # Table filter controls
  form-field.tsx              # Form field wrapper with label/error
  form-layout.tsx             # Form layout grid
  header.tsx                  # Page header
  header-card.tsx             # Card-style header
  language-switcher.tsx       # NL/FR locale toggle
  lookup.tsx                  # Async search lookup field
  new-button.tsx              # "New item" button
  number-input.tsx            # Numeric input field
  pagination.tsx              # Table pagination controls
  sidebar.tsx                 # Navigation sidebar
  status-badge.tsx            # Colored status indicator
  tab-nav.tsx                 # Tab navigation
  table-skeleton.tsx          # Loading skeleton for tables
  text-area.tsx               # Multi-line text input
  text-input.tsx              # Single-line text input
  toast.tsx                   # Toast notification
```

Each component has a corresponding `.test.tsx` file for unit tests.

## Messages directory

Translation files for internationalization:

```
messages/
  nl.json                     # Dutch translations (primary)
  fr.json                     # French translations
```

Messages are organized by namespace (e.g., `common`, `nav`, `fleet`, `validation`) and loaded server-side based on the user's locale cookie.

## Supabase migrations

Database schema is managed through numbered migration files:

```
supabase/migrations/
  20260303000001_core_tables.sql
  20260303000002_seed_data.sql
  ...
  20260303000018_template_table.sql
```

See [[technical/database/migrations|Database migrations]] for the full list and descriptions.

## Key conventions

- **Server Components by default**: Pages are React Server Components unless client interactivity is needed
- **Co-located utilities**: Domain-specific utilities live alongside their pages (e.g., `invoices/invoicing-utils.ts`)
- **Co-located tests**: Test files are next to the code they test (e.g., `invoicing-utils.test.ts`)
- **Shared components**: Reusable UI components live in the top-level `components/` directory
- **Business logic in `lib/`**: All database interactions and integrations are in `lib/` or `lib/actions/`
