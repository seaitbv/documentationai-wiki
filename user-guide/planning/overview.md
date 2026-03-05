---
title: "Planning overview"
description: "Use the Gantt-style planning timeline to visualize trailer availability, contracts, and non-productive periods."
---

The planning screen is a Gantt-style timeline that gives you a visual overview of your entire fleet's schedule. Each trailer appears as a row, with colored bars representing contracts, non-productive periods, and other events across time.

## Screen layout

The planning screen has three main areas:

- **Filter zone** (top) - Controls which trailers and time period you see
- **Trailer column** (left) - Fixed panel showing trailer identification
- **Timeline** (right) - Horizontally scrollable area displaying events as colored bars

## Filter zone

Use the filters at the top of the screen to control which trailers and time periods are displayed.

| Filter | Type | Default |
|--------|------|---------|
| **Period (From - To)** | Date range picker | Today to today + 1 month |
| **Company** | Multi-select | All |
| **Trailer type** | Dropdown | All |
| **Volume** | Numeric range | No filter |
| **Sheet type** | Dropdown | All |
| **Model** | Dropdown | All |
| **Door type** | Dropdown | All |

> [!tip]
> The filters match the critical trailer properties. Use them to quickly find available trailers that meet specific rental requirements, such as a tipper with a certain volume and sheet type.


Trailers that do not match the active filters are hidden from the view.

## Time scale

The timeline automatically adjusts its column granularity based on the selected period length.

| Period length | Column display |
|---------------|----------------|
| Up to 31 days | Daily columns |
| 32 to 92 days | Weekly columns |
| 93 to 365 days | Monthly columns |
| Over 365 days | Quarterly columns |

## Trailer identification

Each row in the left panel shows:

| Element | Description |
|---------|-------------|
| **Display name** | Trailer reference and plate (e.g., "K01 - QAMD180") |
| **Company badge** | Atrac or Urbain indicator |
| **Pick-up location** | Abbreviated location name |
| **Inspection milestone** | Flag icon on the active inspection's expiry date |

Trailers are grouped by type and sorted by reference within each group.

## Events on the timeline

The timeline displays several types of events as colored bars. See [[user-guide/planning/reading-timeline|Reading the timeline]] for a complete guide to interpreting colors and interactions.

| Event | Color | Description |
|-------|-------|-------------|
| Quote (option) | Blue (striped) | A sent quote reserving this trailer for a period |
| Contract - Reserved | Orange | A contract that is created, sent, or accepted but not yet active |
| Contract - In rental | Red | An active rental contract |
| Service order | Dark gray | A service order from an external system |
| Non-productive period | Light gray | A recorded NP period |
| Inspection milestone | Flag icon | The expiry date of the active inspection |

> [!info]
> Quotes with status "Rejected" or "Created" (not yet sent) do not appear on the timeline. Rejected contracts are also hidden.


## Background highlights

Trailer rows can have a yellow background to indicate items that need attention:

- A contract is in "To check" status (trailer returned, pending inspection)
- Damage was found on a recently returned trailer (`damage_found = true`)

The background returns to normal once the check is completed or the repair order is closed.

## Clicking on events

Click any event bar to open a compact popup showing key details:

- Event type and reference number
- Customer name (for contracts and quotes)
- Trailer reference
- Period dates
- Current status

The popup includes a **Show more** link that navigates to the full detail screen for that event (contract, quote, etc.). Click outside the popup or use the **Close** button to dismiss it.

## Date logic

The timeline uses estimated dates for display when actual start or end dates have not been filled in yet. Once real dates are recorded, the timeline updates automatically.

## Related pages

- **[[user-guide/planning/reading-timeline|Reading the timeline]]** — Learn how to interpret colors, bars, and highlights.

  - **[[user-guide/planning/creating-np-periods|Creating NP periods]]** — Add non-productive periods directly from the planning view.
