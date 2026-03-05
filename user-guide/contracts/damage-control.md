---
title: "Damage control"
description: "Track post-return trailer inspections and damage findings on contracts in ARMS."
---

After a customer returns a trailer, you need to inspect it for damage before completing the contract. The damage control tab on the contract detail screen lets you record the inspection result and link any repair work.

> [!info]
> The damage control tab becomes visible and editable only after the trailer has been returned (the contract is in "To check" status or later).


## Damage control fields

| Field | Type | Description |
|-------|------|-------------|
| **Checked** | Checkbox | Indicates whether the technical inspection has been performed |
| **Damage found** | Checkbox | Indicates whether damage was found during the inspection |
| **Repair order reference** | Text | Reference to the external repair order system for tracking repairs |

## Inspection workflow

### Step 1: Return the trailer

When the customer returns the trailer, update the contract status from "In rental" to "To check". This enables the damage control tab.

### Step 2: Perform the inspection

Physically inspect the trailer for any damage, wear, or issues.

### Step 3: Record the result

On the damage control tab:
    - Check the **Checked** checkbox to confirm the inspection is done
    - If you found damage, check the **Damage found** checkbox
    - If a repair is needed, enter the **Repair order reference** to link the external repair work

### Step 4: Complete the contract

Once the inspection is done and any repairs are resolved, mark the contract as "Completed". This triggers the automatic [[user-guide/contracts/deposits-advances|deposit credit note]].


## Yellow background warning

While a contract has outstanding damage control items, the contract row appears with a **yellow background** in the contract list and on the planning timeline. This visual indicator remains active when either:

- The **Checked** checkbox is not checked (inspection not yet performed)
- The **Damage found** checkbox is checked (damage exists that needs resolution)

> [!tip]
> The yellow background clears automatically when the linked repair order is marked as completed (either through the external system or manually). This returns the contract row and planning timeline to their normal appearance.


## Resolving damage

When damage is found, the typical resolution flow is:

1. Record the damage on the damage control tab
2. Create a repair order in your external repair system
3. Enter the repair order reference on the contract
4. Once the repair is completed, the yellow indicator clears
5. You can now mark the contract as "Completed"

> [!warning]
> You can technically mark a contract as "Completed" before the repair order is resolved, but the yellow background serves as a reminder to ensure all damage is properly handled and costs are accounted for.


## Related pages

- **[[user-guide/contracts/lifecycle|Contract lifecycle]]** — Understand the full status flow including the "To check" stage.

  - **[[user-guide/contracts/overview|Contract overview]]** — See how attention colors highlight contracts needing action.
