---
title: "Invoicing server actions"
description: "Server actions for invoice proposal generation, invoice creation, status management, and Exact Online export"
---

## Overview

The invoicing server actions in `lib/actions/invoicing.ts` implement the billing engine for ARMS. This is the most complex action file, handling proposal generation for both day-based and month-based contracts, invoice creation from proposals, manual invoice line support, status transitions, and export to Exact Online.

## Key functions

### generateInvoiceProposals

Generates billing proposals for active contracts within a specified period. This is the core of the invoicing workflow.

| Property | Value |
|----------|-------|
| Signature | `generateInvoiceProposals(input: GenerateProposalsInput)` |
| Auth | Authenticated read |
| Returns | `{ data: ProposalRow[]; error: string \| null }` |

```typescript
interface GenerateProposalsInput {
  unitType: "day" | "month";
  startDate?: string;        // Required for day billing
  endDate?: string;           // Required for day billing
  month?: number;             // Required for month billing
  year?: number;              // Required for month billing
  companyIds: string[];       // Filter by companies
  customerId?: string;        // Optional customer filter
}
```

**How it works:**
1. Determines the billing period based on `unitType` (date range for day, month range for month)
2. Fetches contracts matching: unit type, company, status "In verhuur" (Active rental), and overlapping rental period
3. For each contract, calculates invoice lines based on rental rates, insurance, and discounts
4. Accounts for non-driving days (day billing) and advance offsets
5. Checks for already-invoiced periods to prevent double billing
6. Returns proposals with a computed status (new, partial, already invoiced)

### createInvoicesFromProposals

Creates actual invoice records from accepted proposals. Groups by customer when applicable.

| Property | Value |
|----------|-------|
| Signature | `createInvoicesFromProposals(input: CreateInvoicesInput)` |
| Auth | `requireAuth()` |
| Returns | `{ data: { created: number }; error: string \| null }` |
| Revalidates | `/invoices` layout |

For each proposal:
1. Generates the next invoice number via the `next_invoice_number` database RPC
2. Calculates the due date from the contract's payment conditions
3. Creates the invoice header and all invoice lines
4. Links the invoice to the contract

### createKmInvoice

Creates a kilometer-based invoice for contracts with `unit = "km"`. These follow a different billing model from day/month invoices.

| Property | Value |
|----------|-------|
| Signature | `createKmInvoice(input: CreateKmInvoiceInput)` |
| Auth | `requireAuth()` |
| Returns | `{ data: { invoice_id: number } \| null; error: string \| null }` |
| Revalidates | `/invoices` layout |

### updateInvoiceStatus

Transitions an invoice through its status workflow using `isInvoiceTransitionAllowed()`.

| Property | Value |
|----------|-------|
| Signature | `updateInvoiceStatus(invoiceId: number, newStatusId: number)` |
| Auth | `requireAuth()` |
| Returns | `{ error: string \| null }` |
| Revalidates | `/invoices` layout |

### exportInvoiceToExactOnline

Validates and serializes an invoice to the Exact Online JSON format for download.

| Property | Value |
|----------|-------|
| Signature | `exportInvoiceToExactOnline(invoiceId: number)` |
| Auth | `requireAuth()` |
| Returns | `{ data: ExactOnlineInvoice \| null; error: string \| null }` |

**Process:**
1. Fetches the invoice with lines and customer VAT number
2. Runs `validateInvoiceForExport()` to check required fields
3. Calls `serializeToExactOnline()` to convert to Exact Online format
4. Returns the JSON object for client-side download

## Calculation utilities

The invoicing actions import calculation functions from `invoicing-utils.ts`:

| Function | Purpose |
|----------|---------|
| `calculateDaysBetween` | Count billable days between two dates |
| `calculateDayInvoiceLines` | Generate lines for day-based contracts |
| `calculateMonthInvoiceLines` | Generate lines for month-based contracts |
| `calculateNonDrivingDaysInPeriod` | Deduct non-driving days from billing |
| `calculateProposalStatus` | Determine if a period is new, partial, or already billed |
| `calculateAdvanceOffsetLine` | Create an offset line for advance payments |
| `calculateInvoiceTotals` | Sum line totals with VAT |
| `getOverlappingLockRanges` | Find already-invoiced date ranges |
| `getMonthDateRange` | Convert month/year to date range |
| `parseDaysFromPaymentCondition` | Extract payment term days |
| `validateManualInvoiceLines` | Validate user-added custom lines |

## Invoice types

The system creates different invoice types at different stages:

| Type | Created by | Description |
|------|-----------|-------------|
| `rental` | Proposal workflow | Standard rental billing |
| `deposit` | Contract acceptance | Security deposit |
| `advance` | Contract acceptance | Advance payment |
| `credit_note` | Contract completion | Deposit refund |
| `km` | Manual creation | Kilometer-based billing |
| `manual` | Manual creation | Custom one-off invoices |
