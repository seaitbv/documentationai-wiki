---
title: "Accounting"
description: "Guide for the Accounting role focused on invoice generation, management, and Exact Online export"
---

## Role overview

As an Accounting user, your primary focus is **invoicing**. You generate invoice proposals, create invoices, and export them to Exact Online. You have read access to customers, offers, and contracts to verify data, but your write access is concentrated in the Invoicing module.

> [!warning]
> MFA (Multi-Factor Authentication) is strongly recommended for the Accounting role due to the financial sensitivity of invoice operations.


## Access matrix

| Module | Access Level | What You Can Do |
|--------|-------------|-----------------|
| Dashboard | Full | View all KPIs and notifications |
| Fleet | Read | View trailer details (no editing) |
| Customers | Read | View customer and contact data (no editing) |
| Offers | Read | View offers (no editing) |
| Contracts | Read | View contract details and linked invoices (no editing) |
| Invoicing | Full | Generate proposals, create invoices, export to Exact Online |
| Planning | -- | Not visible |
| Templates | -- | Not visible |
| Parameters | -- | Not visible |

> [!info]
> You cannot edit customers, offers, or contracts. If you find incorrect data that affects invoicing (wrong VAT%, payment conditions, or pricing), contact the Commercial team or an Administrator to correct it.


## Key responsibilities

- **Invoice proposal generation**: run billing calculations for day, month, and km-based contracts
- **Invoice creation**: select proposals and generate official invoices
- **Invoice review**: verify invoice lines, amounts, VAT, and advance offsets
- **Exact Online export**: export invoices to Exact Online for payment processing
- **Payment tracking**: monitor payment status returned from Exact Online
- **Credit notes**: manage automatic deposit credit notes upon contract completion

## Monthly invoicing workflow

### Step 1: Generate day-based proposals

Open **Invoicing** and go to the **Invoice Proposals** tab.

    1. Select unit type **Day**.
    2. Set the billing period start and end dates (typically the previous month).
    3. Select the company (Atrac, Urbain, or both).
    4. Click **Generate Overview**.

    Review the results. Each row shows the billable days, non-driving day deductions, pricing, and anti-double-invoicing status.

    > [!tip]
> For contracts of 1 or 2 total days, ARMS applies forfait pricing automatically instead of the per-day rate. See [[user-guide/invoicing/day-based|Day-Based Invoicing]] for details.

### Step 2: Generate month-based proposals

Switch unit type to **Month**.

    1. Select the **month and year** to invoice.
    2. Click **Generate Overview**.

    ARMS calculates pro-rata amounts for contracts that start or end mid-month, rounding up to 2 decimal places.

### Step 3: Generate km-based proposals

Switch unit type to **Km**.

    1. Set the billing period.
    2. Click **Generate Overview**.

    > [!warning]
> Rows highlighted in red indicate missing km registration data. Coordinate with the Fleet Manager to ensure km readings are up to date before creating invoices.

### Step 4: Select and create invoices

For each proposal type:

    1. Select the rows to invoice using the checkboxes.
    2. Click **Generate Invoice(s)**.
    3. ARMS creates invoices grouped by customer (one invoice per customer per run).
    4. Invoice lines include rental, insurance, non-driving day deductions, and advance offset where applicable.

### Step 5: Review invoices

Switch to the **Invoices** tab and review newly created invoices:

    - Verify invoice lines and totals
    - Check VAT calculations
    - Confirm advance offset was applied correctly on the first recurrent invoice

### Step 6: Export to Exact Online

For each reviewed invoice:

    1. Click **Export to Exact Online**.
    2. ARMS sends the invoice data to Exact Online.
    3. On success, the invoice status changes to "Exported" and the Exact Online reference is recorded.

    > [!info]
> If the export fails, ARMS displays the error message from Exact Online. Common causes include missing customer mappings or network issues. See [[help/troubleshooting|Troubleshooting]] for solutions.


## Understanding the anti-double-invoicing system

ARMS prevents invoicing the same period or km range twice using lock records:

- **Period locks** (`Invoice_Period_Lock`): track which date ranges have been invoiced for day and month contracts
- **Km locks** (`Invoice_Km_Lock`): track which km ranges have been invoiced for km contracts

When generating proposals, already-invoiced portions are excluded and marked as "Partially invoiced" or "Fully invoiced" in the overview.

## Related guides

- **[[user-guide/invoicing/proposals|Invoice Proposals]]** — Detailed guide on generating and reviewing invoice proposals.

  - **[[user-guide/invoicing/exact-online-export|Exact Online Export]]** — How to export invoices and handle errors.

  - **[[role-guides/workflows/monthly-invoicing|Monthly Invoicing Workflow]]** — Complete monthly invoicing cycle guide.

  - **[[user-guide/invoicing/day-based|Day-Based Invoicing]]** — Calculation details for day-based contracts including forfait pricing.
