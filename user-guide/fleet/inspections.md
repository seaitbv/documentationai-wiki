---
title: "Inspections"
description: "Track and manage technical inspections for your trailers, including expiry warnings and status monitoring."
---

Every rental trailer must undergo periodic technical inspections. The Inspections tab on the [[user-guide/fleet/trailer-details|trailer detail screen]] lets you track all inspection records and monitor upcoming expiry dates.

## Inspection list

The inspection list displays all inspections for a trailer in chronological order.

| Column | Description |
|--------|-------------|
| **Valid from** | Start date of the inspection validity period |
| **Valid to** | End date of the inspection validity period |
| **Status** | Active, Expired, or Future |
| **Remaining days** | Calculated number of days until expiry (`valid_to` minus today) |

## Color coding

Each inspection row is color-coded based on its expiry status:

| Color | Condition | Meaning |
|-------|-----------|---------|
| Red | `valid_to` is in the past | Inspection has expired |
| Orange | `valid_to` is within the warning threshold | Inspection is expiring soon |
| Green | `valid_to` is beyond the warning threshold | Inspection is valid |

> [!info]
> The warning threshold is controlled by the **INSPECTION_WARNING_DAYS** parameter. When an inspection's expiry date falls within this number of days from today, it displays in orange. Your administrator can adjust this value in the [[user-guide/administration/parameters|Parameters]] module.


## Adding a new inspection

### Step 1: Open the inspection form

Click **Add inspection** on the Inspections tab. The inspection form opens.

### Step 2: Enter the validity dates

Set the **Valid from** date (when the inspection starts) and the **Valid to** date (when it expires).

### Step 3: Save the inspection

Click **Save** to add the inspection record. The list updates with the new entry and the header card reflects the updated inspection date.


## Editing an inspection

You can edit only the most recent active inspection. Older or expired inspections are read-only to preserve the audit trail.

### Step 1: Select the inspection

Click the edit action on the most recent active inspection row.

### Step 2: Update the dates

Modify the **Valid from** or **Valid to** dates as needed.

### Step 3: Save your changes

Click **Save** to apply the updated dates.


> [!warning]
> Expired inspections affect the trailer's status in the [[user-guide/fleet/overview|fleet overview]]. An expired inspection displays the inspection column in red, making it easy to identify trailers that need urgent attention.


## Inspection status on the fleet overview

The **Inspection** column in the fleet list shows the `valid_to` date of the active inspection. You can filter the fleet list by inspection status:

- **All** - Shows all trailers regardless of inspection status
- **Expired** - Shows only trailers with expired inspections
- **Expiring soon** - Shows trailers within the warning threshold
- **Valid** - Shows trailers with valid inspections

## Related pages

- **[[user-guide/fleet/overview|Fleet overview]]** — Filter the fleet list by inspection status.

  - **[[user-guide/planning/reading-timeline|Planning timeline]]** — See inspection milestones on the planning view.
