---
title: "Administrator"
description: "Complete guide for the Admin role with full access to all ARMS modules including system configuration"
---

## Role overview

As an Administrator, you have **full access** to every module in ARMS. You are responsible for system configuration, user management, template management, and maintaining the operational parameters that drive ARMS business logic.

> [!warning]
> The Admin role has the highest privilege level. Actions like modifying parameters, deactivating dropdown values, or changing templates affect all users immediately. Review changes carefully before saving.


## Access matrix

| Module | Access Level | Key Actions |
|--------|-------------|-------------|
| Dashboard | Full | View all KPIs, notifications, and activity |
| Fleet | Full | Create, edit, and manage all trailers, inspections, km registrations, NP periods |
| Customers | Full | Create, edit, deactivate customers and contacts |
| Offers | Full | Create, send, accept, reject, and convert offers |
| Contracts | Full | Full lifecycle management including damage control |
| Invoicing | Full | Generate proposals, create invoices, export to Exact Online |
| Planning | Full | View and interact with the Gantt timeline |
| Templates | Full | Upload, activate, deactivate, and preview document templates |
| Parameters | Full | Configure all system parameters, dropdown values, and email templates |

## Key responsibilities

### System configuration

You manage the parameters that control how ARMS behaves across all modules:

- **Inspection warning thresholds** -- how many days before an inspection expires a notification appears
- **Invoice forfait amounts** -- fixed prices for 1-day and 2-day contracts
- **Deposit defaults** -- standard deposit amount for new contracts
- **Session timeout** -- inactivity period before automatic logout
- **Offer due date offset** -- default number of weeks until an offer expires

See [[user-guide/administration/parameters|Parameters]] for the complete parameter reference.

### Dropdown value management

You control the dropdown options available across all forms:

- Trailer types, sheet types, models, door types
- Payment conditions
- Non-productive period reasons
- Document types
- Trailer extra options

See [[user-guide/administration/dropdown-values|Dropdown Values]] for management instructions.

### Template management

You manage document templates for offers and contracts per company (Atrac/Urbain) and per language (NL/FR):

- Upload new Word/HTML templates
- Set active templates per company, document type, and language
- Preview templates with sample data
- Deactivate outdated templates

See [[user-guide/administration/templates|Templates]] for details.

## Daily workflow

### Step 1: Review the Dashboard

Start your day on the Dashboard. Pay attention to:

    - **Critical notifications** (red): expired inspections, overdue offers
    - **Attention notifications** (orange): upcoming inspection expirations, contracts awaiting response
    - **KPI widgets**: click any widget to jump to the relevant filtered view

### Step 2: Address critical items

Work through critical notifications first:

    - **Expired inspections**: coordinate with the Fleet Manager to schedule inspections
    - **Overdue offers**: follow up with the Commercial team or close the offer
    - **Contracts to check**: verify returned trailers have been inspected

### Step 3: Review system health

Periodically check:

    - **Parameters**: ensure values are current (e.g., forfait prices, km thresholds)
    - **Templates**: verify active templates are up to date
    - **Dropdown values**: add new options as business needs evolve

### Step 4: Support other roles

As an Admin, you can perform any action in the system. Support your team when they encounter issues or need configuration changes.


> [!tip]
> Set up the `INSPECTION_ALERT_RECIPIENTS` parameter with email addresses of team members who should receive inspection expiration alerts. This ensures nothing is missed even when you are not checking the Dashboard.


## Related guides

- **[[user-guide/administration/parameters|Parameters]]** — Complete reference for all configurable system parameters.

  - **[[user-guide/administration/templates|Templates]]** — Managing document templates for offers and contracts.

  - **[[user-guide/administration/dropdown-values|Dropdown Values]]** — Adding and managing dropdown options across the system.

  - **[[role-guides/workflows/offer-to-cash|Offer-to-Cash Workflow]]** — End-to-end workflow from offer creation to payment.
