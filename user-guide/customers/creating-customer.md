---
title: "Creating a customer"
description: "Step-by-step guide to adding a new customer in ARMS, including VIES validation and financial settings."
---

When you create a new customer in ARMS, the system guides you through entering identification details, validating the VAT number via VIES, and setting up financial information.

> [!warning]
> Only users with the **Admin** or **Commercial** role can create customers.


## Steps to create a customer

### Step 1: Open the customer form

Navigate to **Customers** in the sidebar and click the **Add customer** button in the top-right corner.

### Step 2: Enter the working name

Type the **working name** for this customer. This is the name your team uses internally and does not need to match the official company name.

    > [!tip]
> Choose a working name that your colleagues will recognize quickly. For example, use a common abbreviation or the name your sales team uses in conversations.

### Step 3: Validate the VAT number

Enter the customer's **VAT number** and click the **Check VIES** button. If validation succeeds, the following fields are automatically filled in:

    - Official name
    - Street and number
    - Postal code
    - City
    - Country

    All auto-filled fields remain editable. See [[user-guide/customers/vies-validation|VIES validation]] for details on the three possible outcomes.

### Step 4: Review and adjust company details

Verify the auto-filled fields and correct them if needed. If VIES was unavailable or the VAT number was not found, fill in these fields manually:

    | Field | Required | Description |
    |-------|----------|-------------|
    | **Official name** | Yes | Legal company name |
    | **Street** | Yes | Street name |
    | **Number** | Yes | Street number |
    | **Postal code** | Yes | Postal / ZIP code |
    | **City** | Yes | City name |
    | **Country** | Yes | Country of registration |

### Step 5: Set financial information

Fill in the financial details for this customer:

    | Field | Required | Description |
    |-------|----------|-------------|
    | **VAT percentage** | Yes | Default VAT rate applied to offers and invoices for this customer |
    | **Payment conditions** | Yes | Select from the dropdown (e.g., "30 days net", "15 days", "Payment on collection") |

    > [!info]
> The VAT percentage and payment conditions you set here are automatically prefilled when you create an offer or contract for this customer. You can override them per offer or contract.

### Step 6: Save the customer

Click **Save** to create the customer record. ARMS validates that all required fields are completed before saving. The new customer appears in the [[user-guide/customers/overview|customer list]] with an **Active** status.


## Field reference

| Field | Required | Source |
|-------|----------|--------|
| Working name | Yes | Manual entry |
| VAT number | Yes | Manual entry |
| Official name | Yes | VIES or manual |
| Street | Yes | VIES or manual |
| Number | Yes | VIES or manual |
| Postal code | Yes | VIES or manual |
| City | Yes | VIES or manual |
| Country | Yes | VIES or manual |
| VAT percentage | Yes | Manual entry |
| Payment conditions | Yes | Dropdown selection |

## Related pages

- **[[user-guide/customers/vies-validation|VIES validation]]** — Understand VIES outcomes and troubleshooting steps.

  - **[[user-guide/customers/contacts|Contacts]]** — Add contact persons to your newly created customer.
