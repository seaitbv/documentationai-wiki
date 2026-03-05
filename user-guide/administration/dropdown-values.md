---
title: "Dropdown values"
description: "Manage the centralized lookup values used in dropdown fields across ARMS, including translations and sort order."
---

The dropdown values module provides a central management screen for all dropdown fields used throughout ARMS. Administrators can add, rename, reorder, and deactivate values from a single location. This module is accessible only to users with the **Admin** role.

## How dropdown values work

ARMS uses a centralized lookup table for all dropdown fields. Each dropdown value has:

| Field | Description |
|-------|-------------|
| **Category** | The dropdown group this value belongs to (e.g., `trailer_type`) |
| **Label (NL)** | Dutch translation displayed in the interface |
| **Label (FR)** | French translation displayed in the interface |
| **Sort order** | Position in the dropdown list |
| **Active** | Whether the value appears in new form dropdowns |

The language shown in dropdown fields depends on the current user's language setting.

## Dropdown categories

The following table lists all dropdown categories and where they are used in ARMS.

| Category | Used in |
|----------|---------|
| `trailer_type` | Trailers, Offers, Contracts |
| `sheet_type` | Trailers, Offers, Contracts |
| `model` | Trailers, Offers, Contracts |
| `door_type` | Trailers, Offers, Contracts |
| `chassis_material` | Trailers |
| `rim_material` | Trailers |
| `trailer_extra_options` | Trailers (multiselect) |
| `trailer_status` | Trailers |
| `non_productive_reason` | Non-productive periods (trailers) |
| `payment_conditions` | Customers, Offers, Contracts |
| `document_type` | Documents |
| `offer_status` | Offers |
| `contract_status` | Contracts |

> [!info]
> The `trailer_type`, `sheet_type`, `model`, and `door_type` categories are considered **critical properties** for trailers. These values are used when searching for available trailers during offer and contract creation.


## Managing dropdown values

### Adding a new value

### Step 1: Open Dropdown Values

Navigate to **Administration > Dropdown Values** in the main menu.

### Step 2: Select the category

Choose the dropdown category you want to add a value to from the category list on the left.

### Step 3: Click Add Value

Click the **Add Value** button at the top of the values list.

### Step 4: Enter translations

Fill in the label for both Dutch (NL) and French (FR). Both translations are required.

### Step 5: Save

Click **Save**. The new value appears at the bottom of the list and is immediately available in all relevant dropdown fields.


> [!tip]
> You can also add dropdown values directly from any form. When filling in a dropdown field, select the **"+ New value"** option at the bottom of the list. This creates the value inline and selects it immediately.


### Renaming a value

To rename a dropdown value, click the value in the list and update the NL and/or FR label. The change applies everywhere the value is displayed, including existing records.

### Reordering values

Adjust the sort order of values using drag-and-drop in the values list. The new order is reflected in all dropdown fields throughout ARMS.

### Deactivating a value

To hide a value from new dropdown selections, toggle the **Active** switch to off.

> [!warning]
> Deactivating a value does **not** remove it from existing records. Records that already use the deactivated value retain it. The value is only hidden from dropdown selections in new or edited forms.


## Bilingual support

Every dropdown value requires both a Dutch (NL) and French (FR) translation. The system displays the translation that matches the current user's language setting.

| User language | Displayed label |
|---------------|----------------|
| NL | Dutch translation |
| FR | French translation |

If a user switches their language, all dropdown values across the interface update to the corresponding translation.

## Impact of changes on existing records

| Action | Effect on existing records |
|--------|---------------------------|
| **Rename** | Existing records display the updated label |
| **Deactivate** | Existing records keep the value; it is hidden in new dropdowns only |
| **Reorder** | Only affects the order in dropdown lists; no impact on existing records |
| **Delete** | Not supported -- use deactivation instead (soft delete) |

> [!info]
> ARMS uses soft deletion for dropdown values. You cannot permanently delete a value because it may be referenced by existing records. Deactivation is the recommended approach.


## Related pages

- **[[user-guide/administration/parameters|System parameters]]** — Configure system-wide thresholds and default values.

  - **[[user-guide/administration/templates|Document templates]]** — Upload and manage document templates for offers and contracts.
