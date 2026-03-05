---
title: "Day-based invoicing"
description: "Understand how ARMS calculates day-based invoice proposals, including non-driving deductions and forfait logic."
---

Day-based invoicing calculates billing amounts based on the number of billable days in the selected period, minus any registered [[user-guide/contracts/non-driving-days|non-driving days]]. Short contracts (1-2 days) use a forfait (flat rate) instead of the regular per-day calculation.

## Proposal columns

The day-based proposal table displays the following columns:

| Column | Description |
|--------|-------------|
| **Contract ID** | Link to the contract detail |
| **Customer** | Customer name |
| **Trailer** | Trailer display name |
| **Contract-period overlap** | Start and end date of the overlap between the contract and billing period |
| **Billable days** | Number of days after deducting non-driving days |
| **Non-driving days in period** | Days deducted from the billable total |
| **Unit price (rental)** | The per-day rental price |
| **Discount (%)** | Discount percentage on the rental |
| **Unit price (insurance)** | The per-day insurance price |
| **Net total (excl. VAT)** | Calculated total before VAT |
| **Status** | Normal, partially invoiced, or fully invoiced |

## Calculation logic

ARMS follows this sequence to determine billable days:

### Step 1: Determine effective dates

The system uses the **real dates** (pickup/dropoff) when available. Otherwise, it falls back to **estimated dates**.

    ```
    effective_start = real start date OR estimated start date
    effective_end   = real end date OR estimated end date
    ```

### Step 2: Calculate the overlap

ARMS calculates the overlap between the contract period and the billing period you selected:

    ```
    period_start = MAX(billing start, effective start)
    period_end   = MIN(billing end, effective end)
    ```

    If the period start is after the period end, the contract does not appear in the proposals (no overlap).

### Step 3: Count billable days

```
    overlap_days = (period_end - period_start) + 1
    non_driving_in_period = total non-driving days within the overlap
    billable_days = overlap_days - non_driving_in_period
    ```


## Forfait logic

For very short contracts, ARMS applies a flat-rate (forfait) instead of the standard per-day calculation. The forfait is based on the **total contract duration**, not the billing period.

| Total contract days | Invoicing method | Default amount |
|--------------------|------------------|----------------|
| **1 day** | Forfait per unit | 120 EUR (`FORFAIT_1_DAY` parameter) |
| **2 days** | Forfait per unit | 170 EUR (`FORFAIT_2_DAYS` parameter) |
| **3+ days** | Standard per-day calculation | billable days x unit price x (1 - discount) |

> [!info]
> The forfait amounts are configurable in [[user-guide/administration/parameters|Parameters]]. When a forfait applies, the invoice shows a single line per unit instead of the standard day-based breakdown.


## Generated invoice lines

For a standard day-based contract (3+ days), ARMS generates the following invoice lines:

| Line | Quantity | Unit price | VAT | Discount applies? |
|------|----------|------------|-----|-------------------|
| **Trailer rental -- [period]** | Billable days | Rental unit price | Customer VAT % | Yes |
| **Non-driving days deduction** | -Non-driving days (negative) | Rental unit price | Customer VAT % | Yes |
| **Insurance -- [period]** | Billable days | Insurance unit price | 0% | No |
| **Insurance non-driving deduction** | -Non-driving days (negative) | Insurance unit price | 0% | No |

> [!warning]
> The discount percentage applies **only to rental lines**, never to insurance. Insurance is always invoiced at the full unit price with **0% VAT**.


For forfait contracts (1-2 days), lines 1-2 are replaced by a single forfait line with quantity 1 and the forfait price.

## Example calculation

A contract with the following details:
- Billing period: March 1-31
- Contract period: March 5-25 (21 days overlap)
- Non-driving days: March 10-12 (3 days)
- Unit price rental: 30 EUR/day
- Unit price insurance: 5 EUR/day
- Discount: 10%
- Customer VAT: 21%

**Result:**

| Line | Qty | Price | Discount | VAT | Total |
|------|-----|-------|----------|-----|-------|
| Trailer rental | 21 | 30.00 | 10% | 21% | 567.00 |
| Non-driving deduction | -3 | 30.00 | 10% | 21% | -81.00 |
| Insurance | 21 | 5.00 | -- | 0% | 105.00 |
| Insurance deduction | -3 | 5.00 | -- | 0% | -15.00 |
| | | | | **Subtotal** | **576.00** |

## Related pages

- **[[user-guide/contracts/non-driving-days|Non-driving days]]** — Register and manage non-driving periods on contracts.

  - **[[user-guide/invoicing/proposals|Invoice proposals]]** — Generate and review invoice proposals before creating invoices.
