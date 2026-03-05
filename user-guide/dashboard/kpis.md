---
title: "KPI widgets"
description: "Learn what each dashboard KPI widget measures, how it is calculated, and where it navigates when clicked."
---

The KPI widget bar sits below the header on the [[user-guide/dashboard/overview|dashboard]]. It displays 6 clickable widgets in a single row. Each widget shows a **counter** (number) and a **label**. Clicking a widget navigates you to the relevant list view with a pre-applied filter.

## Widget reference

### Active contracts

| Property | Value |
|----------|-------|
| **Counts** | Contracts with status "In rental" |
| **Navigates to** | Contracts list, filtered by status: In rental |

This widget shows how many contracts are currently active. It helps you quickly see the volume of ongoing rental operations.

### Available trailers

| Property | Value |
|----------|-------|
| **Counts** | Trailers with status "Active" that have no active contract |
| **Navigates to** | Fleet list, filtered by: Available |

This widget shows how many trailers in your fleet are ready to be rented out. A trailer must have status "Active" and must not be linked to any contract currently in the "In rental" status.

### Open offers

| Property | Value |
|----------|-------|
| **Counts** | Offers with status "Created" or "Sent" |
| **Navigates to** | Offers list, filtered by: Open |

This widget tracks offers that are still pending a customer response. It includes both newly created offers and offers that have been sent to the customer.

### Expiring offers

| Property | Value |
|----------|-------|
| **Counts** | Offers where `due_date` is within 3 business days from today |
| **Navigates to** | Offers list, filtered by: Expiring |

This widget highlights offers that are approaching or have passed their due date. The calculation uses **business days** (Monday through Friday), so weekends are excluded.

> [!tip]
> The default due date for new offers is calculated using the `OFFER_DUE_DATE_OFFSET_WEEKS` parameter. You can adjust this in [[user-guide/administration/parameters|Parameters]] to change how far ahead the due date is set.


### Inspections expiring

| Property | Value |
|----------|-------|
| **Counts** | Trailers with inspections expiring within the `INSPECTION_WARNING_DAYS` threshold |
| **Navigates to** | Fleet list, filtered by: Inspection attention |

This widget combines both **expired** inspections (already past due) and **expiring** inspections (within the warning threshold). The default warning threshold is 14 days, but your administrator can adjust this through the `INSPECTION_WARNING_DAYS` [[user-guide/administration/parameters|parameter]].

> [!warning]
> Trailers with expired inspections cannot legally be rented. Address expired inspection alerts promptly to avoid fleet downtime.


### To invoice

| Property | Value |
|----------|-------|
| **Counts** | Contracts with uninvoiced periods in the current calendar month |
| **Navigates to** | Invoicing overview -- Proposals |

This widget shows how many contracts have rental periods in the current month that have not yet been invoiced. Use it to ensure all billable periods are captured before month-end.

## How KPI values are calculated

KPI values are calculated in real time when you load the dashboard. The following table summarizes the data source and filter logic for each widget.

| Widget | Data source | Filter condition |
|--------|-------------|-----------------|
| Active contracts | `contracts` table | `status = "In rental"` |
| Available trailers | `trailers` table | `status = "Active"` AND no active contract |
| Open offers | `offers` table | `status IN ("Created", "Sent")` |
| Expiring offers | `offers` table | `due_date <= today + 3 business days` AND open status |
| Inspections expiring | `technical_inspections` table | `valid_to <= today + INSPECTION_WARNING_DAYS` |
| To invoice | `contracts` + `invoices` tables | Uninvoiced periods in current month range |

> [!info]
> KPI counters reflect the current state of your data. If another user creates a contract or resolves an inspection while you are viewing the dashboard, the counters update on your next page load.


## Related pages

- **[[user-guide/dashboard/overview|Dashboard overview]]** — Return to the full dashboard layout and navigation guide.

  - **[[user-guide/administration/parameters|Parameters]]** — Configure thresholds that affect KPI calculations.
