---
title: "Fleet overview"
description: "View, filter, and manage your entire trailer fleet from the fleet list screen in ARMS."
---

The fleet overview is your central hub for managing all rental trailers. It displays every trailer in a searchable, filterable list with key information visible at a glance.

## Fleet list columns

The fleet list displays the following columns for each trailer:

| Column | Description |
|--------|-------------|
| **Ref - Plate** | Combined trailer reference and plate number (e.g., "K01 - QAMD180") |
| **Nickname** | The trailer's nickname for easy identification |
| **Type** | Trailer type (e.g., tipper, walking floor) |
| **Company** | The owning entity: Atrac or Urbain |
| **Location** | The designated pick-up location |
| **Status** | Color-coded status badge (see below) |
| **Inspection** | Expiry date of the active inspection, with color warnings |
| **Current contract** | Link to the active contract, if applicable |

## Status badges

Each trailer displays a color-coded status badge indicating its current state:

| Status | Color | Meaning |
|--------|-------|---------|
| Active | Green | Trailer is available for rental |
| Rented | Blue | Trailer is currently under an active contract |
| To check | Yellow | Trailer requires inspection after return |
| End-of-life | Dark gray | Trailer is permanently retired from the fleet |
| Sold | Gray | Trailer has been sold and removed from operations |

> [!info]
> Status changes between states follow specific rules and validations. See [[user-guide/fleet/status-changes|Status changes]] for the full transition diagram.


## Filtering the fleet list

Use the filter bar above the list to narrow down the trailers you see. You can combine multiple filters simultaneously.

| Filter | Options |
|--------|---------|
| **Status** | Multi-select: Active, Rented, To check, End-of-life, Sold |
| **Company** | Atrac or Urbain |
| **Trailer type** | Dropdown with all configured trailer types |
| **Pick-up location** | Dropdown with all locations |
| **Inspection** | All, Expired, Expiring soon, Valid |
| **Search bar** | Searches by reference, plate number, nickname, or chassis number |

> [!tip]
> Use the inspection filter set to "Expired" or "Expiring soon" to quickly find trailers that need attention before their inspection lapses.


## Actions

### Add a new trailer

### Step 1: Open the add trailer form

Click the **Add trailer** button in the top-right corner of the fleet overview. This opens the trailer creation form.

### Step 2: Fill in the required fields

Enter the trailer's registration details, organization, and properties. Required fields are marked with an asterisk.

### Step 3: Save the trailer

Click **Save** to add the trailer to your fleet. The new trailer appears in the list with an "Active" status.


### Export to Excel

Click the **Export** button to download the current (filtered) list as an Excel file (.xlsx). The export respects all active filters, so you can export a subset of your fleet.

### View trailer details

Click any row in the fleet list to navigate to the [[user-guide/fleet/trailer-details|trailer detail screen]] for that trailer.

## Related pages

- **[[user-guide/fleet/trailer-details|Trailer details]]** — View and edit all information for a specific trailer.

  - **[[user-guide/fleet/status-changes|Status changes]]** — Understand the rules governing trailer status transitions.
