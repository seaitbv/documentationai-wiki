---
title: "Invoice proposals"
description: "Generate and review invoice proposals in ARMS before creating effective invoices."
---

Invoice proposals are calculated billing overviews based on your active contracts. You review and select proposals before turning them into effective invoices. This two-step process gives you full control over what gets invoiced.

## Selection bar

Before generating proposals, configure the invoice run using the selection bar at the top of the screen.

| Field | Type | Description |
|-------|------|-------------|
| **Unit type** | Radio/dropdown | Choose one: day, month, or km. Each run covers a single unit type. |
| **Start date** | Date picker | The start of the billing period (for day and km unit types) |
| **End date** | Date picker | The end of the billing period (for day and km unit types) |
| **Month / Year** | Calendar selector | The billing month (for month unit type only; replaces start/end date) |
| **Company** | Multi-select | Atrac, Urbain, or both |
| **Customer** | Lookup (optional) | Filter proposals for a specific customer |

> [!tip]
> Run proposals per unit type separately. A day-based run only shows day-based contracts, a month-based run only shows month-based contracts, and so on.


## Generating proposals

### Step 1: Configure the selection bar

Select the unit type, date range or month, and company. Optionally filter by customer.

### Step 2: Click Generate overview

Click the **Generate overview** button. ARMS calculates the billing amounts for all matching contracts and displays them in a results table.

### Step 3: Review the proposals

Review each row for correctness. Check the status indicators to identify contracts that have already been partially or fully invoiced.

### Step 4: Select and invoice

Select one or more rows using the checkboxes, then click **Generate invoice(s)** to create the effective invoices.

    > [!info]
> ARMS groups selected proposals by customer. One invoice is created per customer per run.


## Anti-double invoicing

ARMS prevents you from invoicing the same period or kilometer range twice. Before displaying the proposals, the system checks the `Invoice_Period_Lock` and `Invoice_Km_Lock` tables for each contract.

| Scenario | Visual indicator | Meaning |
|----------|-----------------|---------|
| Not yet invoiced | Normal row | Full amount is available for invoicing |
| Partially invoiced | Warning indicator with details | Part of the period or km range has already been invoiced. The already-invoiced portion is excluded from the calculation. |
| Fully invoiced | Blocked indicator | The entire period or km range has been invoiced. No amount is available. |

> [!info]
> When a proposal shows as partially invoiced, ARMS displays the already-invoiced date range or km range so you can verify what has been billed previously.


## Proposal columns by unit type

The proposal table shows different columns depending on the unit type. See the detailed calculation pages for the full column breakdown:

- [[user-guide/invoicing/day-based|Day-based invoicing]] -- billable days, non-driving deductions, forfait logic
- [[user-guide/invoicing/month-based|Month-based invoicing]] -- pro-rata months, partial period calculations
- [[user-guide/invoicing/km-based|Km-based invoicing]] -- driven kilometers, km readings, data warnings

## Creating invoices from proposals

When you click **Generate invoice(s)**, ARMS:

1. Validates that the selected rows belong to the same customer (one invoice per customer)
2. Generates the invoice lines based on the calculation for the selected unit type
3. Registers the invoiced period or km range in the lock tables to prevent double billing
4. Creates the invoice with status "Created" on the [[user-guide/invoicing/managing-invoices|effective invoices]] tab

## Related pages

- **[[user-guide/invoicing/day-based|Day-based invoicing]]** — Day-based calculation details including forfait and non-driving deductions.

  - **[[user-guide/invoicing/month-based|Month-based invoicing]]** — Month-based pro-rata calculations.

  - **[[user-guide/invoicing/km-based|Km-based invoicing]]** — Km-based calculation using odometer readings.
