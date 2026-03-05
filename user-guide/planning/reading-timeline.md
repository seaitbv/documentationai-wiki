---
title: "Reading the timeline"
description: "Learn how to interpret the colors, bars, and highlights on the ARMS planning timeline."
---

The planning timeline uses colors, patterns, and highlights to communicate different types of events and their statuses at a glance. This guide explains how to read every visual element on the timeline.

## Event bar colors

Each bar on the timeline represents a specific type of event. The color tells you what kind of event it is.

| Color | Pattern | Event type | Meaning |
|-------|---------|------------|---------|
| Blue | Striped | Quote (option) | A sent quote has reserved this trailer for the displayed period |
| Orange | Solid | Contract - Reserved | A contract exists but the rental has not started yet |
| Red | Solid | Contract - In rental | The trailer is actively rented under this contract |
| Dark gray | Solid | Service order | A service order from an external system is linked to this trailer |
| Light gray | Solid | Non-productive period | The trailer is unavailable due to maintenance, damage, or other reasons |

## Milestone markers

In addition to bars, the timeline shows milestone markers:

| Marker | Meaning |
|--------|---------|
| Flag icon | The expiry date of the trailer's active technical inspection |

> [!tip]
> Use inspection flags to quickly spot trailers whose inspections are expiring during a planned rental period. This helps you schedule inspections proactively.


## Background highlights

The background color of a trailer row provides additional context:

| Background | Meaning | Action needed |
|------------|---------|---------------|
| **Yellow** | Trailer needs attention | A contract is in "To check" status (post-return inspection pending) or damage was found on a recent return |
| **Normal** (white/default) | No attention needed | Inspection is completed or repair order is closed |

> [!warning]
> A yellow background means the trailer requires your review. Check whether a post-return inspection has been completed or whether a damage report needs follow-up.


## Hovering over events

Hover your cursor over any event bar to see a tooltip with summary information, including the event type, reference number, and date range. This gives you quick context without clicking.

## Clicking on events

Click any event bar to open a detail popup showing:

- **Event type and reference** (e.g., "Contract CT-2026-047")
- **Customer name** (for contracts and quotes)
- **Trailer** reference
- **Period** start and end dates
- **Status** of the event

From the popup, you can:

- Click **Show more** to navigate to the full detail screen for that event
- Click **Close** or click outside the popup to dismiss it

## Reading availability

To assess trailer availability for a specific period:

### Step 1: Set the date range

Adjust the period filter to cover the dates you are interested in.

### Step 2: Apply property filters

Filter by trailer type, volume, sheet type, or other critical properties to show only relevant trailers.

### Step 3: Look for gaps

Available trailers show empty (uncolored) space during the target period. Any bar in the period means the trailer is partially or fully unavailable.

### Step 4: Check for yellow backgrounds

Trailers with a yellow background need attention before they can be considered available, even if their timeline shows a gap.


## Quick reference diagram

```mermaid
graph LR
    A["Blue striped"] -->|Quote| B["Option reserved"]
    C["Orange solid"] -->|Contract| D["Reserved, not started"]
    E["Red solid"] -->|Contract| F["In rental"]
    G["Dark gray"] -->|Service| H["External service order"]
    I["Light gray"] -->|NP period| J["Unavailable"]
    K["Flag icon"] -->|Milestone| L["Inspection expiry"]
```

## Related pages

- **[[user-guide/planning/overview|Planning overview]]** — Full guide to the planning screen layout and filters.

  - **[[user-guide/fleet/overview|Fleet overview]]** — Check trailer statuses in the fleet list view.
