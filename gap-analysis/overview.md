---
title: "PRD v1.3.1 Gap Analysis"
description: "Comprehensive gap analysis comparing PRD v1.3.1 requirements against the current ARMS implementation, covering functional, technical, and architectural perspectives."
---

## About this analysis

This gap analysis compares PRD v1.3.1 (dated 04-03-2026) against the current ARMS implementation. The methodology uses a 6-perspective analysis (Functional, Technical, Solution Architecture, Database, Next.js, Devil's Advocate) against the full PRD and codebase.

### Status legend

<Callout kind="success">
  **Implemented** — Feature is fully implemented and matches PRD requirements.
</Callout>

<Callout kind="alert">
  **Partially implemented** — Feature exists but is incomplete or deviates from PRD specifications.
</Callout>

<Callout kind="danger">
  **Not implemented** — Feature is entirely missing from the current codebase.
</Callout>

---

## 1. Missing screens

Cross-referenced against Bijlage B (31 screens). The current implementation has approximately 16 screens; 10 are fully missing and 5 are partially implemented.

### 1.1 Completely missing screens (10)

| # | PRD Screen | PRD Ref | Expected Route | Notes |
|---|-----------|---------|---------------|-------|
| 1 | Keuringen overzicht (standalone) | Bijlage B #6 | `/inspections` | Only exists as tab within trailer detail. No cross-fleet inspection overview. |
| 2 | Kilometerstanden overzicht (standalone) | Bijlage B #7 | `/km-registrations` | Only exists as tab within trailer detail. No cross-fleet km overview. |
| 3 | Documentenbibliotheek (global) | Bijlage B #20, FR-DOC-002 | `/documents` | Documents only attached per-entity. No global cross-search library with filters (entity type, company, document type, datum, uploader). |
| 4 | Communicatielog | Bijlage B #21, FR-CLOG-001 | `/communication` | No communication log page. No tracking of Outlook draft creation, sent marking, or per-offerte/contract log. |
| 5 | Integraties — Exact Online | Bijlage B #22, TR-EXACT-001 | `/integrations/exact` | No integration config screen. Export queue, retry, error visibility per record all missing. |
| 6 | Service/Repair order koppeling | Bijlage B #24, TR-REPAIR-001 | `/service-orders` | Only a `repair_order_ref` text field on contract. No dedicated linking screen, no status sync. |
| 7 | Bedrijven beheer (Atrac/Urbain) | Bijlage B #27, FR-ORG-001 | `/companies` | Companies loaded from DB for dropdowns but no admin CRUD UI. |
| 8 | Locaties beheer (pick-up locations) | Bijlage B #28, FR-ORG-001 | `/locations` | Locations used in dropdowns but no admin management UI. |
| 9 | Gebruikers & Rollen | Bijlage B #30, SEC-RBAC-001 | `/users` | `user_profile` table exists but no admin UI for managing users/roles. |
| 10 | Auditlog | Bijlage B #31, FR-AUD-001 | `/audit` | No audit log viewer. No `audit_log` table. No before/after value tracking. |

### 1.2 Partially implemented screens (5)

| # | PRD Screen | PRD Ref | Current State | Gap |
|---|-----------|---------|--------------|-----|
| 1 | Meldingen center | FR-NOTIF-001/002 | Sidebar panel on dashboard (`notification-panel.tsx`) | PRD requires standalone inbox with status (new/read/handled), filters (type/status/period/owner/company), and deep links. Current is a simple panel, not a full inbox. |
| 2 | Facturatievoorstellen | FR-INVP-001-005 | Tab within invoices page | PRD specifies separate screen. Combined with invoices makes navigation harder. |
| 3 | Facturen genereren (batch) | FR-INVP-004 | Embedded in proposals tab | PRD specifies dedicated batch generation screen with multiselect. |
| 4 | Import/Export Kilometerstanden | TR-TRANS-001 | Modal dialog (`km-import-dialog.tsx`) within fleet | PRD specifies standalone page with mapping, preview, validation, and persistent import log. |
| 5 | Stamdata beheer (dropdown manager) | FR-MD-001 | Section within Parameters page | PRD implies standalone page. Current is a tab on Parameters. Functional but not separately navigable. |

---

## 2. Database schema gaps

<ExpandableGroup>
  <Expandable title="2.1 Missing columns" default-open="true">
    | Table | Missing Column | PRD Ref | Type | Mandatory | Notes |
    |-------|---------------|---------|------|-----------|-------|
    | `customer` | `floor` | Bijlage A, Customer #7 | text | No | Address field for floor/verdieping. Missing entirely. |
    | `contract` | `damage_description` | FR-CON-009 | text | No | PRD says "schade (ja/nee + beschrijving)". `damage_found` boolean exists but no description field. |
    | `contract` | `checked_date` | FR-CON-009 | date | No | PRD says "gecontroleerd (ja/nee + datum)". `checked_after_return` boolean exists but no date. |
    | `notification_log` | `status` values | FR-NOTIF-001 | - | - | PRD requires new/gelezen/afgehandeld. Current has only `'sent'` default. Needs enum or dropdown for inbox-style status. |
    | `notification_log` | `owner` | FR-NOTIF-001 | uuid | No | PRD requires filter by owner. No ownership column exists. |
  </Expandable>

  <Expandable title="2.2 Enum/constraint gaps" default-open="false">
    | Enum | Current Values | PRD Requires | Gap |
    |------|---------------|-------------|-----|
    | `contact_language` | `'NL', 'FR'` | `'NL', 'FR', 'EN'` | **EN missing**. Affects contact, offer, contract, document_template tables. |
    | `entity_type` | `'trailer', 'contract', 'offer', 'inspection'` | + `'customer', 'invoice'` | Documents cannot be attached to customers or invoices. |
    | Contract status (dropdown seed) | 7 values (Aangemaakt, Verzonden, Geaccepteerd, In verhuur, Te controleren, Afgerond, Geweigerd) | + `Schadeverwerking` | **Damage processing state missing**. PRD: Te controleren -> Schadeverwerking -> Afgerond. |
    | Invoice status (dropdown seed) | 4 values (Aangemaakt, Verzonden, Betaald, Geannuleerd) | + `exported`, `failed`, + Exact statuses (paid/unpaid) | Missing `exported` and `failed` statuses for Exact Online lifecycle. |
  </Expandable>

  <Expandable title="2.3 Missing seed data" default-open="false">
    | Category | Gap |
    |----------|-----|
    | `document_type` | Only 3 types seeded (Getekend contract, Trailerfoto, Inschrijvingsbewijs). PRD implies more (e.g., "Overig"). |
    | `ADVANCE_DUE_DATE_OFFSET_DAYS` parameter | PRD requires configurable offset for advance invoice due date (`contract start - N days`). Parameter does not exist. |
    | EN email templates | `OFFER_EMAIL_SUBJECT_EN`, `OFFER_EMAIL_BODY_EN`, `CONTRACT_EMAIL_SUBJECT_EN`, `CONTRACT_EMAIL_BODY_EN` all missing. |
  </Expandable>
</ExpandableGroup>

---

## 3. Missing tables

| # | Table | PRD Ref | Purpose | Priority |
|---|-------|---------|---------|----------|
| 1 | `audit_log` | FR-AUD-001 | Track who/what/when with before/after values for core entities. GDPR-limited PII. | Must/MVP |
| 2 | `communication_log` | FR-CLOG-001 | Track Outlook drafts created, by whom, when, linked to offer/contract, sent marking with timestamp. | Must/MVP |
| 3 | `import_log` | TR-TRANS-001 | Persist Transics/Excel import results: success/fail per record, timestamp, user, file reference. | Must/MVP |
| 4 | `contract_damage_control` | FR-CON-009 | Dedicated table for post-return inspection details. Current schema has only boolean fields on contract. Needed for detailed damage records, repair order linking, multiple inspections. | Should |
| 5 | `repair_order` | TR-REPAIR-001 | External repair order references with status field affecting planning highlights. Current: only `repair_order_ref` text on contract. | Must/MVP |

<Callout kind="info">
  **Note on `customer_contact`**: PRD Bijlage A implies a separate linking table, but current schema uses 1:N (contact belongs to one customer via `customer_id` FK). If the business truly requires many-to-many (one contact for multiple customers), a junction table is needed. This requires stakeholder clarification.
</Callout>

<Callout kind="info">
  **Note on `document_link`**: PRD mentions "Document + DocumentLink". Current uses polymorphic `entity_type + entity_id` on `document` table. This works for 1:1 document-to-entity linking but does not support linking one document to multiple entities. Current approach is acceptable if cross-linking is not required.
</Callout>

---

## 4. Business logic gaps

<ExpandableGroup>
  <Expandable title="4.1 KM invoicing — NOT IMPLEMENTED" default-open="true">
    <Callout kind="danger">
      **Severity: Critical** — Entire billing unit missing (FR-INVP-001, Section 7.4).
    </Callout>

    The `generateInvoiceProposals` function (`lib/actions/invoicing.ts`) only accepts `unitType: "day" | "month"`. KM is entirely excluded.

    **Missing functionality:**
    - KM proposal generation (determine start/end km from `km_registration` table)
    - KM billing calculation (`km_driven x unit_price_rental`)
    - Red marking when km registration data is missing near billing period boundaries (FR-INVP-003)
    - `invoice_km_lock` creation during KM invoicing (table exists but never populated)
    - Exclusion of non-driving days for KM contracts (FR-INVP-005)
    - Exclusion of KM allowance for km-unit contracts (Section 7.4)
  </Expandable>

  <Expandable title="4.2 KM yearly allowance — NOT IMPLEMENTED" default-open="true">
    <Callout kind="danger">
      **Severity: High** — Revenue-relevant calculation missing (Section 7.1).
    </Callout>

    Parameters exist (`KM_YEARLY_MAX = 100000`, `KM_SURPLUS_PRICE_EUR = 0.30`) but no code consumes them.

    **Missing functionality:**
    - Annual KM usage computation per contract/trailer
    - Comparison against 100,000 km threshold
    - Surcharge calculation at 0.30 EUR/km for overage
    - Surcharge invoice line generation
  </Expandable>

  <Expandable title="4.3 Forfait logic" default-open="false">
    <Callout kind="success">
      **Status: Implemented.** Forfait correctly uses total contract duration (not invoice period). Parameters `FORFAIT_1_DAY_EUR` (120) and `FORFAIT_2_DAYS_EUR` (170) are configurable.
    </Callout>
  </Expandable>

  <Expandable title="4.4 Deposit/advance gaps" default-open="true">
    <Callout kind="alert">
      **Section 7.6** — Multiple deviations from PRD requirements.
    </Callout>

    | Gap | PRD Requirement | Current Implementation |
    |-----|----------------|----------------------|
    | Combined invoice | Deposit + advance on 1 invoice with 2 lines (FR-DEP-001) | Creates 2 separate invoices |
    | Due date | `contract_start - N days` (parameter, default 14) (FR-DEP-002) | Uses `today + 30 days` |
    | Negative line convention | `qty < 0, price > 0` (Peppol/accounting compatible) (FR-DEP-003) | Uses `qty: 1, price: -amount` |
    | Saldo tracking | Only real invoices affect saldo, not proposals (FR-DEP-004) | No distinction between proposals and invoices for saldo |
    | Default advance amount | day=30xprice, month=1xprice, km=6000kmxprice (Section 7.6) | Default 0, no auto-calculation |
  </Expandable>

  <Expandable title="4.5 Contract status flow gaps" default-open="true">
    <Callout kind="alert">
      **FR-CON-005** — Missing states and auto-transitions.
    </Callout>

    | Gap | Details |
    |-----|---------|
    | Missing "Schadeverwerking" state | PRD: Te controleren -> Schadeverwerking (if damage) -> Afgerond. Current: Te controleren -> Afgerond directly. |
    | No auto-transition to "Te controleren" | PRD implies auto-transition when `rental_end_real` passes. Current edge function only handles Geaccepteerd -> In verhuur. |
    | No auto-derived "Verhuurstatus" | Trailer status should be computed from active contracts. Currently manually set. |

    **PRD-specified contract status flow:**

    ```mermaid
    graph LR
      A[Aangemaakt] --> B[Verzonden]
      B --> C[Geaccepteerd]
      B --> G[Geweigerd]
      C --> D[In verhuur]
      D --> E[Te controleren]
      E --> F[Afgerond]
      E --> H[Schadeverwerking]
      H --> F
    ```

    <Callout kind="info">
      The dashed path from **Te controleren** to **Schadeverwerking** is the missing state. Currently the system goes directly from Te controleren to Afgerond, skipping damage processing entirely.
    </Callout>
  </Expandable>

  <Expandable title="4.6 Day invoicing" default-open="false">
    <Callout kind="success">
      **Status: Fully implemented.** Overlap calculation, non-driving day deduction, discount on rental only, forfait based on total contract duration all correct.
    </Callout>
  </Expandable>

  <Expandable title="4.7 Month invoicing" default-open="false">
    <Callout kind="success">
      **Status: Mostly implemented.** Pro-rata with `ceilTo2Decimals(daysUsed / daysInMonth)` correct. Uses generic period locks instead of month-specific interval tracking (functionally equivalent but structurally different from PRD).
    </Callout>
  </Expandable>

  <Expandable title="4.8 Double billing prevention gaps" default-open="false">
    | Unit | Status | Gap |
    |------|--------|-----|
    | Day | Implemented | Period locks working, race condition guard present |
    | Month | Partial | Uses generic period locks, not month-specific intervals |
    | KM | **Not implemented** | `invoice_km_lock` table exists but never populated |
    | Exact export idempotency | Not implemented | No idempotency key; retry may create duplicates |
  </Expandable>
</ExpandableGroup>

---

## 5. UI/UX gaps

<ExpandableGroup>
  <Expandable title="5.1 Planning (FR-PLAN-001-008)" default-open="false">
    | Feature | PRD Ref | Status | Gap |
    |---------|---------|--------|-----|
    | Period selection 1/2/3 months + custom | FR-PLAN-001 | Partial | Date range picker exists but no preset buttons (1m/2m/3m) |
    | Zoom +/- buttons | FR-PLAN-002 | Missing | Zoom is auto-calculated from period span. No manual zoom controls. |
    | Trailer grouping by type and/or company | FR-PLAN-003 | Partial | Groups by trailer type. No company grouping toggle. |
    | Event click -> popup -> "toon meer" | FR-PLAN-004 | Implemented | Popup with navigate/refuse/delete actions |
    | Offer as "optie" | FR-PLAN-005 | Implemented | Striped pattern for sent offers without linked contract |
    | Post-drop-off yellow highlight | FR-PLAN-007 | Implemented | Yellow row for "Te controleren" and damage |
    | Inspection milestone | FR-PLAN-008 | Implemented | Shield icons in left panel |
    | Conflict warning (not hard block) | KS7-KS13 | Implemented | Warning popup, user can confirm |
  </Expandable>

  <Expandable title="5.2 Fleet (FR-FLEET-001-010)" default-open="false">
    | Feature | PRD Ref | Status | Gap |
    |---------|---------|--------|-----|
    | Display "Referentie - Nummerplaat" | FR-FLEET-001 | Implemented | |
    | Computed "Verhuurstatus vandaag" badge | FR-FLEET-001/003 | **Missing** | Status badge is from dropdown (manual), not computed from active contracts/planning events. |
    | Vlootstatus (lifecycle, time-independent) | FR-FLEET-002 | Implemented | |
    | Visual icons/badges for properties | FR-FLEET-004 | Partial | Some icons present but not comprehensive |
    | Warning icons with tooltip | FR-FLEET-005 | Partial | Inspection warnings exist; missing km and conflict warnings in list |
    | Drag-drop documents with type tagging | FR-FLEET-007 | Implemented | Drop zone with type selection |
    | KM validation (decline block/override) | FR-FLEET-009 | Partial | Decline detection exists; override-with-reason flow unclear |
  </Expandable>

  <Expandable title="5.3 Invoicing (FR-INVP, FR-INV, FR-DEP)" default-open="false">
    | Feature | PRD Ref | Status | Gap |
    |---------|---------|--------|-----|
    | KM proposal red marking for missing data | FR-INVP-003 | **Missing** | KM invoicing not implemented |
    | Multiselect batch generation | FR-INVP-004 | Implemented | |
    | Manual invoice (linked to contract) | FR-INV-MAN-001 | Implemented | |
    | Invoice status workflow (new/exported/failed) | FR-INV-002 | Partial | Missing exported/failed statuses |
    | Exact status sync (paid/unpaid) | FR-INV-003 | Not implemented | Field exists but no sync mechanism |
  </Expandable>

  <Expandable title="5.4 Navigation" default-open="false">
    | Feature | PRD Ref | Status | Gap |
    |---------|---------|--------|-----|
    | Tree-structure grouping | KS3-KS4 | **Missing** | Flat sidebar. PRD requires nested groups (e.g., Facturatie -> Voorstellen + Facturen). |
    | Contacts in sidebar | - | **Missing** | Contacts only accessible via customer detail or direct URL. |
    | Admin screens in sidebar | - | **Missing** | No nav items for: Documents library, Communication log, Integrations, Import/Export, Companies, Locations, Users & Roles, Auditlog. |
  </Expandable>

  <Expandable title="5.5 Notifications (FR-NOTIF-001-003)" default-open="false">
    | Feature | PRD Ref | Status | Gap |
    |---------|---------|--------|-----|
    | Standalone inbox page | FR-NOTIF-001 | Missing | Only a sidebar panel on dashboard |
    | Status (new/read/handled) | FR-NOTIF-001 | Missing | No status management for notifications |
    | Filters (type/status/period/owner/company) | FR-NOTIF-001 | Missing | No filtering |
    | Deep link to object | FR-NOTIF-002 | Partial | Links exist in dashboard panel but not in a full inbox context |
  </Expandable>
</ExpandableGroup>

---

## 6. Integration gaps

<ExpandableGroup>
  <Expandable title="6.1 Exact Online API (TR-EXACT-001/002)" default-open="false">
    | Feature | PRD Ref | Status | Gap |
    |---------|---------|--------|-----|
    | Export factuurdata | TR-EXACT-001 | Partial | JSON serialization exists. MVP is client-side JSON download, not API POST. |
    | Foutafhandeling + retry | TR-EXACT-001 | **Missing** | No retry logic, no error queue, no per-record error visibility |
    | Idempotent export | Section 9.3 | **Missing** | No idempotency key. `exactonline_ref` is a simple string, not a dedup key. |
    | External reference storage | TR-EXACT-001 | Partial | `exactonline_ref` field exists but stores self-generated ref, not Exact-returned ID |
    | Status sync (paid/unpaid) | TR-EXACT-002 | **Missing** | No mechanism to pull payment status from Exact |
    | Integration config screen | Bijlage B #22 | **Missing** | No admin UI for Exact connection settings |
  </Expandable>

  <Expandable title="6.2 Transics import (TR-TRANS-001)" default-open="false">
    | Feature | PRD Ref | Status | Gap |
    |---------|---------|--------|-----|
    | Excel upload | TR-TRANS-001 | Implemented | XLSX parsing with `xlsx` library |
    | Column mapping | TR-TRANS-001 | Implemented | Dynamic field mapping UI |
    | Preview + validation | TR-TRANS-001 | Implemented | Decline detection, date validation, duplicates |
    | Import log (persistent) | TR-TRANS-001 | **Missing** | Results are transient; no `import_log` table; no per-record audit trail |
    | Standalone page | Bijlage B #23 | Missing | Currently a modal dialog within fleet |
    | Direct Transics API | TR-TRANS-001 | Not in MVP | PRD acknowledges this is optional/later |
  </Expandable>

  <Expandable title="6.3 Creditworthiness API (FR-CUST-002)" default-open="false">
    | Feature | PRD Ref | Status | Gap |
    |---------|---------|--------|-----|
    | External API check (Companyweb etc.) | FR-CUST-002 | **Missing** | Only a free-text `creditworthiness` field on customer. No API integration. |
    | Result logging (result + date) | FR-CUST-002 | **Missing** | No logging mechanism |
    | Result display on customer detail | FR-CUST-002 | Partial | Field displayed but manually entered |
  </Expandable>

  <Expandable title="6.4 PDF generation (FR-COMM-001, FR-CON-006)" default-open="false">
    | Feature | PRD Ref | Status | Gap |
    |---------|---------|--------|-----|
    | Offerte PDF generation | FR-COMM-001 | **Missing** | Template upload exists but no PDF rendering from template data |
    | Contract PDF generation | FR-CON-006 | **Missing** | Same - template storage works, no PDF output |
    | Attachment to Outlook draft | FR-COMM-001 | Partial | Graph API draft creation exists, but no PDF generation to attach |
  </Expandable>

  <Expandable title="6.5 VIES integration (TR-VIES-001)" default-open="false">
    <Callout kind="success">
      **Status: Fully implemented.** SOAP-based VIES check, address parsing, timeout/retry, UI integration. No gaps.
    </Callout>
  </Expandable>

  <Expandable title="6.6 Outlook integration (TR-OUTLOOK-001)" default-open="false">
    | Feature | PRD Ref | Status | Gap |
    |---------|---------|--------|-----|
    | Generate draft with attachments | TR-OUTLOOK-001 | Implemented | Graph API integration |
    | "Sent" manual marking + logging | TR-OUTLOOK-001, KS14-KS20 | **Missing** | No mechanism to mark a draft as sent. No communication log entry created. |
    | Inschrijvingsbewijs as contract attachment | FR-CON-006 | **Missing** | Contract email exists but does not auto-attach registration certificate document |
  </Expandable>
</ExpandableGroup>

---

## 7. i18n gaps

| Language | Status | Gap |
|----------|--------|-----|
| NL (Dutch) | Implemented | `messages/nl.json` (~41KB) |
| FR (French) | Implemented | `messages/fr.json` (~43KB) |
| EN (English) | **Missing** | No `messages/en.json`. PRD says UI is NL/FR only (MVP), but EN is needed for templates/contacts. |

<ExpandableGroup>
  <Expandable title="7.1 Contact/template language support" default-open="false">
    | Feature | PRD Ref | Status | Gap |
    |---------|---------|--------|-----|
    | Contact language NL/FR/EN | FR-CUST-003, KS14-KS20 | **Missing EN** | `contact_language` enum = `('NL', 'FR')`. EN not in enum. |
    | Templates per language NL/FR/EN | FR-TPL-001 | **Missing EN** | `document_template.language` uses `contact_language` enum (no EN). Templates can only be NL/FR. |
    | Email templates EN | KS14-KS20 | **Missing** | No EN email subject/body parameters seeded. |
  </Expandable>

  <Expandable title="7.2 Locales config" default-open="false">
    Current `i18n/config.ts`:

    ```typescript i18n/config.ts
    export const locales = ["nl", "fr"] as const;
    ```

    Does not include `"en"` even if UI-EN is deferred — the `contact_language` enum and template system need EN independently of UI language.
  </Expandable>
</ExpandableGroup>

---

## 8. Security/RBAC gaps

<ExpandableGroup>
  <Expandable title="8.1 Role model" default-open="false">
    PRD defines 5 roles: Admin, Verhuurmedewerker (commercial), Vlootbeheerder (fleet_manager), Facturatie (accounting), Management (read_only).

    Current implementation uses: `admin`, `commercial`, `accounting`, `fleet_manager`, `read_only`.

    <Callout kind="alert">
      **Gap**: Role names map but "Management" = `read_only` is a semantic mismatch. Management may need KPI/reporting access beyond pure read-only. Requires stakeholder clarification.
    </Callout>
  </Expandable>

  <Expandable title="8.2 Page-level RBAC" default-open="true">
    | Gap | Details |
    |-----|---------|
    | Binary admin check | Most pages only check `isAdmin` for write permissions. The full 5-role matrix in `rbac.ts` is not enforced at the component level. E.g., `accounting` can see offers page (per sidebar) but page only checks `isAdmin` for editing. |
    | Missing module-level write guards | `commercial` should write offers/contracts but not fleet. `fleet_manager` should write fleet but not invoices. Current: admin = full write, non-admin = limited write. |
    | No per-company data segregation in UI | RLS policies exist at DB level, but the UI does not filter data by the user's assigned company. All users see all companies' data in dropdowns and lists. |
  </Expandable>

  <Expandable title="8.3 RLS policy gaps" default-open="false">
    | Gap | Details |
    |-----|---------|
    | Missing `audit_log` RLS | Table doesn't exist yet. When created, needs admin-only write, role-based read. |
    | Missing `communication_log` RLS | Table doesn't exist. Needs appropriate policies. |
    | Missing `import_log` RLS | Table doesn't exist. Needs admin + fleet_manager policies. |
    | Document template RLS inconsistency | Uses direct subquery instead of `get_user_role()` function (migration 000018 vs 000008 pattern). Functionally correct but inconsistent. |
    | No company-scoped RLS | PRD requires multi-company segregation (NFR-SEC-001). Current RLS checks role but not company assignment. Users of one company can read/write data of the other. |
  </Expandable>

  <Expandable title="8.4 Missing security features" default-open="false">
    | Feature | PRD Ref | Status |
    |---------|---------|--------|
    | Pen-test/authorization tests | NFR-SEC-001 | No test suite for cross-company access attempts |
    | GDPR compliance in logs | FR-AUD-001 | No audit log exists; no PII filtering strategy |
    | Session timeout | - | `SESSION_TIMEOUT_MINUTES` parameter exists but enforcement unclear |
  </Expandable>
</ExpandableGroup>

---

## 9. Data integrity gaps

<ExpandableGroup>
  <Expandable title="9.1 NOT NULL constraints vs PRD mandatory fields" default-open="false">
    | Table | Column | PRD Says | Current | Gap |
    |-------|--------|----------|---------|-----|
    | `customer` | `vat_number` | Mandatory | nullable | PRD Bijlage A #3: "Yes". DB allows NULL. |
    | `customer` | `official_name` | Mandatory | nullable | PRD Bijlage A #4: "Yes". DB allows NULL. |
    | `customer` | `street` | Mandatory | nullable | PRD Bijlage A #5: "Yes". DB allows NULL. |
    | `customer` | `number` | Mandatory | nullable | PRD Bijlage A #6: "Yes". DB allows NULL. |
    | `customer` | `postal_code` | Mandatory | nullable | PRD Bijlage A #8: "Yes". DB allows NULL. |
    | `customer` | `city` | Mandatory | nullable | PRD Bijlage A #9: "Yes". DB allows NULL. |
    | `customer` | `country` | Mandatory | nullable | PRD Bijlage A #10: "Yes". DB allows NULL. |
    | `customer` | `vat_percentage` | Mandatory | nullable | PRD Bijlage A #11: "Yes". DB allows NULL. |
    | `customer` | `payment_conditions_id` | Mandatory | nullable | PRD Bijlage A #12: "Yes". DB allows NULL. |

    <Callout kind="info">
      These are deliberately nullable to support the workflow where a customer is created first (name + VAT) and then VIES fills in the rest. A compromise would be to enforce NOT NULL at the application layer (before saving a "complete" customer) rather than at DB level, or add an `is_complete` flag.
    </Callout>
  </Expandable>

  <Expandable title="9.2 Missing unique indexes" default-open="false">
    | Table | Column(s) | PRD Requirement | Status |
    |-------|-----------|----------------|--------|
    | `customer` | `vat_number` | Implied unique (business key) | Index exists (`idx_customer_vat_number`) but **not UNIQUE**. Two customers with same VAT possible. |
    | `km_registration` | `(plate_number, registration_date)` | Implied unique (one reading per day) | No unique constraint. Duplicate entries per day possible. |
    | `invoice` | `invoice_number` | Should be unique per company | Index exists but **not UNIQUE**. Duplicate invoice numbers possible. |
  </Expandable>

  <Expandable title="9.3 Date validation gaps" default-open="false">
    | Validation | PRD Ref | Status | Gap |
    |-----------|---------|--------|-----|
    | Non-driving days within contract period | FR-CON-007 | Implemented | Trigger `trg_ndd_within_contract_period` validates server-side. |
    | Non-productive period overlap | FR-FLEET-010 | Implemented | EXCLUDE constraint prevents overlap per trailer. |
    | KM monotonic increase | FR-FLEET-009 | Partial | Validation exists in import utils but no DB-level constraint. Manual km entry in UI may not enforce. |
    | Contract period overlap per trailer | FR-CON-003 | Partial | Warning shown in UI (planning) but no server-side EXCLUDE constraint. |
  </Expandable>

  <Expandable title="9.4 Cascade/referential integrity" default-open="false">
    | Relationship | Current | Concern |
    |-------------|---------|---------|
    | `contract.offer_id` -> `offer` | No CASCADE | Deleting an offer with linked contracts leaves orphan reference. Should be RESTRICT. |
    | `invoice.contract_id` -> `contract` | nullable (since migration 000014) | Invoices can exist without contracts. PRD says "facturen moeten altijd gelinkt zijn aan een contract" (FR-INV-MAN-001). |
  </Expandable>
</ExpandableGroup>

---

## 10. Contradictions and ambiguities

These findings require stakeholder decisions before implementation.

<ExpandableGroup>
  <Expandable title="10.1 Customer-Contact relationship: 1:N vs M:N" default-open="false">
    - **PRD**: Bijlage A lists a `customer_contact` linking table (implying M:N).
    - **Current**: `contact.customer_id` FK makes it 1:N (contact belongs to exactly one customer).
    - **Decision needed**: Can one contact serve multiple customers? If not, current 1:N is correct and PRD data dictionary is misleading.
  </Expandable>

  <Expandable title="10.2 Invoice-Contract nullability" default-open="false">
    - **PRD** (FR-INV-MAN-001): "facturen moeten altijd gelinkt zijn aan een contract"
    - **Current**: `invoice.contract_id` is nullable (migration 000014 made it optional for customer grouping).
    - **Decision needed**: Should standalone invoices be allowed? If not, restore NOT NULL constraint.
  </Expandable>

  <Expandable title="10.3 Deposit/advance: 1 invoice vs 2 invoices" default-open="false">
    - **PRD** (FR-DEP-001): "Indien beide gevraagd: 1 factuur met 2 factuurlijnen"
    - **Current**: Creates 2 separate invoices (one for deposit, one for advance).
    - **Decision needed**: Confirm PRD is correct (1 invoice with 2 lines). This affects invoice numbering, Exact Online mapping, and accounting treatment.
  </Expandable>

  <Expandable title="10.4 Negative line convention" default-open="false">
    - **PRD** (FR-DEP-003): "negatief aantal (qty < 0) en positieve unit price"
    - **Current**: `qty: 1, price: -amount`
    - **Decision needed**: Which convention does Exact Online / Peppol require? PRD is explicit about `qty < 0, price > 0` for compatibility.
  </Expandable>

  <Expandable title="10.5 Verhuurstatus: computation vs manual status" default-open="false">
    - **PRD** (FR-FLEET-001/003, KS7-KS13): Verhuurstatus is "tijdsafhankelijk, op datum X afgeleid uit planning-events".
    - **Current**: Trailer status is a manually-set dropdown value.
    - **Decision needed**: Should the system automatically compute rental status from active contracts/planning events (PRD intent), or keep manual status with a separate computed badge?
  </Expandable>

  <Expandable title="10.6 Contract status auto-transitions" default-open="false">
    **PRD** (FR-CON-005) implies multiple auto-transitions:
    - Geaccepteerd -> In verhuur (when start date <= today) — **implemented** via edge function
    - In verhuur -> Te controleren (after real end date) — **not implemented**
    - Te controleren -> Schadeverwerking (if damage) — **not implemented**, state doesn't exist

    **Decision needed**: Should all these be auto-transitions or manual? Edge function currently only handles the first one.
  </Expandable>

  <Expandable title="10.7 Factuurnummering: Internal vs Exact" default-open="false">
    - **PRD** (FR-INVNUM-001, open punt): "Tool bewaart intern factuurnummer en Exact-factuurnummer"
    - **Current**: `invoice_number` (internal, auto-generated per company) + `exactonline_ref` (self-generated `EOL-{number}`).
    - **Decision needed**: How does Exact Online assign its own number? Does the tool need to receive and store it? What happens if numbers diverge?
  </Expandable>

  <Expandable title="10.8 PDF generation technology" default-open="false">
    - **PRD** (FR-COMM-001, FR-CON-006): Offerte/contract PDF generation from templates with data merge.
    - **Current**: Template upload/storage works, but no PDF generation engine.
    - **Decision needed**: Which PDF library? Options: puppeteer/chromium (HTML->PDF), pdf-lib, react-pdf, or server-side generation. This affects template format (HTML vs DOCX vs custom).
  </Expandable>

  <Expandable title="10.9 Notification triggers: Real-time vs batch" default-open="false">
    - **PRD** (FR-NOTIF-001, FR-SET-001): Parameters trigger notifications (inspection X days, follow-up sent > X days).
    - **Current**: `notification_log` table exists, `notifications.ts` has logic for checking conditions, but execution model is unclear.
    - **Decision needed**: Should notifications be generated by a cron job (Supabase Edge Function on schedule), by database triggers, or by application-level event handlers?
  </Expandable>

  <Expandable title="10.10 Outlook: Desktop vs web" default-open="false">
    - **PRD** (Section 12, open punt): "Technische aanpak voor Outlook draft (desktop vs web)"
    - **Current**: Microsoft Graph API (web-based drafts in cloud mailbox).
    - **Decision needed**: Is Graph API (web/cloud) sufficient, or do users expect desktop Outlook integration? Graph API creates drafts in cloud mailbox visible in Outlook Web and Desktop.
  </Expandable>

  <Expandable title="10.11 STAS as Invoice-To" default-open="false">
    - **PRD** (FR-CON-004): "STAS kan ook gekozen worden (bv. garantie)"
    - **Current**: `invoice_to_id` FK points to `customer` table.
    - **Decision needed**: Is STAS a customer record in the system, or does it need special handling? If it's just a customer record, current schema works. If STAS is a special entity (the parent company), it may need distinct treatment.
  </Expandable>

  <Expandable title="10.12 Repair order status sync" default-open="false">
    - **PRD** (TR-REPAIR-001, Section 12 open punt): "Synchronisatie van repair order status: welke statussen zijn beschikbaar uit externe tool en hoe vaak syncen."
    - **Current**: Only `repair_order_ref` text field.
    - **Decision needed**: Which external repair order system is used? What statuses are available? Is polling needed or manual entry sufficient?
  </Expandable>
</ExpandableGroup>

---

## Requirement coverage matrix

Summary of Must/MVP requirements from PRD sections 6.A-6.I and their implementation status.

### 6.A Dashboard and notifications

| ID | Requirement | Status |
|----|------------|--------|
| FR-DASH-001 | KPI tiles with counts | Implemented |
| FR-DASH-002 | KPI click -> filtered list | Implemented |
| FR-DASH-003 | Alerts list (Should) | Partial — Activity stream exists but not a priority-sorted alerts list |
| FR-NOTIF-001 | Notification inbox with status/filters | Not implemented — Sidebar panel only |
| FR-NOTIF-002 | Deep link from notification | Partial — Links exist but no full inbox |

### 6.B Planning

| ID | Requirement | Status |
|----|------------|--------|
| FR-PLAN-001 | Timeline with period selection | Partial — Date range but no 1/2/3 month presets |
| FR-PLAN-002 | Zoom +/- buttons (Should) | Not implemented — Auto-zoom only |
| FR-PLAN-003 | Group by type/company + filters | Partial — Type grouping yes, company grouping no |
| FR-PLAN-004 | Click -> popup -> detail | Implemented |
| FR-PLAN-005 | Offers as "optie" | Implemented |
| FR-PLAN-006 | Contract status -> planning | Implemented |
| FR-PLAN-007 | Post-drop-off yellow highlight | Implemented |
| FR-PLAN-008 | Inspection milestone | Implemented |

### 6.C Fleet

| ID | Requirement | Status |
|----|------------|--------|
| FR-FLEET-001 | Display name + Verhuurstatus computed | Partial — Display name yes, computed badge no |
| FR-FLEET-002 | Vlootstatus lifecycle | Implemented |
| FR-FLEET-003 | Verhuurstatus time-dependent | Not implemented — Not computed |
| FR-FLEET-004 | Visual icons/badges (Should) | Partial |
| FR-FLEET-005 | Warning icons with tooltip | Partial |
| FR-FLEET-006 | Trailer detail tabs | Implemented |
| FR-FLEET-007 | Drag-drop documents with type | Implemented |
| FR-FLEET-008 | Inspection warnings | Implemented |
| FR-FLEET-009 | KM validation (decline/override) | Partial |
| FR-FLEET-010 | Non-productive period overlap | Implemented |

### 6.D Customers and contacts

| ID | Requirement | Status |
|----|------------|--------|
| FR-CUST-001 | VIES check + auto-fill | Implemented |
| FR-CUST-002 | Creditworthiness API | Not implemented |
| FR-CUST-003 | Contact language NL/FR/EN | Partial — NL/FR only |
| FR-CUST-004 | VAT% + payment conditions defaults | Implemented |

### 6.E Offers

| ID | Requirement | Status |
|----|------------|--------|
| FR-OFFER-001 | Internal/external description, due date | Implemented |
| FR-OFFER-002 | Status flow (created->sent->approved/rejected) | Implemented |
| FR-OFFER-003 | Company + template per language | Partial — No EN templates |
| FR-OFFER-004 | Unit pricing, discount on rental only | Implemented |
| FR-OFFER-005 | Trailer requirements filter (Should) | Implemented |
| FR-COMM-001 | Mail offerte (Outlook draft + PDF) | Partial — Draft yes, PDF generation no, sent marking no |

### 6.F Contracts

| ID | Requirement | Status |
|----|------------|--------|
| FR-CON-001 | Create from offer or scratch | Implemented |
| FR-CON-002 | Trailer required, estimated dates required | Implemented |
| FR-CON-003 | Conflict warning (not hard block) | Implemented |
| FR-CON-004 | Invoice-to (default customer) | Implemented |
| FR-CON-005 | Status flow (incl. schadeverwerking) | Partial — Missing schadeverwerking state |
| FR-CON-006 | Mail contract (draft + PDF + inschrijvingsbewijs) | Partial — Draft yes, PDF no, inschrijvingsbewijs attachment no |
| FR-CON-007 | Non-driving days (unit=day only) | Implemented |
| FR-CON-008 | KM per non-driving day + threshold | Partial — Threshold parameter exists, red marking implementation unclear |
| FR-CON-009 | Post-drop-off check + damage + repair | Partial — Boolean fields on contract, no dedicated table |

### 6.G Invoicing

| ID | Requirement | Status |
|----|------------|--------|
| FR-INVP-001 | Proposals per unit/period | Partial — Day/month only, no KM |
| FR-INVP-002 | Proposal line details | Implemented (for day/month) |
| FR-INVP-003 | KM red marking for missing data | Not implemented |
| FR-INVP-004 | Batch generate from proposals | Implemented |
| FR-INVP-005 | NDD not applicable for km/month | Implemented |
| FR-INV-002 | Status workflow (new/exported/failed) | Partial — Missing exported/failed |
| FR-INV-003 | Exact status sync (Should) | Not implemented |
| FR-INV-004 | Double billing prevention | Partial — Day yes, month partial, km no |
| FR-DEP-001 | Deposit+advance combined invoice | Not implemented — Creates 2 separate invoices |
| FR-DEP-002 | Advance due date calculation | Not implemented — Wrong calculation |
| FR-DEP-003 | Negative lines (qty<0, price>0) | Not implemented — Wrong convention |
| FR-DEP-004 | Saldo only from real invoices | Not implemented — No distinction |
| FR-INV-MAN-001 | Manual invoice (linked to contract) | Implemented |

### 6.H Documents, communication, audit

| ID | Requirement | Status |
|----|------------|--------|
| FR-DOC-001 | Drag-drop upload on all tabs | Implemented |
| FR-DOC-002 | Global document library | Not implemented |
| FR-CLOG-001 | Communication log | Not implemented |
| FR-AUD-001 | Audit log with filters + before/after | Not implemented |

### 6.I Integrations and admin

| ID | Requirement | Status |
|----|------------|--------|
| TR-EXACT-001 | Exact export with retry | Partial — Export exists, no retry |
| TR-EXACT-002 | Exact API sync (Should) | Not implemented |
| TR-OUTLOOK-001 | Outlook draft + logging | Partial — Draft yes, no sent logging |
| TR-VIES-001 | VIES validation | Implemented |
| TR-TRANS-001 | Transics import with log | Partial — Import exists, no persistent log |
| TR-REPAIR-001 | Repair order link + status | Partial — Text ref only |
| FR-SET-001 | Parameters screen | Implemented |
| FR-MD-001 | Dropdown manager | Implemented |
| FR-TPL-001 | Template management | Implemented |
| FR-ORG-001 | Company + location management | Not implemented |
| SEC-RBAC-001 | Role-based access | Partial — Sidebar filtering yes, granular per-module write no |

---

## Priority summary

### Critical (Must/MVP, not implemented)

<Callout kind="danger">
  These items are Must/MVP requirements that are entirely missing from the current implementation and should be prioritized first.
</Callout>

<Steps>
  <Step title="KM invoicing" icon="gauge" titleType="h3">
    Entire billing unit missing. The `generateInvoiceProposals` function only accepts `unitType: "day" | "month"`. KM is entirely excluded.

    **PRD refs**: FR-INVP-001, Section 7.4
  </Step>

  <Step title="Creditworthiness API" icon="shield-check" titleType="h3">
    No external integration for credit checks. Only a free-text `creditworthiness` field on customer exists.

    **PRD ref**: FR-CUST-002
  </Step>

  <Step title="Audit log" icon="scroll-text" titleType="h3">
    No `audit_log` table, no viewer screen, no before/after value tracking.

    **PRD ref**: FR-AUD-001
  </Step>

  <Step title="Communication log" icon="message-square" titleType="h3">
    No tracking of Outlook draft creation, sent marking, or per-offerte/contract communication log.

    **PRD ref**: FR-CLOG-001
  </Step>

  <Step title="Global document library" icon="library" titleType="h3">
    Documents only attached per-entity. No global cross-search library with filters.

    **PRD ref**: FR-DOC-002
  </Step>

  <Step title="Notification inbox" icon="bell" titleType="h3">
    No standalone inbox page with status management, filters, or deep links.

    **PRD ref**: FR-NOTIF-001
  </Step>

  <Step title="User/role management" icon="users" titleType="h3">
    `user_profile` table exists but no admin UI for managing users and roles.

    **PRD ref**: SEC-RBAC-001
  </Step>

  <Step title="Company/location management" icon="building" titleType="h3">
    Companies and locations used in dropdowns but no admin CRUD management UI.

    **PRD ref**: FR-ORG-001
  </Step>

  <Step title="Contact language enum missing EN" icon="globe" titleType="h3">
    `contact_language` enum is `('NL', 'FR')` only. EN is missing, blocking EN templates and contacts.

    **PRD ref**: FR-CUST-003
  </Step>
</Steps>

### High (Must/MVP, partially implemented)

<Callout kind="alert">
  These items exist in some form but have significant gaps that need to be addressed.
</Callout>

| # | Item | PRD Ref |
|---|------|---------|
| 10 | Deposit/advance: combined invoice + due date + negative line convention | FR-DEP-001-004 |
| 11 | Contract status: Schadeverwerking state | FR-CON-005 |
| 12 | Invoice status: exported/failed | FR-INV-002 |
| 13 | Computed Verhuurstatus badge | FR-FLEET-001/003 |
| 14 | PDF generation for offers/contracts | FR-COMM-001, FR-CON-006 |
| 15 | Outlook sent marking + logging | TR-OUTLOOK-001 |
| 16 | Exact export retry + idempotency | TR-EXACT-001 |
| 17 | Transics import log persistence | TR-TRANS-001 |

### Medium (Should/MVP or structural)

| # | Item | PRD Ref |
|---|------|---------|
| 18 | Planning zoom +/- buttons | FR-PLAN-002 |
| 19 | Tree-structure navigation | KS3-KS4 |
| 20 | Standalone screens: Keuringen overview, KM overview, Import/Export, Integrations, Service orders | Various |
| 21 | Granular RBAC per module (not just admin/non-admin) | SEC-RBAC-001 |
| 22 | Company-scoped RLS | NFR-SEC-001 |
| 23 | KM yearly allowance calculation | Section 7.1 |
