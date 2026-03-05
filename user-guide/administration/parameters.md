---
title: "System parameters"
description: "Configure system-wide thresholds, default values, and email templates in the ARMS parameter management screen."
---

The parameters module allows administrators to configure all system-wide thresholds, default values, and notification settings without technical intervention. This module is accessible only to users with the **Admin** role.

> [!warning]
> Only users with the Admin role can access and modify system parameters. If you do not see the Parameters option in the Administration menu, contact your system administrator.


## How parameters work

Parameters are stored as key-value pairs. Each parameter has:

| Field | Description |
|-------|-------------|
| **Key** | Unique identifier (e.g., `INSPECTION_WARNING_DAYS`) |
| **Value** | The configured value |
| **Type** | Data type: integer, decimal, boolean, text, or email_list |
| **Description (NL)** | Dutch description of the parameter's purpose |
| **Description (FR)** | French description of the parameter's purpose |

> [!info]
> Parameter changes are cached for 5 minutes (300 seconds). After you save a change, it may take up to 5 minutes for the new value to take effect across the system.


## Parameter reference

### Inspection parameters

| Key | Default | Type | Description |
|-----|---------|------|-------------|
| `INSPECTION_WARNING_DAYS` | 14 | Integer | Number of days before inspection expiry that triggers a dashboard notification and warning color |
| `INSPECTION_ALERT_RECIPIENTS` | (empty) | Email list | Comma-separated email addresses that receive inspection alert emails |

The `INSPECTION_WARNING_DAYS` parameter controls:
- The orange warning color on trailer inspection dates in the [[user-guide/fleet/overview|Fleet module]]
- The "Inspection expiring soon" [[user-guide/dashboard/notifications|notification]] on the dashboard
- The count shown in the "Inspections expiring" [[user-guide/dashboard/kpis|KPI widget]]

### Invoicing parameters

| Key | Default | Type | Description |
|-----|---------|------|-------------|
| `FORFAIT_1_DAY_EUR` | 120 | Decimal | Flat rate amount for 1-day rental contracts |
| `FORFAIT_2_DAYS_EUR` | 170 | Decimal | Flat rate amount for 2-day rental contracts |
| `KM_YEARLY_MAX` | 100,000 | Integer | Maximum kilometers per year included in contract |
| `KM_SURPLUS_PRICE_EUR` | 0.30 | Decimal | Price per extra kilometer above yearly maximum |
| `DEPOSIT_DEFAULT_AMOUNT_EUR` | 2,000 | Decimal | Default deposit amount for new contracts |

### Contract and offer parameters

| Key | Default | Type | Description |
|-----|---------|------|-------------|
| `OFFER_DUE_DATE_OFFSET_WEEKS` | 1 | Integer | Default number of weeks added to today's date for offer due dates |
| `NON_DRIVING_KM_THRESHOLD` | 10 | Integer | Km/day threshold below which non-driving days are flagged in red |
| `CONTRACT_FOLLOWUP_WARNING_DAYS` | 7 | Integer | Number of days after sending a contract before a yellow warning appears |

### Session and security parameters

| Key | Default | Type | Description |
|-----|---------|------|-------------|
| `SESSION_TIMEOUT_MINUTES` | 60 | Integer | Minutes of inactivity before automatic logout |

### Document parameters

| Key | Default | Type | Description |
|-----|---------|------|-------------|
| `MAX_UPLOAD_SIZE_MB` | 25 | Integer | Maximum file size per upload in megabytes |

### Email template parameters

ARMS stores email subject lines and body templates as parameters. These templates are used when sending offers and contracts via email.

| Key | Type | Description |
|-----|------|-------------|
| Offer email subject (NL) | Text | Subject line for Dutch offer emails |
| Offer email subject (FR) | Text | Subject line for French offer emails |
| Offer email body (NL) | Text | Body template for Dutch offer emails |
| Offer email body (FR) | Text | Body template for French offer emails |
| Contract email subject (NL) | Text | Subject line for Dutch contract emails |
| Contract email subject (FR) | Text | Subject line for French contract emails |
| Contract email body (NL) | Text | Body template for Dutch contract emails |
| Contract email body (FR) | Text | Body template for French contract emails |

Email templates support the following variables:

| Variable | Description |
|----------|-------------|
| `{{contact.first_name}}` | Contact's first name |
| `{{contact.last_name}}` | Contact's last name |
| `{{company.name}}` | Company name (Atrac or Urbain) |
| `{{offer.id}}` | Offer reference number |
| `{{contract.id}}` | Contract reference number |

## Editing a parameter

### Step 1: Open the Parameters screen

Navigate to **Administration > Parameters** in the main menu.

### Step 2: Find the parameter

Scroll through the parameter list or use the search field to locate the parameter you want to change. Parameters are grouped by category.

### Step 3: Edit the value

Click the parameter row to edit it. Enter the new value in the value field. The system validates the input against the parameter's data type.

    > [!warning]
> Verify the data type before saving. For example, entering text in an integer field will produce a validation error.

### Step 4: Save the change

Click **Save** to apply the change. The updated value is cached and takes effect within 5 minutes across the system.

    > [!success]
> A confirmation message appears when the parameter is saved. You can verify the change by refreshing the parameter list.


## Caching behavior

Parameter values are cached with a **300-second (5-minute) revalidation** interval. This means:

- After saving a change, the old value may still be used by the system for up to 5 minutes.
- Dashboard notifications, KPI calculations, and other features that depend on parameters refresh on their next data load after the cache expires.
- No manual cache clearing is needed -- the system handles revalidation automatically.

## Related pages

- **[[user-guide/administration/dropdown-values|Dropdown values]]** — Manage the values that appear in dropdown fields throughout ARMS.

  - **[[user-guide/administration/templates|Document templates]]** — Upload and manage offer and contract document templates.

  - **[[user-guide/dashboard/notifications|Notifications]]** — See how parameters affect dashboard notification thresholds.

  - **[[user-guide/dashboard/kpis|KPI widgets]]** — Understand how parameters influence KPI calculations.
