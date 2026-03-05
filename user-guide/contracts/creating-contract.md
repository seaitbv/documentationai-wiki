---
title: "Creating a contract"
description: "Learn how to create a new rental contract in ARMS, either from scratch or from an accepted offer."
---

You can create a rental contract in two ways: from scratch or by converting an accepted offer. When you create a contract from an offer, key fields are prefilled automatically.

## Starting a contract

#### From scratch

Click the **Add contract** button on the [[user-guide/contracts/overview|contract overview]]. This opens a blank contract form where you fill in all fields manually.

#### From an accepted offer

On the offer detail screen, click **Convert to contract**. ARMS creates a new contract with the customer, trailer, pricing, and company fields prefilled from the offer. You can adjust any value before saving.

    See [[user-guide/offers/converting-to-contract|Converting to contract]] for more details.


## Contract header fields

The header section captures the core contract information.

| Field | Required | Description |
|-------|----------|-------------|
| **Contract ID** | Auto | System-generated unique identifier |
| **Name** | Yes | A descriptive name for the contract |
| **Company** | Yes | The entity (Atrac or Urbain) |
| **Customer** | Yes | Lookup field; prefilled from offer when applicable |
| **VAT %** | Yes | Prefilled from the customer record |
| **Payment conditions** | Yes | Prefilled from the customer record |
| **Contact** | Yes | Dropdown filtered by the selected customer |
| **Contract template** | Yes | Dropdown filtered by the selected company |
| **Language** | Yes | Prefilled from the selected contact's language |
| **Status** | Yes | Starts as "Created" for new contracts |
| **Internal description** | No | Notes visible only to your team |
| **External description** | No | Appears on the contract document |
| **Free text notes** | No | Internal notes for additional context |

> [!tip]
> The VAT percentage and payment conditions are automatically loaded from the customer record. If these values change, update them on the [[user-guide/customers/overview|customer detail]] screen first.


## Rental period

The rental period defines when the trailer is rented. You must always set estimated dates. Real dates are filled in when the trailer is physically picked up and returned.

| Field | Required | Description |
|-------|----------|-------------|
| **Estimated start date** | Yes | The planned start of the rental |
| **Estimated end date** | Yes | The planned end of the rental |
| **Real start date (pickup)** | No | The actual date the customer picks up the trailer |
| **Real end date (dropoff)** | No | The actual date the customer returns the trailer |

> [!info]
> ARMS uses the real dates for all invoicing, planning, and availability calculations when they are available. Otherwise, it falls back to the estimated dates. Always update the real dates when the trailer is physically picked up or returned.


## Rental details

The rental details define the pricing and billing setup for the contract.

| Field | Required | Description |
|-------|----------|-------------|
| **Unit** | Yes | The billing unit: day, month, or km |
| **Unit price (rental)** | Yes | The price per unit for the trailer rental |
| **Discount (%)** | No | Percentage discount applied to the rental price only |
| **Unit price (insurance)** | No | The price per unit for insurance; defaults to 0 if left empty |
| **Trailer** | Yes | The trailer to rent; filtered by desired properties. Displays the trailer's display name. |
| **Invoice-to** | Yes | Who receives the invoices. Defaults to the selected customer. Alternatives: Atrac/Urbain (as a commercial gesture) or STAS (for warranty cases). |

> [!warning]
> A trailer is **required** on every contract. The trailer dropdown only shows trailers that match the selected properties and are available for the contract period.


> [!info]
> The discount percentage applies **only** to the rental price, not to insurance. Insurance is always invoiced at its full unit price with 0% VAT.


## Saving the contract

### Step 1: Fill in all required fields

Complete the header, rental period, and rental details sections. Required fields are marked with an asterisk.

### Step 2: Review the deposit and advance

ARMS automatically calculates the deposit and advance amounts based on the unit and price. You can adjust these values if needed. See [[user-guide/contracts/deposits-advances|Deposits and advances]] for calculation details.

### Step 3: Save the contract

Click **Save** to create the contract. It appears in the contract list with the status "Created".


## Next steps

After creating a contract, you typically:

1. Review the contract document preview on the **Contract visualization** tab
2. Send the contract to the customer via email. See [[user-guide/contracts/sending-outlook|Sending via Outlook]].

## Related pages

- **[[user-guide/contracts/deposits-advances|Deposits and advances]]** — Understand how deposit and advance amounts are calculated.

  - **[[user-guide/contracts/lifecycle|Contract lifecycle]]** — Follow the contract through its full status flow.
