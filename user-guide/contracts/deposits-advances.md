---
title: "Deposits and advances"
description: "Understand how deposit and advance amounts are calculated and invoiced in ARMS contracts."
---

Every contract in ARMS includes a deposit (security guarantee) and an advance payment. Both are automatically calculated when you create a contract, but you can adjust them manually before saving.

## Deposit

The deposit is a security amount that protects against potential damage during the rental period. When the contract is completed, ARMS automatically creates a credit note to return the deposit.

| Property | Value |
|----------|-------|
| **Default amount** | 2,000 EUR |
| **Configurable** | Yes, via the `DEPOSIT_DEFAULT_AMOUNT` parameter |
| **Adjustable per contract** | Yes, you can change the amount manually |

> [!info]
> The default deposit amount is set in [[user-guide/administration/parameters|Parameters]]. Your administrator can change this value at any time, and new contracts will use the updated default.


## Advance

The advance is a prepayment based on the contract's billing unit and rental price. ARMS calculates it automatically, but you can override the amount if needed.

### Advance calculation by unit

| Unit | Formula | Example (unit price = 25 EUR) |
|------|---------|-------------------------------|
| **Day** | 30 x unit price | 30 x 25 = **750 EUR** |
| **Month** | 1 x unit price | 1 x 25 = **25 EUR** |
| **Km** | 6,000 x unit price | 6,000 x 25 = **150,000 EUR** |

> [!tip]
> The advance is always recalculated when you change the unit or unit price. If you have manually adjusted the advance, changing these fields resets it to the calculated value.


## Payment tracking

Each contract shows two checkboxes to track payment status:

| Checkbox | Description |
|----------|-------------|
| **Advance invoice paid** | Check this when the customer has paid the advance |
| **Deposit invoice paid** | Check this when the customer has paid the deposit |

These checkboxes are for internal tracking. They do not affect contract status transitions or invoicing logic.

## Automatic invoice creation

When a contract transitions from "Accepted" to "In rental" (which happens automatically when the start date is reached), ARMS creates two invoices:

### Step 1: Advance invoice is created

A new invoice of type **Advance invoice** is created for the advance amount. It appears in the [[user-guide/invoicing/overview|invoice overview]] with status "Created".

### Step 2: Deposit invoice is created

A new invoice of type **Deposit invoice** is created for the deposit amount. It also appears with status "Created".


> [!warning]
> These invoices are created automatically. You do not need to create them manually. Check the [[user-guide/invoicing/overview|invoice overview]] after a contract enters "In rental" to verify they are there.


## Advance offset on subsequent invoices

When the first regular (recurring) invoice is generated for a contract, ARMS checks the remaining advance balance. If there is an unspent advance amount, the system adds a negative line to the invoice to offset the advance:

- **Line description**: "Advance offset"
- **Amount**: Negative (deducted from the invoice total)
- **VAT**: 0%

The offset amount is tracked on the contract so that subsequent invoices are not double-deducted.

See [[user-guide/invoicing/managing-invoices|Managing invoices]] for more details on how advance offsets appear on invoices.

## Deposit credit note at completion

When a contract is marked as "Completed", ARMS automatically creates a **credit note** for the full deposit amount. This credit note is ready for export to Exact Online and appears in the invoice overview.

## Related pages

- **[[user-guide/contracts/lifecycle|Contract lifecycle]]** — See when automatic invoices are triggered in the status flow.

  - **[[user-guide/invoicing/overview|Invoicing overview]]** — View and manage all invoices including advance and deposit invoices.
