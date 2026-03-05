---
title: "VIES validation"
description: "How ARMS validates VAT numbers through the EU VIES system and what to do when validation fails."
---

ARMS integrates with **VIES** (VAT Information Exchange System) to automatically validate customer VAT numbers and retrieve official company details. This ensures accurate customer data and reduces manual data entry.

## What is VIES?

VIES is a service operated by the European Commission that allows businesses to verify the validity of VAT numbers issued by EU member states. When you enter a VAT number in ARMS and click **Check VIES**, the system queries this service in real time.

## How to use VIES validation

### Step 1: Enter the VAT number

Type the customer's VAT number in the VAT number field. Use the standard format with the country prefix (e.g., `BE0123456789`, `NL123456789B01`, `DE123456789`).

    > [!tip]
> You can enter the VAT number with or without dots and spaces. ARMS normalizes the format automatically before querying VIES.

### Step 2: Click Check VIES

Click the **Check VIES** button next to the VAT number field. The system queries the EU VIES database and returns one of three outcomes described below.

### Step 3: Review the result

Check the validation message and verify the auto-filled fields if applicable.


## Possible outcomes

### Success: VAT number is valid

A green confirmation message appears: *"VAT number valid -- details filled in."*

The following fields are automatically populated from the VIES response:

- Official name
- Street and number
- Postal code
- City
- Country

All auto-filled fields remain fully editable. Review the data and adjust where needed before saving.

> [!success]
> A successful VIES check gives you confidence that the customer's VAT registration is active and the company details are up to date.


### Invalid: VAT number not found

A red error message appears: *"VAT number not found in VIES."*

This means the VAT number is not registered in the VIES database. The auto-fill fields remain empty. Possible causes:

- The VAT number contains a typo
- The number belongs to a non-EU country (VIES only covers EU member states)
- The company's VAT registration has been deactivated

You can still fill in all company details manually and save the customer.

> [!warning]
> Double-check the VAT number format with the customer before proceeding with manual entry. An incorrect VAT number can cause invoicing issues later.


### Unavailable: VIES service is down

An orange warning message appears: *"VIES service temporarily unavailable -- fill in details manually."*

The VIES service experiences occasional downtime for maintenance. The form remains fully editable so you can enter all fields manually.

> [!info]
> If VIES is unavailable, you can save the customer now and re-validate the VAT number later by editing the customer and clicking **Check VIES** again.


## VAT number format reference

| Country | Format | Example |
|---------|--------|---------|
| Belgium | BE + 10 digits | `BE0123456789` |
| Netherlands | NL + 9 digits + B + 2 digits | `NL123456789B01` |
| Germany | DE + 9 digits | `DE123456789` |
| France | FR + 2 chars + 9 digits | `FR12345678901` |
| Luxembourg | LU + 8 digits | `LU12345678` |

> [!tip]
> Always include the two-letter country prefix. Without it, VIES cannot identify which national database to query.


## Related pages

- **[[user-guide/customers/creating-customer|Creating a customer]]** — Full procedure for adding a customer with VIES validation.

  - **[[user-guide/customers/overview|Customer overview]]** — Browse and filter your complete customer list.
