---
title: "Non-driving days"
description: "Register periods when a trailer is not in use to deduct them from day-based invoicing in ARMS."
---

Non-driving days are periods during a rental (such as holidays or downtime) when the trailer is not in use. These periods are deducted from the billable days on day-based invoices, so the customer is not charged for days the trailer sits idle.

> [!info]
> Non-driving days only apply to contracts with the billing unit set to **day**. The tab is not available for month-based or km-based contracts.


## Viewing non-driving days

Open a day-based contract and navigate to the **Non-driving days** tab. You see a table with all registered non-driving periods:

| Column | Description |
|--------|-------------|
| **Start date** | First day of the non-driving period |
| **End date** | Last day of the non-driving period |
| **Duration** | Number of days in the period (calculated automatically) |
| **Km driven** | Total kilometers driven during this period |

## Adding a non-driving period

### Step 1: Open the non-driving days tab

Navigate to the contract detail screen and select the **Non-driving days** tab.

### Step 2: Click Add period

Click the **Add period** button to open the date selection form.

### Step 3: Select start and end dates

Use the date pickers to select the start and end dates for the non-driving period.

    > [!warning]
> Dates outside the contract's rental period are greyed out and cannot be selected. The start date must be on or after the contract start, and the end date must be on or before the contract end.

### Step 4: Save the period

Click **Save** to register the non-driving period. It appears in the table and is automatically included in future invoice calculations.


You can add multiple non-driving periods per contract.

## Km control

For each non-driving period, ARMS checks how many kilometers the trailer was actually driven. This helps you verify that the trailer was truly idle during the claimed period.

### How it works

ARMS looks at km registrations from the [[user-guide/fleet/km-registration|fleet km registration]] records that fall within each non-driving period. It calculates the average daily kilometers driven and compares it against a threshold.

| Metric | Description |
|--------|-------------|
| **Km readings in period** | Km registrations that fall within the non-driving period dates |
| **Total km driven** | Sum of kilometer differences within the period |
| **Average km/day** | Total km driven divided by the number of days |
| **Threshold** | `NON_DRIVING_KM_THRESHOLD` parameter (default: 10 km/day) |

### Red flag indicator

If the average kilometers per day exceeds the threshold, the row displays in **red**. This indicates the trailer was likely still in use during the claimed non-driving period and needs investigation.

> [!warning]
> A red row does not automatically prevent invoicing. It is a visual warning for you to review and verify the non-driving claim with the customer before generating invoices.


### Per-day breakdown

Click the expand arrow on any non-driving period row to see a **per-day breakdown** of kilometers driven. This detailed view shows the interpolated or nearest km reading for each day in the period, helping you identify exactly when the trailer was in use.

## Impact on invoicing

Non-driving days are subtracted from the billable days when ARMS generates day-based invoice proposals. The invoice includes:

- A main rental line for the billable days
- A **negative deduction line** for the non-driving days
- A corresponding negative insurance deduction line

See [[user-guide/invoicing/day-based|Day-based invoicing]] for the full calculation breakdown.

## Related pages

- **[[user-guide/invoicing/day-based|Day-based invoicing]]** — See how non-driving days affect the invoice calculation.

  - **[[user-guide/fleet/km-registration|Km registration]]** — Manage km readings used for the non-driving day verification.
