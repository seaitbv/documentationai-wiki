---
title: "Fleet Manager"
description: "Guide for the Fleet Manager role focused on trailer management, inspections, km registrations, and non-productive periods"
---

## Role overview

As a Fleet Manager, you are responsible for the **physical fleet of trailers**. You manage trailer records, track technical inspections, register kilometer readings, and handle non-productive periods. You have read access to customers, contracts, and the planning timeline to understand how trailers are being used.

## Access matrix

| Module | Access Level | What You Can Do |
|--------|-------------|-----------------|
| Dashboard | Full | View all KPIs and notifications |
| Fleet | Full | Create, edit, manage trailers, inspections, km registrations, NP periods |
| Customers | Read | View customer data (no editing) |
| Offers | -- | Not visible |
| Contracts | Read | View contract details linked to trailers (no editing) |
| Invoicing | -- | Not visible |
| Planning | Read | View the Gantt timeline (no modifications) |
| Templates | -- | Not visible |
| Parameters | -- | Not visible |

> [!info]
> You cannot access Offers, Invoicing, Parameters, or Templates. For changes to trailer dropdown options or system parameters, contact your Administrator.


## Key responsibilities

- **Trailer management**: create and maintain trailer records with accurate properties (type, volume, sheet type, model, door type)
- **Technical inspections**: track inspection validity dates, respond to expiration warnings
- **Km registrations**: record kilometer readings manually or via Excel import
- **Non-productive periods**: register periods when trailers are unavailable (damage, maintenance, seasonal storage)
- **Document management**: upload trailer-related documents (registration certificates, photos, inspection reports)
- **Status management**: update trailer status (Active, To Check, End-of-Life, Sold)

## Daily workflow

### Step 1: Check Dashboard notifications

Start with the Dashboard and focus on fleet-related notifications:

    - **Expired inspections** (red): trailers with expired technical inspections need immediate attention
    - **Expiring inspections** (orange): trailers approaching the inspection warning threshold (default: 14 days)
    - **Missing km registrations** (blue): trailers on km-based contracts without a recent km reading (> 30 days)
    - **Trailers to check** (orange): returned trailers awaiting post-rental inspection

### Step 2: Address inspection alerts

Open **Fleet** and filter on **Inspection: Expiring** or **Inspection: Expired**.

    For each trailer:

    1. Schedule the technical inspection with the inspection center.
    2. After the inspection, open the trailer detail and go to the **Inspections** tab.
    3. Click **Add Inspection** and enter the new valid-from and valid-to dates.
    4. The notification clears automatically once the new inspection record is saved.

    > [!warning]
> A trailer with an expired inspection should not be rented out. Coordinate with the Commercial team if the trailer is on an active offer.

### Step 3: Register km readings

Go to the **Km Registration** tab on trailer details:

    - **Manual entry**: click **Add Registration**, enter the date and km reading.
    - **Excel import**: upload a file with columns for plate number, date, and km reading. ARMS validates that plate numbers exist and km values are non-decreasing.

    > [!tip]
> Regular km registrations are essential for km-based invoicing accuracy. Aim to register readings at least monthly, or more frequently if the Accounting team needs to invoice mid-period.

### Step 4: Manage non-productive periods

When a trailer is taken out of service:

    1. Open the trailer detail and go to the **Non-Productive** tab.
    2. Click **Add Period**.
    3. Enter the start date, end date, and reason (Damage, Inspection, Maintenance, Seasonal Storage).
    4. Save the period.

    > [!warning]
> Non-productive periods cannot overlap with active contracts. ARMS validates this and shows the conflicting contract if there is an overlap.

### Step 5: Check the Planning timeline

Use the **Planning** view (read-only) to see:

    - Which trailers are currently rented, reserved, or available
    - Upcoming inspection milestones (flag icons on the timeline)
    - Non-productive periods (grey blocks)
    - Trailers requiring post-return inspection (yellow background)


## Fleet onboarding checklist

When adding a new trailer to the fleet, ensure you complete all fields:

| Category | Required Fields |
|----------|----------------|
| Registration | Plate number, trailer reference, chassis number, first registration date, construction year |
| Organization | Company (Atrac/Urbain), pick-up location |
| Critical properties | Trailer type, volume (m3), sheet type, model, door type |
| Optional properties | Brand, trailer number, nickname, chassis material, rim material, weights |
| Documents | Registration certificate, photos |
| First inspection | Valid-from and valid-to dates |

See [[role-guides/workflows/fleet-onboarding|Fleet Onboarding Workflow]] for the complete step-by-step process.

## Related guides

- **[[role-guides/workflows/fleet-onboarding|Fleet Onboarding]]** — Complete workflow for adding a new trailer to the fleet.

  - **[[user-guide/fleet/inspections|Inspections]]** — Managing technical inspections and validity tracking.

  - **[[user-guide/fleet/km-registration|Km Registration]]** — Recording and importing kilometer readings.

  - **[[role-guides/workflows/trailer-return|Trailer Return Workflow]]** — The post-return inspection and damage control flow.
