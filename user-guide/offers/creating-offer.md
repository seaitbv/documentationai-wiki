---
title: "Creating an offer"
description: "Step-by-step guide to creating a rental offer in ARMS, including customer selection, pricing, and trailer properties."
---

When you create an offer in ARMS, you configure the customer details, rental pricing, and desired trailer properties. Many fields are automatically prefilled based on your selections to speed up the process.

## Steps to create an offer

### Step 1: Open the offer form

Navigate to **Offers** in the sidebar and click the **Add offer** button in the top-right corner.

### Step 2: Fill in the header fields

Complete the offer header with the following fields:

    | Field | Required | Behavior |
    |-------|----------|----------|
    | **Name** | Yes | A descriptive name for this offer |
    | **Company** | Yes | Select Atrac or Urbain. This determines which templates are available. |
    | **Customer** | Yes | Search and select the customer. Selecting a customer prefills VAT %, payment conditions, and the available contacts. |
    | **VAT %** | Yes | Prefilled from customer, editable per offer |
    | **Payment conditions** | Yes | Prefilled from customer, editable per offer |
    | **Contact** | Yes | Dropdown filtered to contacts of the selected customer. Selecting a contact prefills the language. |
    | **Template** | Yes | Dropdown filtered by the selected company |
    | **Language** | Yes | Prefilled from contact, editable |
    | **Status** | Yes | Defaults to "Created" |
    | **Due date** | Yes | Defaults to today plus a configurable number of weeks (set in [[user-guide/administration/parameters|Parameters]]) |
    | **Internal description** | No | Notes visible only to your team, not included in the offer document |
    | **External description** | No | Text that appears on the generated offer document |

    > [!tip]
> Select the customer first. This prefills VAT %, payment conditions, and filters the contact dropdown -- saving you time and reducing errors.

### Step 3: Enter rental details

Configure the pricing and rental period:

    | Field | Required | Description |
    |-------|----------|-------------|
    | **Estimated start date** | No | Expected rental start date (not always known at offer stage) |
    | **Estimated end date** | No | Expected rental end date |
    | **Unit** | Yes | Billing unit: day, month, or km |
    | **Unit price rental** | Yes | Price per selected unit |
    | **Discount %** | No | Percentage discount applied to the rental price only (not insurance) |
    | **Insurance price** | No | Insurance cost per unit. No discount is applied to this amount. |

    > [!info]
> The discount percentage applies only to the rental unit price. Insurance pricing is always charged at full rate.

### Step 4: Specify desired trailer properties

Define the type of trailer the customer needs:

    | Field | Required | Description |
    |-------|----------|-------------|
    | **Trailer type** | Yes | Select from the configured trailer types (e.g., tipper, walking floor) |
    | **Volume** | No | Desired trailer volume |
    | **Sheet type** | No | Type of sheet / cover |
    | **Model** | No | Specific trailer model |
    | **Door type** | No | Type of rear door |
    | **Selected trailer** | No | Optional. Lookup filtered by the properties above. Only Active trailers are shown. |

    > [!tip]
> Fill in the trailer properties first to narrow down the **Selected trailer** dropdown. The system automatically filters available trailers based on your selections.


    > [!info]
> Selecting a specific trailer is optional in an offer. If you do select one, the trailer's photos are attached when you [[user-guide/offers/sending-outlook|send the offer via Outlook]].

### Step 5: Save the offer

Click **Save** to create the offer. The offer is saved with the status "Created" and appears in the [[user-guide/offers/overview|offers list]].


## Prefill behavior summary

When you select a customer and contact, several fields are automatically populated:

| Selection | Fields prefilled |
|-----------|-----------------|
| **Customer** | VAT %, payment conditions, available contacts |
| **Contact** | Language |
| **Company** | Available templates |
| **Trailer properties** | Available trailers in the Selected trailer dropdown |

All prefilled values are editable before saving.

## What happens next

After saving an offer, you can:

- **Send it to the customer** via Outlook -- see [[user-guide/offers/sending-outlook|Sending via Outlook]]
- **Track its status** through the lifecycle -- see [[user-guide/offers/lifecycle|Offer lifecycle]]
- **Convert it to a contract** once accepted -- see [[user-guide/offers/converting-to-contract|Converting to contract]]

## Related pages

- **[[user-guide/customers/overview|Customer overview]]** — Browse customers before creating an offer.

  - **[[user-guide/offers/sending-outlook|Sending via Outlook]]** — Send the completed offer to your customer.
