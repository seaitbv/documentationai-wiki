---
title: "Converting to contract"
description: "How to convert an accepted offer into a rental contract in ARMS, with prefilled fields and required adjustments."
---

Once a customer accepts an offer, you can convert it directly into a rental contract. ARMS prefills the contract form with data from the offer, saving you from re-entering information.

## Prerequisites

The **Create contract** button is only visible on offers with the status **Accepted**. If you do not see this button, verify that the offer status has been updated. See [[user-guide/offers/lifecycle|Offer lifecycle]] for status transition details.

## Steps to convert an offer to a contract

### Step 1: Open the accepted offer

Navigate to the offer in the [[user-guide/offers/overview|offers overview]] and open the offer detail page. Confirm the status is **Accepted**.

### Step 2: Click Create contract

Click the **Create contract** button. ARMS opens the contract creation form with fields prefilled from the offer.

### Step 3: Review prefilled fields

The following fields are automatically populated from the offer:

    | Field | Prefilled from offer |
    |-------|---------------------|
    | Company | Yes |
    | Customer | Yes |
    | Contact | Yes |
    | Language | Yes |
    | External description | Yes |
    | Unit (day/month/km) | Yes |
    | Unit price rental | Yes |
    | Discount % | Yes |
    | Insurance price | Yes |
    | Desired trailer properties | Yes |
    | Selected trailer | Yes (if one was chosen in the offer) |
    | Estimated start date | Yes (if filled in on the offer) |
    | Estimated end date | Yes (if filled in on the offer) |

    All prefilled fields are editable. Review and adjust any values before saving.

### Step 4: Assign a trailer

If no trailer was selected in the offer, you must select one now.

    > [!warning]
> A trailer is **required** in a contract, unlike in an offer where it is optional. You cannot save the contract without selecting a specific trailer.


    Use the trailer lookup to find an available trailer. The dropdown is filtered by the desired trailer properties (type, volume, sheet type, model, door type) and only shows trailers with an Active status.

### Step 5: Complete additional contract fields

Fill in any contract-specific fields that are not part of the offer, such as the contract template and deposit information. See [[user-guide/contracts/creating-contract|Creating a contract]] for the full list of contract fields.

### Step 6: Save the contract

Click **Save** to create the contract. ARMS creates the contract record and links it back to the originating offer.

    > [!success]
> After saving, the offer detail page shows the linked contract in the "Linked contract" tab, with a direct link to the contract detail.


## Key differences between offers and contracts

| Aspect | Offer | Contract |
|--------|-------|----------|
| **Trailer** | Optional | Required |
| **Estimated dates** | Optional guidance | Become the planned rental period |
| **Status flow** | Created, Sent, Accepted, Refused | Has its own lifecycle (see [[user-guide/contracts/lifecycle|Contract lifecycle]]) |
| **Invoicing** | Not invoiced | Basis for invoice generation |

## Related pages

- **[[user-guide/offers/lifecycle|Offer lifecycle]]** — Review the full offer status flow.

  - **[[user-guide/contracts/creating-contract|Creating a contract]]** — Full reference for all contract creation fields and options.

  - **[[user-guide/contracts/lifecycle|Contract lifecycle]]** — Understand the contract status flow after conversion.

  - **[[user-guide/offers/overview|Offers overview]]** — Return to the offers list to manage other offers.
