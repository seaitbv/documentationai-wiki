---
title: "Commercial"
description: "Guide for the Commercial role focused on customer acquisition, offer creation, and contract management"
---

## Role overview

As a Commercial user, your primary focus is on **customer relationships, offers, and contracts**. You manage the full sales cycle from customer creation through offer negotiation to contract execution. You can view fleet and planning data to inform your work but cannot modify fleet records or access invoicing.

## Access matrix

| Module | Access Level | What You Can Do |
|--------|-------------|-----------------|
| Dashboard | Full | View all KPIs, notifications, and activity |
| Fleet | Read | View trailer details, inspections, properties (no editing) |
| Customers | Full | Create, edit, and manage customers and contacts |
| Offers | Full | Create, send, accept, reject, and convert offers |
| Contracts | Full | Create, send, manage lifecycle, record non-driving days |
| Invoicing | Read | View invoice overviews (no creation or export) |
| Planning | Read | View the Gantt timeline (no modifications) |
| Templates | -- | Not visible |
| Parameters | -- | Not visible |

> [!info]
> You can see invoices linked to your contracts in read-only mode. For invoice generation and export, coordinate with the Accounting team.


## Key responsibilities

- **Customer acquisition**: create new customers with VIES-validated VAT data and maintain contact information
- **Offer management**: create, configure, and send rental offers via Outlook integration
- **Contract lifecycle**: convert accepted offers to contracts, manage signing, and track status
- **Trailer selection**: use fleet and planning views to find available trailers matching customer requirements
- **Non-driving days**: register non-driving periods for day-based contracts

## Daily workflow

### Step 1: Check the Dashboard

Review key indicators relevant to your role:

    - **Open offers**: offers in "Created" or "Sent" status needing follow-up
    - **Expiring offers**: offers approaching or past their due date
    - **Contracts awaiting response**: contracts sent more than 7 days ago without a reply
    - **Activity stream**: recent changes to your offers and contracts

### Step 2: Follow up on sent offers

Open the **Offers** module and filter on status "Sent". Check offers that are nearing their due date. Contact the customer or update the status as needed.

    > [!tip]
> Offers with a passed due date appear with a yellow badge. Address these first to keep your pipeline clean.

### Step 3: Process new customer requests

For new customers:

    1. Create the customer record with VIES validation.
    2. Add contact persons with the correct language and communication preferences.
    3. Create an offer based on the customer's requirements.
    4. Use the Planning view to check trailer availability before committing to dates.

### Step 4: Manage active contracts

Review contracts in "Accepted" and "In Rental" status:

    - Verify estimated dates are still accurate, update real pickup/dropoff dates as they become known.
    - Register non-driving day periods when customers notify you of planned downtime (day-based contracts only).
    - Coordinate with Fleet Management for trailer returns and inspections.


## Tips for offer creation

- **Check availability first**: open the [[user-guide/planning/overview|Planning]] view to see which trailers are free during the requested period.
- **Use trailer filters**: when selecting a trailer in the offer, the list is automatically filtered by the desired trailer properties you set (type, volume, sheet type, model, door type).
- **Pre-fill from customer**: selecting a customer automatically fills VAT%, payment conditions, and available contacts.
- **External description**: this text appears on the offer PDF sent to the customer. Write it clearly and professionally.

## Related guides

- **[[user-guide/customers/creating-customer|Creating a Customer]]** — Step-by-step guide for adding new customers.

  - **[[user-guide/offers/creating-offer|Creating an Offer]]** — How to create and configure a rental offer.

  - **[[role-guides/workflows/offer-to-cash|Offer-to-Cash Workflow]]** — The complete workflow from offer to payment.

  - **[[user-guide/planning/overview|Planning Overview]]** — Using the Gantt timeline to check trailer availability.
