---
title: "Creating NP periods from planning"
description: "Add non-productive periods directly from the planning timeline for quick scheduling."
---

In addition to creating non-productive (NP) periods from the [[user-guide/fleet/non-productive-periods|trailer detail screen]], you can add them directly from the planning view. This is convenient when you are reviewing the timeline and need to block out time for a trailer without navigating away.

## Adding an NP period from the planning view

### Step 1: Locate the trailer on the timeline

Find the trailer you want to mark as non-productive in the planning timeline. Use the [[user-guide/planning/overview#filter-zone|filters]] to narrow down the view if needed.

### Step 2: Open the NP period form

Right-click on the trailer's timeline row or use the add action to open the NP period creation form. The dates may be pre-filled based on where you clicked on the timeline.

### Step 3: Set the start and end dates

Enter or adjust the **Start date** and **End date** for the non-productive period. Verify the dates align with the gaps you see on the timeline.

### Step 4: Select a reason

Choose the reason for the downtime from the dropdown:

    | Reason | Use case |
    |--------|----------|
    | **Damage** | Trailer is out of service due to damage |
    | **Inspection** | Scheduled technical inspection |
    | **Maintenance** | Routine or preventive maintenance |
    | **Seasonal storage** | Off-peak storage period |

### Step 5: Save the NP period

Click **Save**. The NP period immediately appears as a light gray bar on the timeline.


## Validation rules

The same validation rules apply whether you create an NP period from the planning view or the trailer detail screen:

- **Start date must be before end date** - The period is rejected if dates are in the wrong order.
- **No overlap with active contracts** - The period cannot overlap with an existing active contract for that trailer.

> [!warning]
> If the system detects an overlap with an active contract, an error message displays the conflicting contract reference and dates. Adjust your NP period dates to avoid the conflict.


> [!tip]
> Creating NP periods from the timeline lets you visually verify there are no scheduling conflicts before saving. You can see existing contracts and other NP periods right next to where your new period will appear.


## Where NP periods appear

NP periods created from the planning view are identical to those created from the trailer detail screen. They appear in both locations:

- **Planning timeline** - As a light gray bar on the trailer's row
- **Trailer detail screen** - In the Non-productive periods tab list

Editing or deleting the NP period from either location updates both views.

## Related pages

- **[[user-guide/fleet/non-productive-periods|NP periods (fleet)]]** — Manage NP periods from the trailer detail screen.

  - **[[user-guide/planning/overview|Planning overview]]** — Full guide to the planning screen.

  - **[[user-guide/planning/reading-timeline|Reading the timeline]]** — Interpret colors and bars on the timeline.
