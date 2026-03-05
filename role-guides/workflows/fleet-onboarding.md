---
title: "Fleet Onboarding"
description: "Step-by-step workflow for adding a new trailer to the ARMS fleet, from record creation to availability"
---

## Overview

When a new trailer arrives, you need to register it in ARMS before it can be included in offers, contracts, and the planning timeline. This workflow walks you through the complete onboarding process.

**Role required**: Fleet Manager or Admin

```mermaid
graph LR
    A[Create Trailer Record] --> B[Enter Properties]
    B --> C[Upload Documents]
    C --> D[Add First Inspection]
    D --> E[Trailer Available]
```

## Onboarding steps

### Step 1: Create the trailer record

Navigate to **Fleet** and click **New Trailer**.

    Fill in the registration details:

    | Field | Description | Required |
    |-------|-------------|:--------:|
    | Plate number | License plate (unique identifier) | Yes |
    | Trailer reference | Internal reference, e.g., "K28" (unique) | Yes |
    | Nickname | Optional female name, e.g., "Delphine" | No |
    | Chassis number | Vehicle chassis number | Yes |
    | First registration date | Date of initial vehicle registration | Yes |
    | Construction year | Year the trailer was built | Yes |
    | Brand | Manufacturer brand | No |
    | Trailer number | Manufacturer serial number | No |
    | Initial customer | Historical information about original owner | No |
    | Company | Atrac or Urbain (owner entity) | Yes |
    | Pick-up location | Where the trailer is stationed | Yes |

    > [!warning]
> The plate number is the primary identifier and cannot be changed after creation. Double-check it before saving.

### Step 2: Set critical properties

Navigate to the **Properties** tab and fill in the critical properties. These determine how the trailer appears in offer and contract trailer selection filters.

    | Property | Description | Critical |
    |----------|-------------|:--------:|
    | Trailer type | Tipper (Kipper) / Walking floor (Zelflosser) / etc. | Yes |
    | Volume (m3) | Cargo volume in cubic meters | Yes |
    | Sheet type | Type of tarpaulin cover | Yes |
    | Model | Trailer model designation | Yes |
    | Door type | Type of rear door | Yes |
    | Extra options | Multi-select: floor sheet, rinse system, potato hooks, insulated, etc. | No |
    | Chassis material | Material of the chassis | No |
    | Rim material | Wheel rim material | No |
    | Empty weight (kg) | Unladen weight | No |
    | Max weight (kg) | Maximum gross weight | No |

    > [!tip]
> The five critical properties (type, volume, sheet type, model, door type) are used to filter available trailers when creating offers and contracts. Fill these in accurately to ensure correct matching.

### Step 3: Upload documents

Go to the **Documents** tab and upload essential documents:

    - **Registration certificate** (inschrijvingsbewijs) -- this is attached to contract emails
    - **Trailer photos** -- these are attached to offer emails when this trailer is selected
    - **Inspection reports** if available

    You can drag and drop files or click **Browse** to select them. Supported formats: PDF, JPEG, PNG, TIFF. Maximum file size: configurable (default 25 MB).

    > [!info]
> Select the appropriate **document type** from the dropdown for each upload. This helps organize documents and determines which files are automatically attached to emails.

### Step 4: Add the first technical inspection

Go to the **Inspections** tab and click **Add Inspection**.

    1. Enter the **valid from** date (when the current inspection was performed).
    2. Enter the **valid to** date (when the inspection expires).
    3. Save.

    The trailer's inspection status is now tracked. ARMS will generate Dashboard notifications when the inspection approaches or exceeds the warning threshold (default: 14 days before expiry).

    > [!warning]
> A trailer without a valid inspection will trigger an "Expired Inspection" notification on the Dashboard. Add the inspection record promptly to avoid false alerts.

### Step 5: Verify the trailer is available

After completing all steps:

    1. The trailer status should be **Active** (set automatically on creation).
    2. Verify the trailer appears in the **Fleet overview** with correct data.
    3. Check the **Planning** view -- the trailer should appear as a new row with no events.
    4. Test the trailer selection in the Offers module -- create a test filter matching this trailer's properties and verify it appears.

    > [!success]
> The trailer is now fully onboarded and available for offers and contracts.


## Post-onboarding checklist

Use this checklist to confirm everything is complete:

- [ ] Plate number and trailer reference are correct and unique
- [ ] Company (Atrac/Urbain) and pick-up location are set
- [ ] All five critical properties are filled in
- [ ] Registration certificate is uploaded
- [ ] At least one photo is uploaded (for offer emails)
- [ ] Technical inspection record is entered with valid dates
- [ ] Trailer appears correctly in the Fleet overview
- [ ] Trailer is visible on the Planning timeline

## Related guides

- **[[user-guide/fleet/trailer-details|Trailer Details]]** — Complete reference for all trailer detail fields and tabs.

  - **[[user-guide/fleet/inspections|Inspections]]** — Managing technical inspections and validity tracking.

  - **[[user-guide/fleet/documents|Documents]]** — Uploading and managing trailer documents.

  - **[[user-guide/fleet/status-changes|Status Changes]]** — Understanding trailer status transitions and rules.
