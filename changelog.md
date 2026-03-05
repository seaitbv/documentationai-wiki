---
title: "Changelog"
description: "Release history and version notes for the ARMS application."
---

## Releases

## v1.0.0 — 2026-03-04 `Initial Release`

### ARMS 1.0 — Initial release

  The first production release of the Atrac Rental Management System.

  **Core modules:**
  - Fleet management with trailer CRUD, inspections, km registrations, and non-productive periods
  - Customer management with VIES VAT validation
  - Offer lifecycle with Outlook email integration
  - Contract lifecycle with automatic status transitions
  - Invoice proposal generation for day-based, month-based, and km-based contracts
  - Exact Online JSON export for invoices
  - Gantt-style planning timeline
  - Parameterizable thresholds and business rules

  **Technical highlights:**
  - Next.js 16 with React 19 Server Components
  - Supabase PostgreSQL with Row Level Security
  - Five user roles (Admin, Commercial, Accounting, Fleet Manager, Read-Only)
  - Bilingual support (NL/FR) via next-intl
  - Microsoft Graph API integration for Outlook drafts
  - 18 database migrations with comprehensive RLS policies

  **Known limitations:**
  - Exact Online integration is JSON download only (API integration planned for v1.1)
  - Chart zone on dashboard is planned for a future release
  - Transics API integration for km data is planned for a future release
