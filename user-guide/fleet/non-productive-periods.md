---
title: "Non-productive periods"
description: "Record and manage periods when a trailer is unavailable for rental due to maintenance, damage, or other reasons."
---

Non-productive (NP) periods track the times when a trailer is unavailable for rental. You manage NP periods from the Non-productive tab on the [[user-guide/fleet/trailer-details|trailer detail screen]], or directly from the [[user-guide/planning/creating-np-periods|planning view]].

## NP period list

The NP period list shows all recorded downtime for the trailer.

| Column | Description |
|--------|-------------|
| **Start date** | First day the trailer is unavailable |
| **End date** | Last day the trailer is unavailable |
| **Reason** | Category for the downtime (see below) |
| **Duration** | Calculated number of days between start and end date |

## Reason categories

Each NP period must be assigned a reason from the following categories:

| Reason | When to use |
|--------|-------------|
| **Damage** | Trailer is out of service due to damage or awaiting repair |
| **Inspection** | Trailer is undergoing a scheduled technical inspection |
| **Maintenance** | Routine or preventive maintenance work |
| **Seasonal storage** | Trailer is stored during an off-peak period |

> [!info]
> Administrators can configure additional reason categories through the [[user-guide/administration/parameters|Parameters]] module.


## Adding an NP period

### Step 1: Open the NP period form

Click **Add NP period** on the Non-productive tab. The form opens with date and reason fields.

### Step 2: Set the start and end dates

Select the **Start date** and **End date** for the period. The start date must be before the end date.

### Step 3: Select a reason

Choose the appropriate reason from the dropdown menu.

### Step 4: Save the NP period

Click **Save** to record the period. The duration is calculated automatically.


## Validation rules

ARMS validates every NP period before saving:

- **Start date must be before end date** - The system rejects periods where the start date is on or after the end date.
- **No overlap with active contracts** - An NP period cannot overlap with an active rental contract for the same trailer. If a conflict exists, an error message appears showing the conflicting contract reference and its dates.

> [!warning]
> If you see a contract conflict error, check the [[user-guide/fleet/trailer-details#tab-contracts|Contracts tab]] on the trailer detail screen to review the overlapping contract before adjusting your NP period dates.


## NP periods on the planning timeline

NP periods appear as gray bars on the [[user-guide/planning/reading-timeline|planning timeline]]. You can also [[user-guide/planning/creating-np-periods|create NP periods directly from the planning view]].

## Related pages

- **[[user-guide/planning/overview|Planning overview]]** — See NP periods in the timeline context.

  - **[[user-guide/planning/creating-np-periods|Create from planning]]** — Add NP periods directly from the planning view.
