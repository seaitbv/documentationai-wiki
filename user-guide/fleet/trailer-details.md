---
title: "Trailer details"
description: "View and manage all information for a specific trailer, including registration, properties, inspections, and documents."
---

The trailer detail screen provides a complete view of a single trailer. It is divided into a header card that is always visible and a set of tabs for different categories of information.

## Header card

The header card remains visible at all times and displays:

- **Display name** - The trailer reference and plate number (e.g., "K01 - QAMD180")
- **Nickname** - The trailer's assigned name
- **Status badge** - Color-coded current status
- **Company** - Atrac or Urbain
- **Location** - The designated pick-up location
- **Inspection valid to** - Expiry date with color coding (green, orange, or red)

Two action buttons appear in the header:

- **Edit** - Opens the trailer's fields for editing
- **Change status** - Opens the status transition dialog (see [[user-guide/fleet/status-changes|Status changes]])

## Tab: General

The General tab contains the core registration and organizational data for the trailer.

| Section | Fields |
|---------|--------|
| **Registration** | Plate number, trailer reference, nickname, brand, trailer number, chassis number, first registration date, build year, initial customer |
| **Organization** | Company (Atrac/Urbain), pick-up location |
| **Status and notes** | Current status (dropdown), free-text remarks field |

## Tab: Properties

The Properties tab organizes trailer characteristics into three sections.

### Critical properties

These properties are used when searching for available trailers during quote and contract creation.

| Property | Description |
|----------|-------------|
| **Trailer type** | The main category (e.g., tipper, walking floor) |
| **Volume** | Cargo volume in cubic meters |
| **Sheet type** | Type of cover sheet |
| **Model** | Specific trailer model |
| **Door type** | Type of rear door configuration |

### Extra options

A multiselect dropdown where you can assign additional features to the trailer. Standard options include:

- Floor sheet
- Wash system
- Potato hooks
- Insulated
- Non-insulated

> [!info]
> Administrators can add custom extra options through the [[user-guide/administration/parameters|Parameters]] module.


### Other properties

| Property | Description |
|----------|-------------|
| **Chassis material** | Material of the chassis frame |
| **Rim material** | Material of the wheel rims |
| **Empty weight** | Trailer weight in kilograms |
| **Max weight** | Maximum permitted weight in kilograms |

## Tab: Inspections

Displays all technical inspections for this trailer. See [[user-guide/fleet/inspections|Inspections]] for full details.

## Tab: Non-productive periods

Lists all periods when the trailer was unavailable for rental. See [[user-guide/fleet/non-productive-periods|Non-productive periods]] for full details.

## Tab: Km registration

Shows the complete kilometer reading history. See [[user-guide/fleet/km-registration|Km registration]] for full details.

## Tab: Contracts

Displays all contracts (active and historical) linked to this trailer.

| Column | Description |
|--------|-------------|
| **Contract ID** | Unique contract identifier |
| **Customer** | Customer name |
| **Period** | Contract start and end dates |
| **Status** | Current contract status |
| **Total value** | Contract's total value |

Click any row to navigate to the contract detail screen.

## Tab: Planning

A mini-planning view focused on this trailer only. It shows the same events as the [[user-guide/planning/overview|global planning screen]] but filtered to this specific trailer. The default view covers one month in the past to three months in the future.

## Tab: Documents

Upload and manage files associated with this trailer. See [[user-guide/fleet/documents|Documents]] for full details.

## Editing a trailer

### Step 1: Click the Edit button

Click **Edit** in the header card. The trailer's fields become editable.

### Step 2: Modify the desired fields

Update any fields across the General and Properties tabs. Required fields remain mandatory.

### Step 3: Save your changes

Click **Save** to apply your changes. Click **Cancel** to discard them and return to view mode.


> [!warning]
> Changing the company field may affect which templates and numbering sequences apply to future contracts and invoices for this trailer.


## Related pages

- **[[user-guide/fleet/inspections|Inspections]]** — Manage technical inspection records.

  - **[[user-guide/fleet/non-productive-periods|NP periods]]** — Track non-productive downtime.

  - **[[user-guide/fleet/documents|Documents]]** — Upload and organize trailer files.
