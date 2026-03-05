---
title: "Component library"
description: "Custom UI components used across the ARMS application"
---

## Overview

ARMS uses a custom component library built with Tailwind CSS and Lucide React icons. All components live in the `components/` directory and are designed for consistency across the application. There is no third-party component library (no shadcn/ui, Radix, or MUI).

## Styling approach

| Technology | Purpose |
|-----------|---------|
| Tailwind CSS 4.x | Utility-first CSS framework for all styling |
| Lucide React | Icon library used consistently across all components |
| CSS variables | Theme colors and spacing tokens |

Components use Tailwind utility classes directly, with no CSS modules or styled-components. Variants and states are handled through conditional class names.

## Core components

### Layout components

| Component | File | Description |
|-----------|------|-------------|
| Sidebar | `sidebar.tsx` | Main navigation sidebar with collapsible menu items |
| Header | `header.tsx` | Page header with breadcrumbs and actions |
| HeaderCard | `header-card.tsx` | Card-style header for detail pages |
| TabNav | `tab-nav.tsx` | Horizontal tab navigation within pages |
| FormLayout | `form-layout.tsx` | Grid layout wrapper for forms |

### Data display components

| Component | File | Description |
|-----------|------|-------------|
| DataTable | `data-table.tsx` | Sortable, paginated data table with column configuration |
| StatusBadge | `status-badge.tsx` | Colored badge for displaying entity statuses |
| EmptyState | `empty-state.tsx` | Placeholder for empty lists with icon and message |
| TableSkeleton | `table-skeleton.tsx` | Loading skeleton that mimics table layout |
| Pagination | `pagination.tsx` | Page navigation for tables |

### Form components

| Component | File | Description |
|-----------|------|-------------|
| FormField | `form-field.tsx` | Wrapper with label, error message, and required indicator |
| TextInput | `text-input.tsx` | Single-line text input |
| TextArea | `text-area.tsx` | Multi-line text input |
| NumberInput | `number-input.tsx` | Numeric input with decimal/integer modes |
| DatePicker | `date-picker.tsx` | Date input with calendar |
| Checkbox | `checkbox.tsx` | Checkbox with label |
| Dropdown | `dropdown.tsx` | Standard select dropdown |
| SmartDropdown | `smart-dropdown.tsx` | Searchable dropdown with async data loading |
| Lookup | `lookup.tsx` | Async search field for entity selection (customers, contacts) |

### Action components

| Component | File | Description |
|-----------|------|-------------|
| NewButton | `new-button.tsx` | Styled "Create new" button |
| ExportButton | `export-button.tsx` | Data export trigger button |
| FilterBar | `filter-bar.tsx` | Table filter controls row |
| ConfirmDialog | `confirm-dialog.tsx` | Confirmation modal for destructive actions |
| Toast | `toast.tsx` | Temporary notification messages |

### Utility components

| Component | File | Description |
|-----------|------|-------------|
| LanguageSwitcher | `language-switcher.tsx` | NL/FR locale toggle |

## Component patterns

### DataTable pattern

The `DataTable` component is the most-used component, appearing on every list page. It accepts column definitions and data:

```typescript
<DataTable
  columns={[
    { key: "trailer_ref", label: t("ref"), sortable: true },
    { key: "plate_number", label: t("plate"), sortable: true },
    { key: "status", label: t("status"), render: (row) => (

    )},
  ]}
  data={trailers}
  onRowClick={(row) => router.push(`/fleet/${row.plate_number}`)}
/>
```

### FormField pattern

Form fields are wrapped in `FormField` for consistent layout:

```typescript
<FormField label={t("plateNumber")} error={errors.plate_number} required>
  <TextInput
    value={form.plate_number}
    onChange={(v) => setForm({ ...form, plate_number: v })}
  />
</FormField>
```

### Lookup pattern

The `Lookup` component provides async search for entity references:

```typescript
<Lookup
  value={form.customer_id}
  onSearch={async (query) => searchCustomers(query)}
  onSelect={(item) => setForm({ ...form, customer_id: item.value })}
  placeholder={t("searchCustomer")}
/>
```

### SmartDropdown pattern

`SmartDropdown` combines a standard dropdown with search filtering:

```typescript
<SmartDropdown
  options={trailerTypes}
  value={form.trailer_type_id}
  onChange={(v) => setForm({ ...form, trailer_type_id: v })}
  searchable
/>
```

## Icon usage

ARMS uses Lucide React icons consistently throughout the application:

```typescript
import { Plus, Pencil, Trash2, Download, Search } from "lucide-react";

// In JSX
<button>

  {t("add")}
</button>
```

Common icon conventions:
- `Plus` for create/add actions
- `Pencil` for edit actions
- `Trash2` for delete actions
- `Download` for export/download
- `Search` for search inputs
- `ChevronLeft` / `ChevronRight` for navigation
- `Check` for success states
- `AlertTriangle` for warnings

## Testing

Every component has a corresponding `.test.tsx` file that verifies rendering, user interactions, and edge cases using Testing Library. See [[technical/development/testing|Testing]] for details on the test infrastructure.
